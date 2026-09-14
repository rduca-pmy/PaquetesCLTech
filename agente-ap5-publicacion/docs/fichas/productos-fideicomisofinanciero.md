# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `FideicomisoFinanciero`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.FideicomisoFinanciero` se llena mediante `040_Productos.dtsx`. La evidencia visible es un `OpenRowset` directo al destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `040_Productos.dtsx` | carga principal | recurrente | paquete troncal del esquema |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga general de productos y subtipos
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Productos].[FideicomisoFinanciero]`
- Tablas relacionadas: `Productos.Titulo`, `Productos.Producto`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `040_Productos.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La tabla se carga desde el paquete maestro del dominio.
- No se detectaron otros jobs directos para este subtipo.

## Inferencias

- Se publica como subtipo de instrumento financiero para consumo en AP5.

## Dudas abiertas

- Si la fuente de negocio proviene de tablas dedicadas o de una clasificacion sobre `Titulo`.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita en paquete troncal.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar la consulta origen del subtipo.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `040_Productos.dtsx`
- Fecha de analisis: `2026-08-11`
