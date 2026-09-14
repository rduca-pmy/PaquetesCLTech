# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `FondoCuentaDepositaria`
- Esquema destino: `Activos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Activos / Fondos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Activos.FondoCuentaDepositaria` se llena mediante `203_FondoCuentaDepositaria.dtsx`. La evidencia observada es un `OpenRowset` directo a la tabla destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `203_FondoCuentaDepositaria.dtsx` | carga principal | recurrente | paquete especifico de relacion fondo/cuenta depositaria |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga de cuentas depositarias por fondo
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Activos].[FondoCuentaDepositaria]`
- Tablas relacionadas: `Activos.FondoFinalidad`, `Personas.CuentaDepositariaPublicacion`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `203_FondoCuentaDepositaria.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- El paquete es especifico y autosuficiente para identificar la relacion.
- No se observaron otros paquetes tocando la misma tabla en la matriz.

## Inferencias

- La tabla publica la habilitacion o asociacion de fondos con cuentas depositarias visibles en AP5.

## Dudas abiertas

- Si la nocion de fondo coincide con el mismo universo que usa `Productos.FondoComunInversion`.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita en paquete dedicado.
- Riesgo de error: bajo.
- Proxima validacion sugerida: contrastar columnas con `Clearing.sql`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `203_FondoCuentaDepositaria.dtsx`
- Fecha de analisis: `2026-08-11`
