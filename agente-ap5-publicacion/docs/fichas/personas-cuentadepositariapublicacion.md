# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `CuentaDepositariaPublicacion`
- Esquema destino: `Personas`
- Clasificacion: `sincronizada`
- Dominio funcional: `Personas`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Personas.CuentaDepositariaPublicacion` se llena mediante el paquete `Personas_CuentaDepositariaPublicacion.dtsx`. La evidencia observada muestra un patron clasico de recarga y mantenimiento: `DELETE`, `OpenRowset` al destino e `UPDATE` sobre la misma tabla.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Personas_CuentaDepositariaPublicacion.dtsx` | carga principal de la tabla | recurrente | paquete activo en `Publicacion.dtproj` |

## Mecanismo tecnico

- Tipo de carga: `delete + insert/update`
- Tarea o data flow: `Delete`, `Inserts` y componentes de update
- Stored procedure: no observado en la evidencia principal
- SQL relevante: `DELETE [Personas].[CuentaDepositariaPublicacion]`, `UPDATE [Personas].[CuentaDepositariaPublicacion]`
- Tabla o tablas origen en Clearing: no confirmadas aun a nivel de objeto exacto

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| delete previo | `Personas_CuentaDepositariaPublicacion.dtsx` | `Delete` | aparece `DELETE [Personas].[CuentaDepositariaPublicacion]` |
| tabla destino | `Personas_CuentaDepositariaPublicacion.dtsx` | componente destino | `OpenRowset` apunta a `[Personas].[CuentaDepositariaPublicacion]` |
| update | `Personas_CuentaDepositariaPublicacion.dtsx` | comando SQL de destino | aparece `UPDATE [Personas].[CuentaDepositariaPublicacion]` |
| proyecto activo | `Publicacion.dtproj` | declaracion SSIS | el paquete figura como activo |

## Hechos observados

- El paquete usa conexiones `Clearing` y `Publicacion`.
- La tabla destino se nombra explicitamente varias veces en el `.dtsx`.
- La operacion no depende de un paquete generalista; tiene job propio.

## Inferencias

- La tabla probablemente concentra una proyeccion publicable de cuentas depositarias y no la entidad operativa original de PBP.

## Dudas abiertas

- Que objeto exacto de `Clearing` sirve de origen.
- Si la recarga es total o segmentada por subconjuntos.

## Clasificacion final

- Motivo de clasificacion: destino explicito con `DELETE`, `OpenRowset` y `UPDATE`.
- Riesgo de error: bajo.
- Proxima validacion sugerida: reconstruir la query origen en `Clearing`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Personas_CuentaDepositariaPublicacion.dtsx`
- Fecha de analisis: `2026-08-10`
