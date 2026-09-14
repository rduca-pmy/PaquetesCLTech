# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `RelacionOperacionesAFijar`
- Esquema destino: `Registro`
- Clasificacion: `sincronizada`
- Dominio funcional: `Registro / A fijar`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Registro.RelacionOperacionesAFijar` se llena mediante `Registro_RelacionOperacionesAFijar.dtsx`. La evidencia combina `DELETE`, `UPDATE` y `OpenRowset`, lo que muestra un mantenimiento completo de la relacion publicada.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Registro_RelacionOperacionesAFijar.dtsx` | carga principal | recurrente | paquete especifico del circuito |

## Mecanismo tecnico

- Tipo de carga: `delete + update + openrowset`
- Tarea o data flow: carga de relaciones entre operaciones a fijar
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `DELETE [Registro].[RelacionOperacionesAFijar]`, `UPDATE [Registro].[RelacionOperacionesAFijar]`
- Tablas relacionadas: `Productos.ContratoAFijarPublicacion`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| delete previo | `Registro_RelacionOperacionesAFijar.dtsx` | comando SQL | aparece `DELETE [Registro].[RelacionOperacionesAFijar]` |
| update | `Registro_RelacionOperacionesAFijar.dtsx` | comando SQL | aparece `UPDATE [Registro].[RelacionOperacionesAFijar]` |
| tabla destino | `Registro_RelacionOperacionesAFijar.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- El paquete es especifico del circuito a fijar.
- Existe una relacion funcional clara con la publicacion de contratos a fijar.

## Inferencias

- La tabla vincula operaciones entre si o con contratos publicados bajo modalidad a fijar.

## Dudas abiertas

- Si se trata de relaciones activas solamente o tambien canceladas/cerradas.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita con mantenimiento completo.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar el criterio de borrado y de actualizacion.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Registro_RelacionOperacionesAFijar.dtsx`
- Fecha de analisis: `2026-08-11`
