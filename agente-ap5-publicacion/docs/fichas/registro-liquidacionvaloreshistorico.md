# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `LiquidacionValoresHistorico`
- Esquema destino: `Registro`
- Clasificacion: `sincronizada`
- Dominio funcional: `Registro / Liquidaciones`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Registro.LiquidacionValoresHistorico` se llena mediante `020_LiquidacionValores.dtsx`. La evidencia combina `DELETE`, `UPDATE` y `OpenRowset`, mostrando una carga con mantenimiento completo.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `020_LiquidacionValores.dtsx` | carga principal | recurrente | paquete especifico de liquidacion de valores |

## Mecanismo tecnico

- Tipo de carga: `delete + update + openrowset`
- Tarea o data flow: publicacion historica de liquidaciones de valores
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `DELETE [Registro].[LiquidacionValoresHistorico]`, `UPDATE [Registro].[LiquidacionValoresHistorico]`
- Tablas relacionadas: `Registro.LiquidacionPublicacion`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| delete previo | `020_LiquidacionValores.dtsx` | comando SQL | aparece `DELETE [Registro].[LiquidacionValoresHistorico]` |
| update | `020_LiquidacionValores.dtsx` | comando SQL | aparece `UPDATE [Registro].[LiquidacionValoresHistorico]` |
| tabla destino | `020_LiquidacionValores.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La tabla es historica y tiene un paquete exclusivo.
- El patron tecnico es el mas completo del conjunto.

## Inferencias

- AP5 conserva historico de liquidaciones por fuera de la tabla publicada vigente.

## Dudas abiertas

- Como se articula funcionalmente con `LiquidacionPublicacion`.

## Clasificacion final

- Motivo de clasificacion: paquete dedicado con evidencia completa.
- Riesgo de error: bajo.
- Proxima validacion sugerida: comparar claves y criterios temporales entre ambas tablas de liquidacion.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `020_LiquidacionValores.dtsx`
- Fecha de analisis: `2026-08-11`
