# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `ContratoAFijarPublicacion`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos / A fijar`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.ContratoAFijarPublicacion` se llena mediante `Productos_ContratoAFijarPublicacion.dtsx`. La evidencia visible combina `UPDATE` y `OpenRowset`.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Productos_ContratoAFijarPublicacion.dtsx` | carga principal | recurrente | paquete especifico del circuito a fijar |

## Mecanismo tecnico

- Tipo de carga: `update + openrowset`
- Tarea o data flow: publicacion de contratos a fijar
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `UPDATE [Productos].[ContratoAFijarPublicacion]`
- Tablas relacionadas: `Registro.RelacionOperacionesAFijar`, `Productos.Contrato`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| update | `Productos_ContratoAFijarPublicacion.dtsx` | comando SQL | aparece `UPDATE [Productos].[ContratoAFijarPublicacion]` |
| tabla destino | `Productos_ContratoAFijarPublicacion.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- El paquete es exclusivo de esta entidad.
- El circuito se relaciona funcionalmente con operaciones a fijar del esquema `Registro`.

## Inferencias

- La tabla expone en AP5 contratos pendientes o configurados bajo modalidad a fijar.

## Dudas abiertas

- Si el `UPDATE` responde a cambios de estado o a enriquecimiento de atributos.

## Clasificacion final

- Motivo de clasificacion: paquete dedicado con destino explicito.
- Riesgo de error: bajo.
- Proxima validacion sugerida: cruzar con la tabla `RelacionOperacionesAFijar`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Productos_ContratoAFijarPublicacion.dtsx`
- Fecha de analisis: `2026-08-11`
