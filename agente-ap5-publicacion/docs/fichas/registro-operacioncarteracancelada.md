# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `OperacionCarteraCancelada`
- Esquema destino: `Registro`
- Clasificacion: `sincronizada`
- Dominio funcional: `Registro / Operaciones`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Registro.OperacionCarteraCancelada` se llena mediante `010_OperacionCarteraCancelada.dtsx`. La evidencia observada es un `OpenRowset` directo al destino dentro del mismo job que tambien maneja el historico.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `010_OperacionCarteraCancelada.dtsx` | carga principal | recurrente | paquete especifico de cancelaciones |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: publicacion de operaciones canceladas
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Registro].[OperacionCarteraCancelada]`
- Tablas relacionadas: `Registro.OperacionCarteraCanceladaHistorico`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `010_OperacionCarteraCancelada.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- El paquete separa tabla vigente y tabla historica.
- La evidencia de destino es explicita.

## Inferencias

- AP5 mantiene una vista publicada de operaciones canceladas de uso operativo.

## Dudas abiertas

- Como se define el pasaje entre la tabla vigente y la historica.

## Clasificacion final

- Motivo de clasificacion: paquete dedicado con destino explicito.
- Riesgo de error: bajo.
- Proxima validacion sugerida: comparar la logica de carga de ambas tablas canceladas.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `010_OperacionCarteraCancelada.dtsx`
- Fecha de analisis: `2026-08-11`
