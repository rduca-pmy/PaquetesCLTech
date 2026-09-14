# Esquema Contribucion

## Resumen

- Tablas en `Publicacion.sql`: `38`
- Tablas con evidencia en SSIS: `10`
- Tablas sin evidencia en SSIS: `28`

## Lectura inicial

La cobertura SSIS directa es relativamente baja para el tamano del esquema. Esto es coherente con el contexto funcional: muchas tablas de `Contribucion` pueden depender de circuitos de mensajes, colas o procesos fuera del alcance actual.

## Paquetes relevantes

- `Contribucion_BonificacionDMA.dtsx`
- `Contribucion_Cuenta.dtsx`
- `Contribucion_DepositoIvaPublicacion (1).dtsx`
- `Contribucion_DistribucionActivo.dtsx`
- `Contribucion_InstrumentoDigital.dtsx`
- `Contribucion_MargenEntrega.dtsx`
- `Contribucion_Orden_Contingencia.dtsx`
- `Contribucion_Orden_Estado.dtsx`

## Paquetes fuera de `dtproj`

- `Contribucion_DepositoIvaPublicacion.dtsx`
- `Contribucion_OfertaEntrega.dtsx`
- `Contribucion_RelacionOperacionesAFijar.dtsx`

## Matriz inicial de tablas

| Tabla | Paquete o paquetes principales | Evidencia observada |
| --- | --- | --- |
| `Contribucion.BonificacionDMA` | `Contribucion_BonificacionDMA.dtsx` | `OpenRowset`, `SELECT` |
| `Contribucion.Cuenta` | `Contribucion_Cuenta.dtsx` | `UPDATE` |
| `Contribucion.DepositoIvaPublicacion` | `Contribucion_DepositoIvaPublicacion (1).dtsx`, `Contribucion_DepositoIvaPublicacion.dtsx` | `OpenRowset` |
| `Contribucion.Instrumento` | `992_Ordenes.dtsx`, `993_AjustesInteresAbierto_EXT.dtsx`, `994_TradeVolumen.dtsx`, `Contribucion_DistribucionActivo.dtsx`, `MarketData_Ajustes.dtsx`, `MarketData_AjustesRFX20.dtsx`, `MarketData_AjustesViejo.dtsx`, `MarketData_ClossingPrices.dtsx`, `MarketData_CotizacionSpot.dtsx`, `MarketData_InteresAbierto.dtsx`, `MarketData_SoloAjustes.dtsx`, `MarketData_SoloAjustes_SinProceso.dtsx` | `OpenRowset` |
| `Contribucion.InstrumentoDigital` | `Contribucion_InstrumentoDigital.dtsx` | `OpenRowset`, `SELECT` |
| `Contribucion.MargenEntrega` | `Contribucion_MargenEntrega.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `Contribucion.OfertaEntrega` | `Contribucion_OfertaEntrega.dtsx` | `OpenRowset`, `SELECT` |
| `Contribucion.Orden` | `992_Ordenes.dtsx`, `Contribucion_Orden_Contingencia.dtsx`, `Contribucion_Orden_Estado.dtsx` | `OpenRowset`, `UPDATE` |
| `Contribucion.OrdenLado` | `992_Ordenes.dtsx` | `OpenRowset` |

## Tablas sin evidencia observada

- `Contribucion.Repo`
- `Contribucion.OrdenParte`
- `Contribucion.MovimientoCustodia`
- `Contribucion.Cancelacion`
- `Contribucion.CambioEstadoCuenta`
- `Contribucion.OTCAgroDetalle`
- `Contribucion.OTCAgro`
- `Contribucion.DistribucionActivo`
- `Contribucion.DistribucionActivoDetalle`
- `Contribucion.InstrumentoDigitalParte`
- `Contribucion.ResumenCustodia`
- `Contribucion.ReporteOperacion`
- `Contribucion.Parte`
- `Contribucion.ReporteOperacionLado`
- `Contribucion.LadoParte`
- `Contribucion.ModificacionCuenta`
- `Contribucion.OfertaEntregaOperacion`
- `Contribucion.ActualizacionCuenta`
- `Contribucion.AgrupamientoOfertaEntrega`
- `Contribucion.AltaCuentaMercadoExterno`
- `Contribucion.ControlDuplicadosMovimientoCustodia`
- `Contribucion.Cotitulares`
- `Contribucion.LadoComision`
- `Contribucion.LadoImpuesto`
- `Contribucion.MensajeGarantiaMAE`
- `Contribucion.OrdersInsertContingency`
- `Contribucion.PosicionCuotaPartista`
- `Contribucion.ReporteOperacionMetodoPago`

## Nota

Este esquema seguramente va a necesitar una fase posterior dedicada a contribuciones y mensajeria, no solo a paquetes.

## Artefactos de soporte

- [contribucion-tablas-matriz.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/contribucion-tablas-matriz.csv)
