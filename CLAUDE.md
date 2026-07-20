# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal data management project for tracking land rental ("arriendo") transactions related to a property called "Cucuter" in Chile. This is a financial/legal documentation project, not a software application.

## Contrato de Arriendo

### Acuerdo Privado de Arriendo
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

## Data Structure

```
DATA_RAW/
├── Contrato arriendo Cucuter.pdf    # Contrato original con planos y escritura
├── Cuenta Jorge Carrizo.xlsx        # Master ledger with payment tracking
├── Bancos/
│   ├── MACH/                        # Cartolas MACH (protegidas, clave: 26797308)
│   ├── MACH_unlocked/               # Cartolas desbloqueadas 2024-2025
│   ├── Banco Estado Cuenta RUT/     # Cartolas Banco Estado
│   ├── Banco Santander Cuenta Corriente/
│   ├── Falabella Cuenta Corriente/
│   └── Falabella CMR/
├── WhatsApp Chat - Jorge Carrizo Terreno Cucuter/
│   ├── _chat.txt                    # Chat actual (export Abr 2026, Oct 2024 - Abr 2026)
│   ├── *.jpg                        # Transfer receipts and photos
│   ├── *.opus                       # Voice messages (12 archivos, transcritos)
│   └── *.vcf                        # Contact card
├── WhatsApp Chat - Jorge Carrizo Terreno Cucuter (export 2025-12-22)/
│   └── ...                          # Export anterior (respaldo)
├── todas_transferencias_jorge.csv   # Consolidado de cartolas bancarias + WhatsApp
├── analisis_completo_jorge.csv      # Análisis cruzado Excel + Cartolas + WhatsApp
└── resumen_financiero.csv           # Resumen ejecutivo
```

## Financial Summary (Actualizado Abr 2026)

### Estado del Contrato
| Concepto | Valor |
|----------|-------|
| **Meses transcurridos** | 50 meses (Feb 2022 - Abr 2026) |
| **Total adeudado** | $9,000,000 CLP |
| **Total verificado** | $5,900,000 CLP |
| **Período cartolas** | Jul 2023 - Jul 2025 |
| **Comprobantes WhatsApp** | Dic 2025 - Mar 2026 |

### Análisis de Pagos por Fuente
| Fuente | Transacciones | Monto | Estado |
|--------|---------------|-------|--------|
| ✅ Verificadas (Excel + Cartola) | 41 | $2,940,000 | Confirmado |
| 🏦 Solo en Cartola Bancaria | 19 | $1,640,000 | Falta en Excel |
| 📊 Solo en Excel | 10 | $800,000 | Sin respaldo |
| 📸 Comprobante WhatsApp | 3 | $520,000 | Verificado con imagen |
| **TOTAL** | **73** | **$5,900,000** | |

### Resumen por Año
| Año | Transacciones | Monto |
|-----|---------------|-------|
| 2023 | 4 | $280,000 |
| 2024 | 48 | $3,890,000 |
| 2025 | 19 | $1,480,000 |
| 2026 | 2 | $250,000 |

### Cuenta Detallada (desde Jun 2024)
- **Meses completamente cubiertos**: 23 (Jun 2024 - Abr 2026)
- **Total pagado (registrado)**: $4,260,000 CLP
- **Mayo 2026**: $70,000 de $180,000 (faltan $110,000)

### ⚠️ Período Sin Cartolas Disponibles
- **Feb 2022 - Jun 2023**: ~17 meses sin cartolas bancarias
- **Arriendo de ese período**: $3,060,000 CLP
- **Estado estimado**: Si período faltante pagado → Pendiente ~$40,000

## Context

- **Parties**: Cristian Mendiola (property renter) ↔ Jorge Carrizo (property owner)
- **Property**: Terreno Cucuter, Lote #4 Subdivisión Lote 6C
- **Transaction Type**: Land rental payments and advance loans
- **Currency**: Chilean Pesos (CLP), amounts referenced in thousands (e.g., "30" = 30,000 CLP)
- **Date Format**: DD-MM-YY (Chilean format)
- **Time Period**: Feb 2022 - Abr 2026 (contrato y transferencias)

## Data Interpretation Notes

- "me anote X" = request for loan of X thousand pesos
- "imagen omitida" = transfer receipt screenshot (proof of payment)
- "audio omitido" = voice message (context may be missing)
- Photos with transfer prefix contain payment confirmations
- Payments are tracked against future rent (adelanto del arriendo)
- TEF = Transferencia Electrónica de Fondos

## Archivos Generados

- **[index.html](index.html)** - Página web con transferencias del Excel + comprobantes WhatsApp
- **[analisis_consolidado.html](analisis_consolidado.html)** - Análisis bancario completo con info del contrato
- **[analisis_bancario.html](analisis_bancario.html)** - Detalle de transacciones por banco
- **[cuenta_detallada.html](cuenta_detallada.html)** - Cuenta mes a mes con desglose de pagos y comprobantes
- **[comprobantes/](comprobantes/)** - 11 imágenes de transferencias (renombradas por fecha y monto)

## Tareas Completadas (Dic 2025)

- ✅ Análisis cruzado Excel vs Imágenes de comprobantes WhatsApp
- ✅ Identificación de 8 transferencias faltantes en Excel ($420,000)
- ✅ Actualización del Excel con las 8 transferencias nuevas
- ✅ Desbloqueo de cartolas MACH (23 archivos 2024-2025)
- ✅ Extracción de transacciones de Banco Estado CuentaRUT
- ✅ Cruce de datos: 70 transacciones totales a Jorge Carrizo
- ✅ Creación de páginas web consolidadas
- ✅ Análisis del contrato de arriendo

## Tareas Completadas (Abr 2026)

- ✅ Incorporación de nuevo export WhatsApp (Oct 2024 - Abr 2026)
- ✅ Transcripción de 12 audios con whisper.cpp
- ✅ Identificación de 3 nuevas transferencias ($520,000) con comprobante
- ✅ Actualización de CSVs y páginas HTML
- ✅ Extensión de cuenta detallada hasta Mayo 2026 (parcial)

## Tareas Pendientes

- Obtener cartolas del período Feb 2022 - Jun 2023 para completar análisis
- Reconciliar 10 transacciones del Excel sin respaldo bancario encontrado
- Agregar 19 transacciones de cartolas que faltan en Excel
- Obtener cartolas Banco Estado Ago 2025 - Mar 2026 para cruzar con comprobantes WhatsApp

## Proceso de Actualización de Cuentas

Cuando el usuario entrega nuevos pagos (comprobantes, chat de WhatsApp, o indicación verbal), seguir este proceso:

### Paso 1: Extraer transferencias
- **Imagen de comprobante**: Leer fecha, monto, N° operación, mensaje
- **Export WhatsApp (.zip)**: Descomprimir, leer `_chat.txt`, identificar transferencias ("imagen omitida" = comprobante), transcribir audios con `whisper-cli`
- **Indicación verbal**: Confirmar fecha y monto

### Paso 2: Verificar contra Google Sheet
Leer hoja "Cuenta Actualizada (Abr 2026)" via API para obtener último mes cubierto, saldo y total. Verificar que no sean duplicados (por N° operación o fecha+monto).

### Paso 3: Calcular asignación mensual
```
carry_anterior + pagos >= $180,000 → mes PAGADO, excedente pasa al siguiente
carry_anterior + pagos < $180,000  → mes PARCIAL
```

### Paso 4: Actualizar Google Sheet
Escribir nuevas filas en la hoja. Las fórmulas SUMPRODUCT en columna H calculan subtotales automáticamente. Columna J (Balance = H-I) verifica el cálculo. Fila de VERIFICACION al final confirma que totales coinciden.

### Paso 5: Actualizar docs/index.html
Modificar los 4 bloques de datos JS:
1. `comprobantes{}` - nuevas imágenes
2. `transaccionesDB{}` - metadata de cada transferencia
3. `accountData[]` - meses con transacciones y carries
4. Summary cards y totales

### Paso 6: Copiar comprobantes
Si hay imágenes, copiar a `docs/comprobantes/` con formato `YYYY-MM-DD_MONTO.jpg`.

### Paso 7: Commit, push y deploy
```bash
git add docs/
git commit -m "Descripción de transferencias"
git push origin main
```

### Paso 8: Verificación cruzada
Leer Google Sheet via API y comparar totales de fórmulas contra HTML. Si coinciden, reportar. Si no, investigar.

### Fuentes autoritativas (en orden)
1. **Cartolas bancarias** (fecha efectiva de la transacción)
2. **Comprobantes de WhatsApp** (imagen del comprobante)
3. **Excel** (registro manual, puede tener errores de fecha ±1-2 días)

## Google Sheet (Respaldo con Verificación)

- **URL**: https://docs.google.com/spreadsheets/d/15sx3-mMtU6Px_XoShTjIm0ee9cQ95rPgtAc9xkNk5ng/
- **Hoja activa**: "Cuenta Actualizada (Abr 2026)" (gid: 936718897)
- **Acceso**: Service account `supabase-sheets-sync@serious-ascent-486416-n8.iam.gserviceaccount.com`
- **Credentials**: `/Volumes/LaCiE/Claude Code Projects/New-reservas.atacamastargazing.com/credentials/service-account-key.json`
- **Estructura**: Columnas A-J (Mes, Fecha, Tipo, Monto, Fuente, N°Op, Notas, Subtotal, Arriendo, Balance)
- **Fórmulas**: Columna H=SUMPRODUCT pagos, I=arriendo fijo, J=H-I (balance), fila 94=totales

## GitHub Pages (Compartido con Jorge)

- **URL**: https://mendiolacristian.github.io/arriendo-cucuter/
- **Contraseña**: RUT de Jorge (12.049.525-9 / 12049525-9 / 120495259)
- **Archivo**: docs/index.html (con login por RUT)
- **Comprobantes**: docs/comprobantes/ (imágenes renombradas YYYY-MM-DD_MONTO.jpg)

## Technical Notes

- **MACH PDFs**: Protegidos con contraseña `26797308` (RUT del titular)
- **Extracción**: Usar `pdfplumber` para extraer texto de cartolas
- **Desbloqueo**: Usar `pikepdf` para remover protección de PDFs
- **Transcripción**: `whisper-cli -m /opt/homebrew/share/whisper-cpp/ggml-medium.bin -f audio.wav --no-timestamps -l es`
- **Audio conversion**: `ffmpeg -i input.opus -ar 16000 -ac 1 -c:a pcm_s16le output.wav`

## Infrastructure Reference

Technical stack inventory: `/Volumes/LaCiE/Claude Code Projects/technical-infrastructure/inventory.yaml`

## Privacy Considerations

This repository contains personal financial communications. Audio files and photos may contain sensitive information.
