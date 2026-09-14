# Esquema Registro

## Resumen

- Tablas en `Publicacion.sql`: `29`
- Tablas con evidencia en SSIS: `15`
- Tablas sin evidencia en SSIS: `14`

## Lectura inicial

La cobertura es intermedia. Hay paquetes claramente centrados en registro, pero varias tablas del esquema no muestran evidencia directa desde `Publicacion`.

## Paquetes relevantes

- `050_Registro.dtsx`
- `050_Registro_Ampliado.dtsx`
- `Registro_AgrupamientoOfertaEntregaPublicacion.dtsx`
- `Registro_ConversionActivaPublicacion.dtsx`
- `Registro_LiquidacionPublicacion.dtsx`
- `Registro_OperacionCarteraExtension.dtsx`
- `Registro_OperacionCarteraMovimientoActivo.dtsx`
- `Registro_OperacionCarteraUsuario.dtsx`
- `Registro_Portfolio.dtsx`
- `Registro_RelacionOperacionesAFijar.dtsx`
- `Registro_ReservaOfertaEntregaPublicacion.dtsx`

## Paquete fuera de `dtproj`

- `LibroDeOrdenes.dtsx`

## Matriz inicial de tablas

| Tabla | Paquete o paquetes principales | Evidencia observada |
| --- | --- | --- |
| `Registro.OperacionCarteraPublicacionHistorico` | `050_Registro.dtsx`, `050_Registro_Ampliado.dtsx` | `OpenRowset` |
| `Registro.AgrupamientoOfertaEntregaPublicacion` | `Registro_AgrupamientoOfertaEntregaPublicacion.dtsx` | `OpenRowset` |
| `Registro.LibroOrden` | `LibroDeOrdenes.dtsx` | `OpenRowset` |
| `Registro.OperacionCarteraCanceladaHistorico` | `010_OperacionCarteraCancelada.dtsx` | `DELETE`, `UPDATE`, `OpenRowset` |
| `Registro.OperacionCarteraCancelada` | `010_OperacionCarteraCancelada.dtsx` | `OpenRowset` |
| `Registro.ReservaOfertaEntregaPublicacion` | `Registro_ReservaOfertaEntregaPublicacion.dtsx` | `OpenRowset` |
| `Registro.RelacionOperacionesAFijar` | `Registro_RelacionOperacionesAFijar.dtsx` | `DELETE`, `UPDATE`, `OpenRowset` |
| `Registro.LiquidacionPublicacion` | `Registro_LiquidacionPublicacion.dtsx` | `DELETE`, `OpenRowset` |
| `Registro.OperacionCarteraExtension` | `Registro_OperacionCarteraExtension.dtsx` | `UPDATE`, `OpenRowset` |
| `Registro.OperacionCarteraMovimientoActivo` | `Registro_OperacionCarteraExtension.dtsx`, `Registro_OperacionCarteraMovimientoActivo.dtsx` | `OpenRowset` |
| `Registro.ConversionActivaPublicacion` | `Registro_ConversionActivaPublicacion.dtsx` | `OpenRowset` |
| `Registro.PosicionCuotaPartistaPublicacion` | `Contribucion_PosicionCuotaPartista.dtsx` | `OpenRowset` |
| `Registro.LiquidacionValoresHistorico` | `020_LiquidacionValores.dtsx` | `DELETE`, `UPDATE`, `OpenRowset` |
| `Registro.OperacionCarteraUsuario` | `Registro_OperacionCarteraUsuario.dtsx` | `OpenRowset` |
| `Registro.Portfolio` | `Registro_Portfolio.dtsx` | `DELETE`, `OpenRowset` |

## Tablas sin evidencia observada

- `Registro.PortfolioDetalle`
- `Registro.OperacionCarteraPublicacion`
- `Registro.PortfolioDetalleActual`
- `Registro.OperacionCarteraOnlinePublicacion`
- `Registro.PortfolioResumen`
- `Registro.OperacionCarteraValores`
- `Registro.TipoCoberturaMensaje`
- `Registro.SolicitudEjercicioOpcion`
- `Registro.SolicitudEjercicioOpcionDetalle`
- `Registro.CambioCoberturaDetalle`
- `Registro.CoberturaInicialDetalle`
- `Registro.Cartera`
- `Registro.LiquidacionValores`
- `Registro.ReporteOperacionPublicacion`

## Nota

Seguramente valga la pena una fase específica para `Registro`, porque mezcla cargas claras y zonas todavía opacas del modelo.

## Artefactos de soporte

- [registro-tablas-matriz.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/registro-tablas-matriz.csv)
- [registro-paquete-tabla-matriz.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/registro-paquete-tabla-matriz.csv)
