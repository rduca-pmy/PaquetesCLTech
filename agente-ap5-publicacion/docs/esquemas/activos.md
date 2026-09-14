# Esquema Activos

## Resumen

- Tablas en `Publicacion.sql`: `20`
- Tablas con evidencia en SSIS: `17`
- Tablas sin evidencia en SSIS: `3`

## Lectura inicial

Es un esquema con cobertura alta desde `IntegrationServices/Publicacion`. Se apoya en paquetes propios del dominio `Activos_*`, en paquetes numerados como `200_*`, `201_*`, `202_*`, `203_*`, y tambien en jobs de movimiento y portfolio.

## Paquetes relevantes

- Activos en `dtproj`: `200_ActivoFinalidad.dtsx`, `201_ActivoCuentaDepositaria.dtsx`, `202_FondoFinalidad.dtsx`, `203_FondoCuentaDepositaria.dtsx`, `510_MovimientoPublicacion.dtsx`, `700_ActivosPublicacion.dtsx`, `920_Activos.dtsx`, `950_PortfolioDeActivos.dtsx`, `Activos_ActivoCertificadoDepositoWarrantPublicacion.dtsx`, `Activos_ActivoPublicacionMoneda.dtsx`, `Activos_AvalPublicacion.dtsx`, `Activos_GrupoOperacionCartera.dtsx`, `Activos_TipoMensajeCuentaDepositaria.dtsx`
- Fuera de `dtproj`: `510_MovimientoPublicacion_7Dias.dtsx`, `510_MovimientoPublicacionHistorico.dtsx`, `800_GarantiasOpcionesMerval.dtsx`, `Activos_MovimientoCustodiaNoProcesadoPublicacion.dtsx`, `MovimientoPublicacionUpdateTesting.dtsx`

## Matriz inicial de tablas

| Tabla | Paquete o paquetes principales | Evidencia observada |
| --- | --- | --- |
| `Activos.PortfolioDetalle` | `950_PortfolioDeActivos.dtsx` | `OpenRowset` |
| `Activos.MovimientoPublicacion` | `510_MovimientoPublicacion.dtsx` y variantes | `OpenRowset` |
| `Activos.ActivoPublicacion` | `700_ActivosPublicacion.dtsx` | `OpenRowset` |
| `Activos.ActivoCertificadoDepositoWarrantPublicacion` | `Activos_ActivoCertificadoDepositoWarrantPublicacion.dtsx` | `DELETE`, `UPDATE`, `OpenRowset` |
| `Activos.OperacionCarteraGrupoOperacionCarteraPublicacion` | `Activos_GrupoOperacionCartera.dtsx` | `OpenRowset` |
| `Activos.ActivoPublicacionFinalidad` | `200_ActivoFinalidad.dtsx` | `UPDATE`, `OpenRowset` |
| `Activos.MovimientoPublicacionExtension` | `510_MovimientoPublicacion.dtsx` | `OpenRowset` |
| `Activos.FondoFinalidad` | `202_FondoFinalidad.dtsx` | `UPDATE`, `OpenRowset` |
| `Activos.Activo` | `920_Activos.dtsx` y paquetes consumidores | `DELETE`, `UPDATE`, `OpenRowset` |
| `Activos.FuenteCotizacionActivo` | `920_Activos.dtsx`, `Operaciones_CancelacionManual.dtsx` | `OpenRowset` |
| `Activos.ActivoPublicacionCuentaDepositaria` | `201_ActivoCuentaDepositaria.dtsx` | `OpenRowset` |
| `Activos.FondoCuentaDepositaria` | `203_FondoCuentaDepositaria.dtsx` | `OpenRowset` |
| `Activos.AvalPublicacion` | `Activos_AvalPublicacion.dtsx` | `OpenRowset` |
| `Activos.TipoMensajeCuentaDepositaria` | `Activos_TipoMensajeCuentaDepositaria.dtsx` | `DELETE`, `OpenRowset` |
| `Activos.GarantiasOpcionesMerval` | `800_GarantiasOpcionesMerval.dtsx` | `DELETE`, `OpenRowset` |
| `Activos.ActivoPublicacionMoneda` | `Activos_ActivoPublicacionMoneda.dtsx` | `OpenRowset` |
| `Activos.MovimientoCustodiaNoProcesadoPublicacion` | `Activos_MovimientoCustodiaNoProcesadoPublicacion.dtsx` | `OpenRowset` |

## Tablas sin evidencia observada

- `Activos.EventoCorporativoPublicacion`
- `Activos.SaldosWidgets`
- `Activos.MovimientoPublicacion_Particionada`

## Nota

`Activos` es un buen candidato para profundizacion posterior porque la relacion entre paquetes y tablas parece bastante visible desde los nombres.

## Artefactos de soporte

- [activos-tablas-matriz.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/activos-tablas-matriz.csv)
- [activos-paquete-tabla-matriz.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/activos-paquete-tabla-matriz.csv)
