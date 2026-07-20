# CLAUDE.md

Proyecto personal de documentación financiera/legal del arriendo del terreno "Cucuter"
(San Pedro de Atacama). No es una aplicación de software: los entregables son el Google
Sheet de cuentas y la página publicada en GitHub Pages.

> **El estado financiero vigente vive en el Google Sheet + `docs/index.html` — NUNCA en
> este archivo.** No copiar tablas de saldos/meses aquí: caducan con cada pago y este
> archivo ya llegó a contradecir los totales corregidos del repo.

## Contrato de Arriendo (Acuerdo Privado)

| Campo | Valor |
|-------|-------|
| **Fecha de Firma** | 22 de Febrero 2022 |
| **Duración** | 5 años con opción a compra (hasta 22/02/2027) |
| **Arrendador** | Jorge Andrés Carrizo Rojas (RUT: 12.049.525-9) |
| **Arrendatario** | Cristian Manuel Mendiola Alcalde (RUT: 26.797.308-3) |
| **Empresa** | AtacamaStargazing |
| **Propiedad** | Lote #4, PLANO DE SUBDIVISIÓN LOTE 6C |
| **Ubicación** | San Pedro de Atacama, Ayllu de Cucuter, II Región Antofagasta |
| **Valor Mensual** | $180,000 CLP |
| **Fecha de Pago** | Últimos cinco días de cada mes |

Contrato original (con planos y escritura): `DATA_RAW/Contrato arriendo Cucuter.pdf`.

## Estado Financiero

- Fuente vigente: Google Sheet (sección abajo) y `docs/index.html`. Leerlos SIEMPRE
  antes de reportar saldos o meses cubiertos.
- Última corrección verificada (10/04/2026, commits `4b26260` + `dcbd323`): $4,500,000
  registrados (25 meses, Jun 2024 - Jun 2026), **al día hasta Junio 2026**. Cualquier
  cifra distinta en documentos viejos es pre-corrección.

## Data Interpretation Notes

- Montos referidos en miles: "30" = $30,000 CLP · fechas en formato chileno DD-MM-YY
- "me anote X" = solicitud de préstamo de X mil pesos
- "imagen omitida" = screenshot de comprobante de transferencia (prueba de pago)
- "audio omitido" = mensaje de voz (puede faltar contexto)
- Fotos con prefijo de transferencia contienen confirmaciones de pago
- Los pagos se abonan contra arriendo futuro (adelanto del arriendo)
- TEF = Transferencia Electrónica de Fondos

### Fuentes autoritativas (en orden)

1. **Cartolas bancarias** (fecha efectiva de la transacción)
2. **Comprobantes de WhatsApp** (imagen del comprobante)
3. **Excel** (registro manual, puede tener errores de fecha ±1-2 días)

## Proceso de Actualización de Cuentas

Cuando el usuario entrega nuevos pagos (comprobantes, export de WhatsApp, o indicación verbal):

1. **Extraer transferencias** — imagen: leer fecha, monto, N° operación, mensaje. Export
   WhatsApp (.zip): descomprimir, leer `_chat.txt` ("imagen omitida" = comprobante),
   transcribir audios (pipeline whisper.cpp del CLAUDE.md global). Verbal: confirmar
   fecha y monto.
2. **Verificar contra Google Sheet** — leer la hoja de cuenta vigente vía API (anclar
   por gid; el nombre de la hoja rota por ciclo): último mes cubierto, saldo y total.
   Descartar duplicados (por N° operación o fecha+monto).
3. **Asignación mensual con carry**: `carry_anterior + pagos >= $180,000` → mes PAGADO,
   excedente pasa al siguiente; si no alcanza → mes PARCIAL.
4. **Actualizar Google Sheet** — escribir nuevas filas; SUMPRODUCT en columna H calcula
   subtotales, columna J (Balance = H−I) verifica, fila VERIFICACION final confirma totales.
5. **Actualizar `docs/index.html`** — 4 bloques de datos JS: `comprobantes{}` (imágenes),
   `transaccionesDB{}` (metadata por transferencia), `accountData[]` (meses y carries),
   summary cards y totales.
6. **Copiar comprobantes** — imágenes a `docs/comprobantes/` como `YYYY-MM-DD_MONTO.jpg`.
7. **Commit, push y deploy** — `git add docs/ && git commit && git push origin main`
   (GitHub Pages publica desde `docs/`).
8. **Verificación cruzada** — releer el Sheet vía API y comparar totales de fórmulas
   contra el HTML. Si coinciden, reportar; si no, investigar antes de cerrar.

## Google Sheet (Respaldo con Verificación)

- **URL**: https://docs.google.com/spreadsheets/d/15sx3-mMtU6Px_XoShTjIm0ee9cQ95rPgtAc9xkNk5ng/
- **Hoja de cuenta vigente**: anclar por **gid 936718897** — el nombre rota por ciclo
  (último conocido: "Cuenta Actualizada (Abr 2026)")
- **Acceso**: service account `supabase-sheets-sync@serious-ascent-486416-n8.iam.gserviceaccount.com`
- **Key local**: `/Volumes/LaCiE/Claude Code Projects/New-reservas.atacamastargazing.com/credentials/service-account-key.json`
- **Estructura**: columnas A-J (Mes, Fecha, Tipo, Monto, Fuente, N°Op, Notas, Subtotal, Arriendo, Balance)
- **Fórmulas**: H=SUMPRODUCT pagos, I=arriendo fijo, J=H−I (balance), fila final de totales

## GitHub Pages (Compartido con Jorge)

- **URL**: https://mendiolacristian.github.io/arriendo-cucuter/
- **Contraseña**: RUT de Jorge (12.049.525-9 / 12049525-9 / 120495259)
- **Archivo publicado**: `docs/index.html` (login por RUT). Los HTML de la raíz
  (`index.html`, `cuenta_detallada.html`, `analisis_*.html`) son legacy gitignored — NO editarlos.
- **Comprobantes**: `docs/comprobantes/` (renombrados `YYYY-MM-DD_MONTO.jpg`)

## Datos Crudos (`DATA_RAW/`, gitignored)

- `Cuenta Jorge Carrizo.xlsx` — master ledger manual de pagos
- `Bancos/MACH/` — cartolas protegidas (clave abajo); `Bancos/MACH_unlocked/` — ya desbloqueadas
- `WhatsApp Chat - Jorge Carrizo Terreno Cucuter/` — export VIGENTE; el directorio con
  sufijo `(export 2025-12-22)` es el respaldo anterior (cubre mensajes previos al inicio
  del export vigente — no borrarlo)
- CSVs consolidados (`todas_transferencias_jorge`, `analisis_completo_jorge`,
  `resumen_financiero` y derivados de cruces Excel/cartolas/WhatsApp)

## Technical Notes

- **MACH PDFs**: protegidos con contraseña `26797308` (RUT del titular)
- **Extracción de cartolas**: `pdfplumber` · **Desbloqueo de PDFs**: `pikepdf`
- **Transcripción de audios**: pipeline whisper.cpp/ffmpeg del CLAUDE.md global

## Tareas Pendientes (lista del ciclo Dic 2025 — re-verificar contra el Sheet antes de usar)

- Obtener cartolas del período Feb 2022 - Jun 2023 (~17 meses sin respaldo bancario)
- Reconciliar 10 transacciones del Excel sin respaldo bancario encontrado
- Agregar 19 transacciones de cartolas que faltan en Excel
- Obtener cartolas Banco Estado Ago 2025 - Mar 2026 para cruzar con comprobantes WhatsApp

## Privacy Considerations

This repository contains personal financial communications. Audio files and photos may
contain sensitive information.
