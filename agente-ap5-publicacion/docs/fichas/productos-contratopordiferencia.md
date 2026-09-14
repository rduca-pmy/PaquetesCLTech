# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `ContratoPorDiferencia`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.ContratoPorDiferencia` se llena mediante `040_Productos.dtsx`. La evidencia encontrada muestra `UPDATE` y `OpenRowset` sobre el destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `040_Productos.dtsx` | carga principal | recurrente | paquete troncal del esquema |

## Mecanismo tecnico

- Tipo de carga: `update + openrowset`
- Tarea o data flow: carga general de subtipos de producto
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `UPDATE [Productos].[ContratoPorDiferencia]`
- Tablas relacionadas: `Productos.Contrato`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| update | `040_Productos.dtsx` | comando SQL | aparece `UPDATE [Productos].[ContratoPorDiferencia]` |
| tabla destino | `040_Productos.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La tabla se publica desde el paquete maestro.
- Sigue el patron de otros subtipos de instrumentos complejos.

## Inferencias

- Puede representar contratos financieros con logica de diferencias o liquidacion particular.

## Dudas abiertas

- Si su origen en `Clearing` reside en tablas dedicadas o en clasificacion por tipo de contrato.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita con update visible.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar query origen del subtipo.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `040_Productos.dtsx`
- Fecha de analisis: `2026-08-11`
