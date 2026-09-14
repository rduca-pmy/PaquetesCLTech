# Esquema ComprobantesGeneral

## Resumen

- Tablas en `Publicacion.sql`: `9`
- Tablas con evidencia en SSIS: `8`
- Tablas sin evidencia en SSIS: `1`

## Lectura inicial

Esquema con buena cobertura, donde los jobs `Comprobantes_*` son la fuente principal de evidencia. Tambien aparecen toques complementarios desde paquetes de contribucion, personas y simulacion.

## Paquetes relevantes

- `Comprobantes_Entidad.dtsx`
- `Comprobantes_Facturacion.dtsx`
- `Comprobantes_Liquidaciones.dtsx`
- `Comprobantes_ManualPublicacion.dtsx`
- `Comprobantes_Retenciones.dtsx`

## Matriz inicial de tablas

| Tabla | Paquete o paquetes principales | Evidencia observada |
| --- | --- | --- |
| `ComprobantesGeneral.ComprobanteDetalleExterno` | `Contribucion_ComprobanteDetalleExterno.dtsx` | `OpenRowset`, `SELECT` |
| `ComprobantesGeneral.ComprobanteDetalleManualPublicacion` | `Comprobantes_ManualPublicacion.dtsx` | `OpenRowset`, `DELETE` |
| `ComprobantesGeneral.ComprobanteDetallePublicacion` | `Comprobantes_Facturacion.dtsx`, `Comprobantes_Liquidaciones.dtsx` | `OpenRowset`, `DELETE` |
| `ComprobantesGeneral.ComprobanteDetalleTarifaDevengada` | `Comprobantes_Facturacion.dtsx` | `OpenRowset`, `SELECT` |
| `ComprobantesGeneral.ComprobanteManualPublicacion` | `Comprobantes_ManualPublicacion.dtsx` | `OpenRowset`, `DELETE` |
| `ComprobantesGeneral.ComprobantePublicacion` | `Comprobantes_Facturacion.dtsx`, `Comprobantes_Liquidaciones.dtsx` | `OpenRowset`, `DELETE` |
| `ComprobantesGeneral.Entidad` | `Comprobantes_Entidad.dtsx`, `Contribucion_BonificacionDMA.dtsx`, `Personas_FondoComunInversion.dtsx`, `Personas_SociedadDepositaria.dtsx`, `Productos_InstrumentoDigital.dtsx`, `SimulacionContratoPublicacion.dtsx`, `SimulacionEscenarioPublicacion.dtsx` | `OpenRowset`, `SELECT` |
| `ComprobantesGeneral.RetencionPublicacion` | `Comprobantes_Retenciones.dtsx` | `OpenRowset`, `DELETE` |

## Tabla sin evidencia observada

- `ComprobantesGeneral.Presentacion`

## Nota

El esquema parece bastante orientado a publicacion documental y comprobantes consumidos por AP5.

## Artefactos de soporte

- [comprobantesgeneral-tablas-matriz.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/comprobantesgeneral-tablas-matriz.csv)
