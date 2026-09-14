# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `DatosPatrimoniales`
- Esquema destino: `Personas`
- Clasificacion: `sincronizada`
- Dominio funcional: `Personas`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Personas.DatosPatrimoniales` se llena mediante `Personas_DatosPatrimoniales.dtsx`, paquete activo del proyecto que muestra un patron de `DELETE`, `OpenRowset` al destino e `UPDATE` posterior sobre la misma tabla.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Personas_DatosPatrimoniales.dtsx` | carga principal de la tabla | recurrente | paquete especifico y activo |

## Mecanismo tecnico

- Tipo de carga: `delete + insert/update`
- Tarea o data flow: secuencia de borrado, insercion y update
- Stored procedure: no observado en la evidencia principal
- SQL relevante: `DELETE [Personas].[DatosPatrimoniales]`, `UPDATE [Personas].[DatosPatrimoniales]`
- Tabla o tablas origen en Clearing: no confirmadas aun a nivel de objeto exacto

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| delete previo | `Personas_DatosPatrimoniales.dtsx` | comando SQL | aparece `DELETE [Personas].[DatosPatrimoniales]` |
| tabla destino | `Personas_DatosPatrimoniales.dtsx` | componente destino | `OpenRowset` apunta a `[Personas].[DatosPatrimoniales]` |
| update | `Personas_DatosPatrimoniales.dtsx` | comando SQL de destino | aparece `UPDATE [Personas].[DatosPatrimoniales]` |

## Hechos observados

- La tabla destino aparece repetidamente en el paquete.
- Se observa lectura previa sobre la misma tabla para comparacion o lookup.
- El paquete es especifico de la entidad y no depende del generalista.

## Inferencias

- Esta tabla probablemente requiera mantenimiento por vigencia o versionado logico, dado que la evidencia menciona `EsVigente`.

## Dudas abiertas

- Que conjunto exacto de datos patrimoniales se replica desde `Clearing`.
- Si existe logica temporal adicional fuera del `.dtsx`.

## Clasificacion final

- Motivo de clasificacion: destino explicito con `DELETE`, `OpenRowset` y `UPDATE`.
- Riesgo de error: bajo.
- Proxima validacion sugerida: reconstruir el origen y la semantica de `EsVigente`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Personas_DatosPatrimoniales.dtsx`
- Fecha de analisis: `2026-08-10`
