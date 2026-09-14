# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `InstrumentoDigital`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.InstrumentoDigital` se llena mediante `Productos_InstrumentoDigital.dtsx`. La evidencia observada combina `UPDATE` y `OpenRowset`.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Productos_InstrumentoDigital.dtsx` | carga principal | recurrente | paquete especializado del subtipo |

## Mecanismo tecnico

- Tipo de carga: `update + openrowset`
- Tarea o data flow: carga de instrumentos digitales
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `UPDATE [Productos].[InstrumentoDigital]`
- Tablas relacionadas: `Productos.Producto`, `Productos.Contrato`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| update | `Productos_InstrumentoDigital.dtsx` | comando SQL | aparece `UPDATE [Productos].[InstrumentoDigital]` |
| tabla destino | `Productos_InstrumentoDigital.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La tabla tiene un job dedicado.
- El patron tecnico replica otros paquetes especificos del esquema.

## Inferencias

- AP5 publica un subtipo de producto o contrato asociado a instrumentos digitales.

## Dudas abiertas

- Si este concepto refiere a firma/documentacion digital o a un producto financiero digital nativo.

## Clasificacion final

- Motivo de clasificacion: paquete especializado con evidencia explicita.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar la definicion de tabla en `Publicacion.sql`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Productos_InstrumentoDigital.dtsx`
- Fecha de analisis: `2026-08-11`
