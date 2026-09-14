# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `ConversionContrato`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos / Conversiones`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.ConversionContrato` se llena mediante `090_ConversionContrato.dtsx`. La evidencia combina `UPDATE` y `OpenRowset`, lo que indica insercion y mantenimiento de la conversion publicada.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `090_ConversionContrato.dtsx` | carga principal | recurrente | paquete especifico de conversiones |

## Mecanismo tecnico

- Tipo de carga: `update + openrowset`
- Tarea o data flow: carga de conversiones de contrato
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `UPDATE [Productos].[ConversionContrato]`
- Tablas relacionadas: `Productos.Contrato`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| update | `090_ConversionContrato.dtsx` | comando SQL | aparece `UPDATE [Productos].[ConversionContrato]` |
| tabla destino | `090_ConversionContrato.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La tabla tiene un paquete exclusivo.
- El nombre del job y la tabla coinciden funcionalmente.

## Inferencias

- Materializa relaciones de conversion o equivalencia entre contratos publicados.

## Dudas abiertas

- Si representa conversion de unidades, especies o transformaciones de negocio.

## Clasificacion final

- Motivo de clasificacion: paquete dedicado con evidencia explicita.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar columnas origen/destino y tipo de conversion.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `090_ConversionContrato.dtsx`
- Fecha de analisis: `2026-08-11`
