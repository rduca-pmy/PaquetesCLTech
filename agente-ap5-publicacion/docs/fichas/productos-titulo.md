# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `Titulo`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.Titulo` se llena mediante `040_Productos.dtsx`. La evidencia visible es un `OpenRowset` directo al destino dentro del paquete troncal del esquema.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `040_Productos.dtsx` | carga principal | recurrente | paquete maestro de productos |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga general de productos y subtipos
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Productos].[Titulo]`
- Tablas relacionadas: `Productos.ObligacionNegociable`, `Productos.FideicomisoFinanciero`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `040_Productos.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La tabla participa del lote general de instrumentos.
- No se detectaron paquetes alternativos en la matriz.

## Inferencias

- `Titulo` funciona como una base comun para varios subtipos financieros.

## Dudas abiertas

- Si la tabla es maestro principal o subtipo intermedio dentro del modelo.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita en paquete troncal.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar jerarquia relacional con `Producto` y `Contrato`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `040_Productos.dtsx`
- Fecha de analisis: `2026-08-11`
