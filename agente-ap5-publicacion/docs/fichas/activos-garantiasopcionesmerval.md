# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `GarantiasOpcionesMerval`
- Esquema destino: `Activos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Activos / Garantias`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Activos.GarantiasOpcionesMerval` se llena mediante `800_GarantiasOpcionesMerval.dtsx`, un paquete hoy fuera de `dtproj`. La evidencia observada muestra `DELETE` y `OpenRowset` directos sobre la tabla.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `800_GarantiasOpcionesMerval.dtsx` | carga principal | recurrente | paquete fuera de `dtproj`, pero con evidencia directa |

## Mecanismo tecnico

- Tipo de carga: `delete + openrowset`
- Tarea o data flow: carga de garantias de opciones
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `DELETE [Activos].[GarantiasOpcionesMerval]`
- Tablas relacionadas: `Activos.Activo`, `Productos.Opcion`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| delete previo | `800_GarantiasOpcionesMerval.dtsx` | comando SQL | aparece `DELETE [Activos].[GarantiasOpcionesMerval]` |
| tabla destino | `800_GarantiasOpcionesMerval.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- El archivo existe fuera del proyecto SSIS declarado.
- Aun asi, la tabla destino aparece de forma explicita.

## Inferencias

- Puede ser un paquete historico, auxiliar o desplegado por fuera del `dtproj` actual, pero util para responder como se llena la tabla.

## Dudas abiertas

- Si sigue activo en produccion o si fue reemplazado por otro mecanismo.

## Clasificacion final

- Motivo de clasificacion: destino explicito, con la salvedad de estar fuera de `dtproj`.
- Riesgo de error: bajo en la relacion tecnica, medio en la vigencia operativa.
- Proxima validacion sugerida: confirmar vigencia del paquete fuera de proyecto.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `800_GarantiasOpcionesMerval.dtsx`
- Fecha de analisis: `2026-08-11`
