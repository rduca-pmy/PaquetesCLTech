# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `ConversionUnidadMedida`
- Esquema destino: `General`
- Clasificacion: `sincronizada`
- Dominio funcional: `General`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `General.ConversionUnidadMedida` se llena mediante `General_ConversionUnidadMedida.dtsx`, donde se observa un patron completo de `DELETE`, `INSERT & UPDATE`, `OpenRowset` y `UPDATE` sobre la misma tabla.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `General_ConversionUnidadMedida.dtsx` | carga principal | recurrente | paquete activo y especifico |

## Mecanismo tecnico

- Tipo de carga: `delete + insert/update`
- Tarea o data flow: `Delete`, `Insert & Update`
- Stored procedure: no observado en la evidencia principal
- SQL relevante: `DELETE FROM [General].[ConversionUnidadMedida]`, `UPDATE [General].[ConversionUnidadMedida]`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| delete previo | `General_ConversionUnidadMedida.dtsx` | `Delete` | aparece `DELETE FROM [General].[ConversionUnidadMedida]` |
| tabla destino | `General_ConversionUnidadMedida.dtsx` | componente destino | `OpenRowset` apunta a `[General].[ConversionUnidadMedida]` |
| update | `General_ConversionUnidadMedida.dtsx` | `Insert & Update` | aparece `UPDATE [General].[ConversionUnidadMedida]` |

## Hechos observados

- El paquete es activo en `dtproj`.
- La tabla tiene evidencia tecnica directa y fuerte.

## Inferencias

- Es una tabla de referencia transversal usada por varios dominios del modelo.

## Dudas abiertas

- Si la recarga es total diaria o eventual.

## Clasificacion final

- Motivo de clasificacion: destino explicito con patron completo de mantenimiento.
- Riesgo de error: bajo.
- Proxima validacion sugerida: identificar consumidores principales de la tabla.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `General_ConversionUnidadMedida.dtsx`
- Fecha de analisis: `2026-08-11`
