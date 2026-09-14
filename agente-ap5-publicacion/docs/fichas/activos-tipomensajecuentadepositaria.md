# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `TipoMensajeCuentaDepositaria`
- Esquema destino: `Activos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Activos / Mensajeria operativa`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Activos.TipoMensajeCuentaDepositaria` se llena mediante `Activos_TipoMensajeCuentaDepositaria.dtsx`. La evidencia combina `DELETE` y `OpenRowset`, por lo que el paquete parece regenerar la publicacion del catalogo o relacion.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Activos_TipoMensajeCuentaDepositaria.dtsx` | carga principal | recurrente | paquete especifico del cruce tipo de mensaje/cuenta |

## Mecanismo tecnico

- Tipo de carga: `delete + openrowset`
- Tarea o data flow: carga de tipos de mensaje por cuenta depositaria
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `DELETE [Activos].[TipoMensajeCuentaDepositaria]`
- Tablas relacionadas: `Personas.CuentaDepositariaPublicacion`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| delete previo | `Activos_TipoMensajeCuentaDepositaria.dtsx` | comando SQL | aparece `DELETE [Activos].[TipoMensajeCuentaDepositaria]` |
| tabla destino | `Activos_TipoMensajeCuentaDepositaria.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La tabla tiene paquete exclusivo.
- El patron tecnico sugiere recarga total del contenido publicado.

## Inferencias

- Puede tratarse de una parametrizacion publicada para enrutamiento o visualizacion de mensajes por cuenta.

## Dudas abiertas

- Si la fuente real nace en tablas maestras de mensajeria o en reglas de negocio derivadas.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita con borrado previo.
- Riesgo de error: bajo.
- Proxima validacion sugerida: identificar si el borrado es total o segmentado.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Activos_TipoMensajeCuentaDepositaria.dtsx`
- Fecha de analisis: `2026-08-11`
