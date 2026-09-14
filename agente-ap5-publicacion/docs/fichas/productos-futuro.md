# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `Futuro`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.Futuro` se llena mediante `040_Productos.dtsx`. La evidencia observada combina `UPDATE` y `OpenRowset` sobre la tabla destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `040_Productos.dtsx` | carga principal | recurrente | paquete troncal del esquema |

## Mecanismo tecnico

- Tipo de carga: `update + openrowset`
- Tarea o data flow: carga general de productos y subtipos
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `UPDATE [Productos].[Futuro]`
- Tablas relacionadas: `Productos.Contrato`, `Productos.Subyacente`, `Productos.DisponibleDeFuturo`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| update | `040_Productos.dtsx` | comando SQL | aparece `UPDATE [Productos].[Futuro]` |
| tabla destino | `040_Productos.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La tabla se publica desde el paquete central del dominio.
- Comparte patron tecnico con otros subtipos financieros.

## Inferencias

- `Futuro` es un subtipo de contrato/instrumento publicado hacia AP5.

## Dudas abiertas

- Si hay enriquecimiento posterior desde otro circuito no visible en SSIS.

## Clasificacion final

- Motivo de clasificacion: destino explicito con update visible.
- Riesgo de error: bajo.
- Proxima validacion sugerida: cruzar con la definicion de `Contrato`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `040_Productos.dtsx`
- Fecha de analisis: `2026-08-11`
