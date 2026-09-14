# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `LiquidacionPublicacion`
- Esquema destino: `Registro`
- Clasificacion: `sincronizada`
- Dominio funcional: `Registro`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Registro.LiquidacionPublicacion` se llena desde `Registro_LiquidacionPublicacion.dtsx`, donde se observa un patron de `DELETE` previo y `OpenRowset` explicito hacia la tabla destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Registro_LiquidacionPublicacion.dtsx` | carga principal | recurrente | paquete activo y especifico |

## Mecanismo tecnico

- Tipo de carga: `delete + openrowset`
- Tarea o data flow: carga de liquidacion
- Stored procedure: no observado en la evidencia principal
- SQL relevante: `DELETE [Registro].[LiquidacionPublicacion]`
- Objeto relacionado: `vOperacionesProvisionalesYFinalesFCI` aparece como apoyo del paquete

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| delete previo | `Registro_LiquidacionPublicacion.dtsx` | comando SQL | aparece `DELETE [Registro].[LiquidacionPublicacion]` |
| tabla destino | `Registro_LiquidacionPublicacion.dtsx` | componente destino | `OpenRowset` apunta a `[Registro].[LiquidacionPublicacion]` |

## Hechos observados

- La tabla aparece como destino explicito.
- El paquete parece operar de manera focalizada sobre esta entidad.

## Inferencias

- Es una tabla de publicacion orientada a exponer liquidaciones ya procesadas.

## Dudas abiertas

- Si la vista auxiliar `vOperacionesProvisionalesYFinalesFCI` es parte critica del armado final.

## Clasificacion final

- Motivo de clasificacion: destino explicito con borrado previo en paquete especifico.
- Riesgo de error: bajo.
- Proxima validacion sugerida: reconstruir la consulta origen completa.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Registro_LiquidacionPublicacion.dtsx`
- Fecha de analisis: `2026-08-10`
