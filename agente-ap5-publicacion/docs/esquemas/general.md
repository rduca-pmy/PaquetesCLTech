# Esquema General

## Resumen

- Tablas en `Publicacion.sql`: `19`
- Tablas con evidencia en SSIS: `19`
- Tablas sin evidencia en SSIS: `0`

## Lectura inicial

Esquema con cobertura total en los paquetes relevados. Aparece como base transversal del modelo, con tablas de apoyo usadas por muchos dominios.

## Paquetes relevantes

- `020_General.dtsx`
- `020_LiquidacionValores.dtsx`
- `General_ConversionUnidadMedida.dtsx`
- `ProcesoPublicacion.dtsx`
- tambien aparece en `030_PersonasGeneral*`, `700_ActivosPublicacion.dtsx`, `950_PortfolioDeActivos.dtsx` y otros

## Matriz inicial de tablas

| Tabla | Paquete o paquetes principales | Evidencia observada |
| --- | --- | --- |
| `General.Aprobacion` | `020_General.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `General.CodigoPostal` | `020_General.dtsx` | `OpenRowset`, `SELECT` |
| `General.ConversionUnidadMedida` | `General_ConversionUnidadMedida.dtsx` | `OpenRowset`, `DELETE`, `UPDATE`, `SELECT` |
| `General.CotizacionMoneda` | `020_General.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `General.CotizacionTasa` | `020_General.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `General.Estado` | `020_General.dtsx` | `OpenRowset`, `UPDATE` |
| `General.EstadoAprobacion` | `010_OperacionCarteraCancelada.dtsx`, `020_General.dtsx`, `020_LiquidacionValores.dtsx`, `090_ConversionContrato.dtsx`, `200_ActivoFinalidad.dtsx`, `600_MargenesContratos.dtsx`, `700_ActivosPublicacion.dtsx`, `Activos_GrupoOperacionCartera.dtsx`, `Compensacion_DerivacionDRP.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `General.Feriado` | `020_General.dtsx`, `PersonasEntrega.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `General.FeriadoMercado` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralLight.dtsx`, `030_PersonasGeneralViejo.dtsx`, `PersonasEntrega.dtsx` | `OpenRowset`, `SELECT` |
| `General.Fuente` | `020_General.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `General.Localidad` | `020_General.dtsx` | `OpenRowset`, `SELECT` |
| `General.Moneda` | `020_General.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `General.MonedaCotizable` | `020_General.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `General.MotivoRechazo` | `020_General.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `General.Proceso` | `020_General.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `General.ProcesoParametro` | `020_General.dtsx`, `ProcesoPublicacion.dtsx` | `OpenRowset`, `SELECT` |
| `General.ProcesoPublicacion` | `ProcesoPublicacion.dtsx` | `OpenRowset`, `DELETE` |
| `General.Tasa` | `020_General.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `General.UnidadMedida` | `020_General.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |

## Nota

`General` parece ser uno de los esquemas estructurales de AP5 y tiene muy buena trazabilidad desde SSIS.

## Artefactos de soporte

- [general-tablas-matriz.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/general-tablas-matriz.csv)
