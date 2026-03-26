# Conversor de cartolas bancarias

Herramienta web (HTML + JavaScript) que lee cartolas exportadas en **`.xlsx`** o **`.xls`** y genera archivos normalizados para importación contable: un **Excel** y un **texto delimitado por tabulaciones**, con la misma estructura de encabezado, movimientos, totales y línea de cierre.

## Requisitos

- Navegador actual (Chrome, Edge, Firefox, etc.).
- Conexión a internet la primera vez que cargas la página: la librería [SheetJS](https://sheetjs.com/) se incluye vía CDN (`cdnjs`). Si trabajas sin red, descarga `xlsx.full.min.js` y apunta el `<script>` del HTML a una copia local.

## Cómo usar

1. Abre **`index-v03.html`** en el navegador (doble clic o “Abrir con…”).
2. Elige el **banco** en el paso 1.
3. Arrastra los archivos a la zona de carga o haz clic para seleccionarlos.
4. Revisa la vista previa (período, saldos, movimientos).
5. Descarga **`.xlsx`** y **`.txt`** cuando el procesamiento sea correcto.

Para cartolas **Santander** con el flujo heredado de la primera versión, también existe **`index.html`** (un solo archivo, lógica v1).

## Bancos soportados (`index-v03.html`)

| Banco | Archivos | Notas |
|--------|----------|--------|
| **Santander** | 1 | Misma lógica que `index.html` v1 (`Detalle movimientos`). |
| **BCI** | 1 o más | Encabezado de tabla por nombres de columna (incl. huecos entre Fecha, Sucursal, Descripción, cargos/abonos). Opcional: sobrescribir N° cartola y fechas del período. |
| **Banco Estado** | 1 o más | Se prioriza la hoja **`Movimientos`** de cada libro. Mismos ajustes opcionales de período que BCI. |
| **Banco de Chile** | 1 | Varias hojas: se usa la que aporte más movimientos; columnas por etiqueta (cartolas con celdas vacías entre columnas). |
| **Itaú** | 1 | Parser dedicado. |
| **Scotiabank** | 1 | Encabezado por nombre de columna; se barren todas las hojas. |
| **Otro banco** | 1 | Modo genérico con detección automática limitada; conviene probar con el banco explícito si existe. |

Si subes varios archivos en un banco que solo admite uno, se usa el primero y se muestra una advertencia.

## Formato de salida

- **Primera fila / línea:** mes, año, saldo inicial, fecha desde, fecha hasta, saldo final.
- **Movimientos:** correlativo, fecha (`DD/MM/YYYY`), tipo (`DP` / `CB`), número de documento, cargo, abono.
- **Penúltima fila:** totales de cargos y abonos.
- **Última fila:** cierre con `0` en la última columna (según implementación de `buildXlsx` / `buildTxt`).

Detalle del contrato y del contexto del proyecto: **`CONTEXT.md`**.

## Estructura del repositorio (referencia)

- `index.html` — conversor v1 (énfasis Santander).
- `index-v03.html` — conversor multi-banco v3.
- `CHANGELOG.md` — registro de versiones.
- `archive-example/` — ejemplos de entrada (cuando existan).

## Privacidad

Todo el procesamiento ocurre **en el navegador**; los archivos no se suben a ningún servidor.
