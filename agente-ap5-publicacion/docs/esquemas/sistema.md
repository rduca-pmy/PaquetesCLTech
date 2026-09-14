# Esquema Sistema

## Resumen

- Tablas en `Publicacion.sql`: `90`
- Tablas con evidencia en SSIS: `56`
- Tablas sin evidencia en SSIS: `34`

## Lectura inicial

Es el esquema mas grande del modelo y tiene cobertura amplia, aunque no completa. Muchas tablas parecen catalogos o diccionarios funcionales reutilizados por distintos jobs.

## Paquetes relevantes

- `010_Sistema.dtsx`
- `040_Productos.dtsx`
- `400_Usuarios.dtsx`
- `510_MovimientoPublicacion.dtsx`
- `950_PortfolioDeActivos.dtsx`
- `Parametros_Notificacion.dtsx`
- `ProcesoPublicacion.dtsx`
- `RolMultiCel.dtsx`
- `RolMulticomitentes.dtsx`

## Paquetes fuera de `dtproj`

- `510_MovimientoPublicacion_7Dias.dtsx`
- `510_MovimientoPublicacionHistorico.dtsx`
- `Contribucion_OfertaEntrega.dtsx`
- `Horus_Productos_Ajuste (1).dtsx`
- `Horus_Productos_Ajuste_.dtsx`
- `MovimientoPublicacionUpdateTesting.dtsx`

## Matriz inicial de tablas

| Tabla | Paquete o paquetes principales | Evidencia observada |
| --- | --- | --- |
| `Sistema.Accion` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.AccionContribucion` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.CadenaAprobacion` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.Cargo` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.ConceptoComprobante` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.ConceptoComprobanteImpuesto` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.CondicionImpuesto` | `010_Sistema.dtsx` | `OpenRowset`, `UPDATE` |
| `Sistema.Dia` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.DivisionPrimaria` | `010_Sistema.dtsx` | `OpenRowset`, `UPDATE` |
| `Sistema.DivisionSecundaria` | `010_Sistema.dtsx` | `OpenRowset`, `UPDATE` |
| `Sistema.Entidad` | `010_Sistema.dtsx` | `OpenRowset`, `UPDATE` |
| `Sistema.EstadoContribucion` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.EstadoMedidaPreventiva` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.EstadoReporteOperacion` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.FrecuenciaFacturacion` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.Impuesto` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.Industria` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.MedioCobro` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.MedioComunicacion` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.MedioPago` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.MetodoCancelacion` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.ModeloValuacion` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.MomentoCreacion` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.MotivoRechazoCheque` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.NotificacionOperacion` | `Parametros_Notificacion.dtsx` | `OpenRowset`, `SELECT` |
| `Sistema.Origen` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.OrigenConversion` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.Originador` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.Pais` | `010_Sistema.dtsx`, `400_Usuarios.dtsx`, `510_MovimientoPublicacion.dtsx`, `510_MovimientoPublicacionHistorico.dtsx`, `510_MovimientoPublicacion_7Dias.dtsx`, `950_PortfolioDeActivos.dtsx`, `MovimientoPublicacionUpdateTesting.dtsx`, `ProcesoPublicacion.dtsx`, `Registro_PortfolioDetalleActualizarSaldo.dtsx`, `RolMultiCel.dtsx`, `RolMulticomitentes.dtsx` | `OpenRowset`, `UPDATE` |
| `Sistema.Periodicidad` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.RubroCuentaContable` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.SaldoHabitual` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.SegmentoMercado` | `040_Productos.dtsx` | `OpenRowset` |
| `Sistema.TipoAccionOperacion` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.TipoAnulacion` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.TipoCheque` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.TipoChequera` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.TipoComprobante` | `010_Sistema.dtsx` | `OpenRowset`, `UPDATE` |
| `Sistema.TipoContrato` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.TipoCuentaContable` | `010_Sistema.dtsx` | `OpenRowset`, `UPDATE` |
| `Sistema.TipoDivisionPrimaria` | `010_Sistema.dtsx` | `OpenRowset`, `UPDATE` |
| `Sistema.TipoDivisionSecundaria` | `010_Sistema.dtsx` | `OpenRowset`, `UPDATE` |
| `Sistema.TipoEntidadBursatil` | `010_Sistema.dtsx` | `OpenRowset`, `UPDATE` |
| `Sistema.TipoEstado` | `010_Sistema.dtsx` | `OpenRowset`, `UPDATE` |
| `Sistema.TipoIdentificacion` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.TipoMovimientoComprobante` | `010_Sistema.dtsx` | `OpenRowset`, `UPDATE` |
| `Sistema.TipoMovimientoContable` | `010_Sistema.dtsx` | `OpenRowset`, `UPDATE` |
| `Sistema.TipoOpcion` | `010_Sistema.dtsx` | `OpenRowset`, `UPDATE` |
| `Sistema.TipoOperacion` | `010_Sistema.dtsx` | `OpenRowset`, `UPDATE` |
| `Sistema.TipoOrden` | `010_Sistema.dtsx` | `OpenRowset`, `UPDATE` |
| `Sistema.TipoRenta` | `010_Sistema.dtsx` | `OpenRowset`, `UPDATE` |
| `Sistema.TipoServicio` | `010_Sistema.dtsx` | `OpenRowset`, `UPDATE` |
| `Sistema.TipoTransaccionReporteOperacion` | `010_Sistema.dtsx` | `OpenRowset`, `UPDATE` |
| `Sistema.TipoTransformacionActivo` | `010_Sistema.dtsx` | `OpenRowset` |
| `Sistema.TratamientoOpcion` | `010_Sistema.dtsx` | `OpenRowset`, `UPDATE` |
| `Sistema.VariacionAplicada` | `010_Sistema.dtsx` | `OpenRowset`, `UPDATE` |

## Tablas sin evidencia observada

- `Sistema.Tramo`
- `Sistema.TipoTransferencia`
- `Sistema.EstadoInstruccion`
- `Sistema.TipoCompraVenta`
- `Sistema.TipoCartera`
- `Sistema.EstadoSolicitudCuentaRegistro`
- `Sistema.TipoDeudaWarrant`
- `Sistema.TipoParteWarrant`
- `Sistema.TipoRelacionEntreCuentas`
- `Sistema.EstadoCancelacionManual`
- `Sistema.MetodoCancelacionManual`
- `Sistema.TipoTransferenciaWarrants`
- `Sistema.GrupoProductoMetodoCancelacion`
- `Sistema.EstadoTransferenciaBVA`
- `Sistema.TipoMovimientoActivo`
- `Sistema.TipoTransferenciaMAE`
- `Sistema.EstadoOrden`
- `Sistema.TipoOrdenExterna`
- `Sistema.EstadoDerivacionDRP`
- `Sistema.ConversionDatosExternos`
- `Sistema.EstadoCOE`
- `Sistema.EstadoEventoCorporativo`
- `Sistema.EstadoRepo`
- `Sistema.EstadoTransferenciaEntreAgentes`
- `Sistema.FuenteConversion`
- `Sistema.Sistema`
- `Sistema.Tablero`
- `Sistema.TipoAcreencia`
- `Sistema.TipoCobertura`
- `Sistema.TipoConversion`
- `Sistema.TipoDeNota`
- `Sistema.TipoMensajeCertificadoDepositoWarrant`
- `Sistema.TipoOperacionOperatoriaBCRA`
- `Sistema.TipoTransaccionOrden`

## Nota

Por volumen y centralidad, este esquema conviene abordarlo en capas y no tabla por tabla de una sola vez.

## Artefactos de soporte

- [sistema-tablas-matriz.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/sistema-tablas-matriz.csv)
