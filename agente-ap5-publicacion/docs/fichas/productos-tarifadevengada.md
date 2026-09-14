# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `TarifaDevengada`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos / Tarifas`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.TarifaDevengada` se llena mediante `Productos_TarifaDevengada.dtsx`. La evidencia observada es un `OpenRowset` directo al destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Productos_TarifaDevengada.dtsx` | carga principal | recurrente | paquete especifico de tarifas devengadas |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga de tarifas devengadas
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Productos].[TarifaDevengada]`
- Tablas relacionadas: `Productos.TarifaDevengadaStage`, `Productos.TarifaPublicacion`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `Productos_TarifaDevengada.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- El paquete dedicado tambien toca `TarifaDevengadaStage`.
- La tabla parece ser el destino publicado principal del circuito.

## Inferencias

- La carga puede incluir una etapa intermedia previa antes de materializar la tabla final.

## Dudas abiertas

- Si `Stage` se usa para deduplicacion, validacion o merge previo.

## Clasificacion final

- Motivo de clasificacion: paquete especializado con destino explicito.
- Riesgo de error: bajo.
- Proxima validacion sugerida: reconstruir el rol exacto de `TarifaDevengadaStage`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Productos_TarifaDevengada.dtsx`
- Fecha de analisis: `2026-08-11`
