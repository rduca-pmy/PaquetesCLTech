# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `GrupoProductoCancelacionProducto`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos / Operaciones`
- Nivel de confianza: `media`

## Respuesta corta

La tabla `Productos.GrupoProductoCancelacionProducto` muestra evidencia en `Operaciones_CancelacionManual.dtsx`. La evidencia combina `DELETE`, `UPDATE` y `OpenRowset`, aunque el paquete pertenece a otro dominio funcional.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Operaciones_CancelacionManual.dtsx` | carga principal observada | recurrente | paquete de operaciones que tambien actualiza tablas de productos |

## Mecanismo tecnico

- Tipo de carga: `delete + update + openrowset`
- Tarea o data flow: cancelacion manual / relacion de grupos y productos
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `DELETE [Productos].[GrupoProductoCancelacionProducto]`, `UPDATE [Productos].[GrupoProductoCancelacionProducto]`
- Tablas relacionadas: `Activos.FuenteCotizacionActivo`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| delete previo | `Operaciones_CancelacionManual.dtsx` | comando SQL | aparece `DELETE [Productos].[GrupoProductoCancelacionProducto]` |
| update | `Operaciones_CancelacionManual.dtsx` | comando SQL | aparece `UPDATE [Productos].[GrupoProductoCancelacionProducto]` |
| tabla destino | `Operaciones_CancelacionManual.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La tabla no se asocia al paquete troncal de productos.
- El job pertenece a un circuito operativo especifico.

## Inferencias

- La relacion grupo-producto se usa como apoyo para cancelaciones manuales u otras acciones operativas.

## Dudas abiertas

- Si existe una carga base previa y este paquete solo ajusta el contenido.

## Clasificacion final

- Motivo de clasificacion: destino explicito, aunque desde un paquete de otro dominio.
- Riesgo de error: medio.
- Proxima validacion sugerida: inspeccionar si la tabla aparece tambien en otro job maestro no relevado aun.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Operaciones_CancelacionManual.dtsx`
- Fecha de analisis: `2026-08-11`
