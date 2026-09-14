# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `ActivoPublicacionCuentaDepositaria`
- Esquema destino: `Activos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Activos / Cuentas depositarias`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Activos.ActivoPublicacionCuentaDepositaria` se llena mediante `201_ActivoCuentaDepositaria.dtsx`. La evidencia visible es un `OpenRowset` directo al destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `201_ActivoCuentaDepositaria.dtsx` | carga principal | recurrente | paquete especifico del cruce activo/cuenta depositaria |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga de cuentas depositarias por activo
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Activos].[ActivoPublicacionCuentaDepositaria]`
- Tablas relacionadas: `Personas.CuentaDepositariaPublicacion`, `Activos.ActivoPublicacion`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `201_ActivoCuentaDepositaria.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- El nombre del paquete coincide con la funcion de la tabla.
- La carga es directa y sin evidencia de pasos intermedios visibles.

## Inferencias

- Se publica la disponibilidad o habilitacion de un activo por cuenta depositaria.

## Dudas abiertas

- Si el cruce incluye restricciones comerciales o solo habilitaciones tecnicas.

## Clasificacion final

- Motivo de clasificacion: paquete dedicado con destino explicito.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar claves y columnas de cruce en `Publicacion.sql`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `201_ActivoCuentaDepositaria.dtsx`
- Fecha de analisis: `2026-08-11`
