# Esquema Parametros

## Resumen

- Tablas en `Publicacion.sql`: `32`
- Tablas con evidencia en SSIS: `16`
- Tablas sin evidencia en SSIS: `16`

## Lectura inicial

La cobertura es intermedia. Hay un conjunto claro de tablas abastecidas por `015_Parametros.dtsx`, `010_Sistema.dtsx` y paquetes de notificaciones, pero muchas otras no aparecen en los jobs relevados.

## Paquetes relevantes

- `010_Sistema.dtsx`
- `015_Parametros.dtsx`
- `Parametros_Notificacion.dtsx`
- `Parametros_NotificacionAdministracion.dtsx`

## Matriz inicial de tablas

| Tabla | Paquete o paquetes principales | Evidencia observada |
| --- | --- | --- |
| `Parametros.ClasificacionArchivo` | `015_Parametros.dtsx` | `OpenRowset`, `UPDATE` |
| `Parametros.ClasificacionCuentaDepositaria` | `015_Parametros.dtsx` | `OpenRowset`, `UPDATE` |
| `Parametros.Concepto` | `015_Parametros.dtsx` | `OpenRowset`, `UPDATE` |
| `Parametros.Ejecucion` | `015_Parametros.dtsx` | `OpenRowset`, `UPDATE` |
| `Parametros.Finalidad` | `010_Sistema.dtsx`, `015_Parametros.dtsx` | `OpenRowset`, `UPDATE` |
| `Parametros.Notificacion` | `Parametros_Notificacion.dtsx`, `Parametros_NotificacionAdministracion.dtsx` | `OpenRowset`, `SELECT` |
| `Parametros.NotificacionContenido` | `Parametros_Notificacion.dtsx`, `Parametros_NotificacionAdministracion.dtsx` | `OpenRowset`, `SELECT` |
| `Parametros.NotificacionDestinatario` | `Parametros_Notificacion.dtsx`, `Parametros_NotificacionAdministracion.dtsx` | `OpenRowset`, `SELECT` |
| `Parametros.NotificacionPlantilla` | `Parametros_NotificacionAdministracion.dtsx` | `OpenRowset`, `SELECT` |
| `Parametros.TipoCuentaCompensacion` | `015_Parametros.dtsx` | `OpenRowset`, `UPDATE` |
| `Parametros.TipoMensaje` | `015_Parametros.dtsx` | `OpenRowset`, `UPDATE` |
| `Parametros.TipoNotificacion` | `Parametros_Notificacion.dtsx`, `Parametros_NotificacionAdministracion.dtsx` | `OpenRowset`, `SELECT` |
| `Parametros.TipoNotificacionContenido` | `Parametros_Notificacion.dtsx`, `Parametros_NotificacionAdministracion.dtsx` | `OpenRowset`, `SELECT` |
| `Parametros.TipoPersona` | `015_Parametros.dtsx` | `OpenRowset`, `UPDATE` |
| `Parametros.TipoProceso` | `015_Parametros.dtsx` | `OpenRowset`, `UPDATE` |
| `Parametros.TipoRueda` | `015_Parametros.dtsx` | `OpenRowset`, `UPDATE` |

## Tablas sin evidencia observada

- `Parametros.TipoOrdenFCI`
- `Parametros.TipoRepo`
- `Parametros.TipoCuentaAdministrativa`
- `Parametros.TipoMovimientoInstruccionGarantia`
- `Parametros.TipoEmision`
- `Parametros.HorariosRueda`
- `Parametros.ProcedenciaMensaje`
- `Parametros.ClasificacionMovimientoActivo`
- `Parametros.MensajeOrigen`
- `Parametros.MonedaWarrant`
- `Parametros.NotificacionCanalesComunicacion`
- `Parametros.OrdenOrigen`
- `Parametros.Rol`
- `Parametros.TipoCuentaRegistro`
- `Parametros.TipoEventoCorporativo`
- `Parametros.TipoPrimaDescuento`

## Nota

Conviene tomar este esquema en una fase propia si despues queremos diferenciar parametros "catalogo" de parametros funcionales vivos.

## Artefactos de soporte

- [parametros-tablas-matriz.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/parametros-tablas-matriz.csv)
