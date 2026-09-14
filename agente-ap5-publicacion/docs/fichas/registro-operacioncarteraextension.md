# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `OperacionCarteraExtension`
- Esquema destino: `Registro`
- Clasificacion: `sincronizada`
- Dominio funcional: `Registro / Operaciones`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Registro.OperacionCarteraExtension` se llena mediante `Registro_OperacionCarteraExtension.dtsx`. La evidencia relevada muestra `UPDATE` y `OpenRowset` sobre la tabla destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Registro_OperacionCarteraExtension.dtsx` | carga principal | recurrente | paquete especifico de extension |

## Mecanismo tecnico

- Tipo de carga: `update + openrowset`
- Tarea o data flow: extension de operaciones de cartera
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `UPDATE [Registro].[OperacionCarteraExtension]`
- Tablas relacionadas: `Registro.OperacionCarteraMovimientoActivo`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| update | `Registro_OperacionCarteraExtension.dtsx` | comando SQL | aparece `UPDATE [Registro].[OperacionCarteraExtension]` |
| tabla destino | `Registro_OperacionCarteraExtension.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La tabla tiene un paquete dedicado.
- El mismo circuito tambien toca `OperacionCarteraMovimientoActivo`.

## Inferencias

- Expone atributos extendidos de operaciones que no entran en la tabla base publicada.

## Dudas abiertas

- Si la tabla es una extension uno a uno o una relacion mas granular.

## Clasificacion final

- Motivo de clasificacion: paquete especializado con evidencia explicita.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar claves y dependencias con la operacion principal.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Registro_OperacionCarteraExtension.dtsx`
- Fecha de analisis: `2026-08-11`
