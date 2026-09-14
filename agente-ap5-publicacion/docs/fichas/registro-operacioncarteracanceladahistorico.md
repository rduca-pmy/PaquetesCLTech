# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `OperacionCarteraCanceladaHistorico`
- Esquema destino: `Registro`
- Clasificacion: `sincronizada`
- Dominio funcional: `Registro`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Registro.OperacionCarteraCanceladaHistorico` se llena mediante `010_OperacionCarteraCancelada.dtsx`, donde se observa un patron explicito de `DELETE`, `UPDATE` y `OpenRowset` sobre la misma tabla.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `010_OperacionCarteraCancelada.dtsx` | carga principal | recurrente | paquete activo y especifico |

## Mecanismo tecnico

- Tipo de carga: `delete + update + openrowset`
- Tarea o data flow: carga de operaciones canceladas historicas
- Stored procedure: no observado en la evidencia principal
- SQL relevante: `DELETE [Registro].[OperacionCarteraCanceladaHistorico]`, `UPDATE [Registro].[OperacionCarteraCanceladaHistorico]`
- Tabla relacionada: `Registro.OperacionCarteraCancelada`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| delete previo | `010_OperacionCarteraCancelada.dtsx` | comando SQL | aparece `DELETE [Registro].[OperacionCarteraCanceladaHistorico]` |
| update | `010_OperacionCarteraCancelada.dtsx` | comando SQL de destino | aparece `UPDATE [Registro].[OperacionCarteraCanceladaHistorico]` |
| tabla destino | `010_OperacionCarteraCancelada.dtsx` | componente destino | `OpenRowset` apunta a `[Registro].[OperacionCarteraCanceladaHistorico]` |

## Hechos observados

- El paquete toca tanto la tabla historica como la tabla actual.
- La tabla historica tiene evidencia tecnica fuerte y directa.

## Inferencias

- El job probablemente separa una vista corriente y una vista historica de cancelaciones de cartera.

## Dudas abiertas

- Que criterio de historizacion utiliza exactamente el paquete.

## Clasificacion final

- Motivo de clasificacion: destino explicito con patron completo de mantenimiento.
- Riesgo de error: bajo.
- Proxima validacion sugerida: comparar la tabla historica con `OperacionCarteraCancelada`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `010_OperacionCarteraCancelada.dtsx`
- Fecha de analisis: `2026-08-10`
