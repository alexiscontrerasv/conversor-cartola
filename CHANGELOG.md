## [1.2.6] - 2026-03-26

### Changed - Documentación

- **Archivos modificados**: `README.md`, `CHANGELOG.md`
- `README.md` describe el propósito del proyecto, requisitos (CDN SheetJS), uso de `index-v03.html` y `index.html`, tabla de **bancos soportados**, formato de salida, referencia a `CONTEXT.md` y tratamiento de datos en cliente.

## [1.2.5] - 2026-03-26

### Fixed - Scripts

- **Archivos modificados**: `index-v03.html`, `CHANGELOG.md`
- BCI: los movimientos se leen por **índice de columna según el encabezado** (Fecha, Descripción, **Cheques y otros cargos**, **Depósitos y Abono**, N° Documento), no por posiciones fijas; corrige cartolas con **columnas vacías** entre sucursal y descripción donde antes casi no se importaban filas.

## [1.2.4] - 2026-03-26

### Fixed - Scripts

- **Archivos modificados**: `index-v03.html`, `CHANGELOG.md`
- Scotiabank: encabezado detectado por **nombres de columna** (reutilizando normalización tipo Banco de Chile), lectura de **Fecha / Descripción / N° Doc. / Cargos / Abonos / Saldo** aunque la tabla empiece en columna B u haya huecos; **N° documento** desde celda cuando aplica; recorrido de **todas las hojas** del libro y elección de la que aporte más movimientos (p. ej. hoja `Data`).

## [1.2.3] - 2026-03-26

### Fixed - Scripts

- **Archivos modificados**: `index-v03.html`, `CHANGELOG.md`
- Banco de Chile: el encabezado se resuelve por **nombre de columna** (índice de cada título), no por celdas contiguas; soporta cartolas `.xls` con **columnas vacías entre Fecha, Descripción, Canal, etc.** (formato típico exportado por el banco).

## [1.2.2] - 2026-03-26

### Fixed - Scripts

- **Archivos modificados**: `index-v03.html`, `CHANGELOG.md`
- Banco de Chile: detección del encabezado de la tabla en **cualquier fila** y **columna base** (p. ej. datos desde columna B); soporta cartola de **6 columnas** (Fecha, Descripción, Número documento, Cargos, Abonos, Saldo) y de **7 columnas** (con Canal/Sucursal y Nro. Docto.); normalización de texto para tildes; número de documento desde celda cuando existe; lectura auxiliar de saldo disponible en filas tipo resumen.

## [1.2.1] - 2026-03-26

### Fixed - Scripts

- **Archivos modificados**: `index-v03.html`, `CHANGELOG.md`
- Santander: el preview y el nombre de archivo usan siempre el banco **Santander** al elegir ese modo (ya no queda por defecto como BCI si el título del Excel no coincide).
- BCI: detección de la tabla de movimientos compatible con textos tipo “Movimientos de Cuenta Corriente”, fallback por fila encabezado con fecha/descripción/cargos y período leído aunque el texto “al” no esté en la misma celda que la etiqueta.
- Banco de Chile: se recorren **todas las hojas** del libro y se elige la que aporta más movimientos (útil cuando la hoja 1 es portada en `.xls`); encabezado alternativo si solo dice cargos/abonos sin la palabra exacta “cargo”.
- Itaú: **saldo final** tomado del último **saldo diario** numérico de la columna de saldo tras ordenar movimientos por fecha.
- Fechas numéricas tipo serial de Excel convertidas en `formatDate` para no descartar filas en cartolas que exportan fechas como número.

## [1.2.0] - 2026-03-26

### Added - Scripts

- **Archivos modificados**: `index-v03.html`, `CHANGELOG.md`
- Página `index-v03.html` que combina el flujo de salida estable (`buildXlsx`, `buildTxt`) con selector de banco y parsers por institución.
- Opción explícita Banco Santander con la misma lógica de lectura que `index.html` v1 (`Detalle movimientos`, `formatDate`/`parsePeriodo` equivalentes vía helpers dedicados).

### Changed - Scripts

- **Archivos modificados**: `index-v03.html`
- BCI y Banco Estado aceptan todos los archivos válidos seleccionados (sin tope de cuatro) y unifican movimientos en un solo output.
- Banco Estado prioriza la hoja con nombre exacto `Movimientos` y devuelve error claro si falta; si no existe, conserva búsqueda por nombre que contenga “movimiento”.

## [1.1.0] - 2026-03-24

### Added - Docs

- **Archivos modificados**: `CHANGELOG.md`
- Registro de versiones del proyecto en el formato definido

### Added - Scripts

- **Archivos modificados**: `index.html`
- Detección de banco, número de cartola (o cuenta) y periodo para armar el nombre de los archivos generados

### Changed - Styles

- **Archivos modificados**: `index.html`
- Tema claro en rosa y pastel con tipografía Rubik en toda la interfaz

### Changed - Scripts

- **Archivos modificados**: `index.html`
- Archivos .xlsx y .txt descargables renombrados al patrón `Banco XXX YYYYYY - MES AÑO` usando el mes en español
