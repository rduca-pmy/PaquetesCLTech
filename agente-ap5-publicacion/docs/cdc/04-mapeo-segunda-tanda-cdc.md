# Mapeo CDC - segunda tanda

## Alcance

Esta segunda tanda cruza funciones CDC de `Clearing.sql` contra tablas, procedimientos y paquetes candidatos en `Publicacion.sql` y `IntegrationServices/Publicacion` para los dominios:

- `Compensacion`
- `Productos`
- `Personas`
- `General`
- `ComprobantesGeneral`
- `Contabilidad`

## Resumen

- Funciones CDC analizadas: `21`
- Mapeos directos: `8`
- Mapeos probables: `12`
- Mapeos ambiguos: `1`
- Sin destino AP5 identificado: `0`
- Fichas CDC generadas para esta tanda: `21`

## Matriz CDC -> AP5

| Funcion CDC | Tabla AP5 candidata | Procedimiento o mecanismo AP5 candidato | Clasificacion | Confianza |
| --- | --- | --- | --- | --- |
| `cdc.fn_cdc_get_Compensacion_BonificacionPorPlazo_Publicacion` | `Compensacion.MargenPublicacionHistorico`, `Compensacion.MargenPublicacion` | `999_MargenPublicacion.dtsx`, `999_MargenPublicacion_5Dias.dtsx` | `mapeo_probable` | `baja` |
| `cdc.fn_cdc_get_Compensacion_GrupoEscenarioPorcentajeBonificacionPorPlazo_Publicacion` | `Compensacion.MargenPublicacionHistorico`, `Compensacion.MargenPublicacion` | `999_MargenPublicacion.dtsx`, `999_MargenPublicacion_5Dias.dtsx` | `mapeo_probable` | `baja` |
| `cdc.fn_cdc_get_Compensacion_GrupoProducto_Publicacion` | `Productos.Contrato`, `Productos.ListaContrato` | `040_Productos.dtsx`, `_100_SecurityList.dtsx` | `mapeo_ambiguo` | `baja` |
| `cdc.fn_cdc_get_Compensacion_Margen_Publicacion` | `Compensacion.MargenPublicacion`, `Compensacion.MargenPublicacionHistorico` | `999_MargenPublicacion.dtsx`, `999_MargenPublicacion_5Dias.dtsx`, `PersonasEntrega.dtsx` | `mapeo_probable` | `media` |
| `cdc.fn_cdc_get_Compensacion_MargenEntreProductoNivel_Publicacion` | `Compensacion.MargenDetalleGrupoProducto` | `Compensacion_MargenDetalleGrupoProducto.dtsx` | `mapeo_probable` | `media` |
| `cdc.fn_cdc_get_Compensacion_MargenLimitePosicionAbierta_Publicacion` | `Compensacion.MargenPublicacion`, `Compensacion.MargenPublicacionHistorico` | `999_MargenPublicacion.dtsx`, `999_MargenPublicacion_5Dias.dtsx` | `mapeo_probable` | `baja` |
| `cdc.fn_cdc_get_Compensacion_MargenProducto_Publicacion` | `Compensacion.MargenDetalleGrupoProducto`, `Compensacion.MargenesContrato` | `Compensacion_MargenDetalleGrupoProducto.dtsx`, `600_MargenesContratos.dtsx` | `mapeo_probable` | `media` |
| `cdc.fn_cdc_get_Compensacion_ParametroContrato_Publicacion` | `Compensacion.ParametroContratoPublicacion` | `Compensacion_ParametroContratoPublicacion.dtsx` | `mapeo_directo` | `alta` |
| `cdc.fn_cdc_get_Compensacion_PorcentajeMontoDrpPorCuenta_Publicacion` | `Compensacion.DerivacionDRP` | `Compensacion_DerivacionDRP.dtsx`, `Compensacion_DerivacionDRP_Update.dtsx` | `mapeo_probable` | `media` |
| `cdc.fn_cdc_get_ComprobantesGeneral_ComprobanteVenta_Publicacion` | `ComprobantesGeneral.ComprobantePublicacion` | `Comprobantes_Facturacion.dtsx`, `Comprobantes_Liquidaciones.dtsx` | `mapeo_probable` | `alta` |
| `cdc.fn_cdc_get_ComprobantesGeneral_ComprobanteVentaDetalle_Publicacion_OLD` | `ComprobantesGeneral.ComprobanteDetallePublicacion` | `Comprobantes_Facturacion.dtsx`, `Comprobantes_Liquidaciones.dtsx` | `mapeo_probable` | `media` |
| `cdc.fn_cdc_get_Contabilidad_Movimiento_Publicacion` | `Contabilidad.MovimientoPublicacionHistorico` | `Contabilidad.MergeMovimientoPublicacion`, `965_Movimientos.dtsx` | `mapeo_probable` | `alta` |
| `cdc.fn_cdc_get_Contabilidad_MovimientoDetalle_Publicacion` | `Contabilidad.MovimientoPublicacionHistorico` | `Contabilidad.MergeMovimientoDetallePublicacion`, `965_Movimientos.dtsx` | `mapeo_probable` | `alta` |
| `cdc.fn_cdc_get_General_CotizacionMoneda_Publicacion` | `General.CotizacionMoneda` | `General.MergeCotizacionMoneda`, `020_General.dtsx` | `mapeo_directo` | `alta` |
| `cdc.fn_cdc_get_General_Proceso_Publicacion` | `General.Proceso` | `020_General.dtsx` | `mapeo_directo` | `alta` |
| `cdc.fn_cdc_get_Personas_CuentaNeteo_Publicacion` | `Personas.CuentaNeteo`, `Personas.CuentaNeteoPublicacion` | `030_PersonasGeneral*` | `mapeo_directo` | `alta` |
| `cdc.fn_cdc_get_Personas_CuentaRegistro_Publicacion` | `Personas.CuentaRegistro`, `Personas.CuentaRegistroPublicacion` | `Personas.MergeCuentaRegistroPublicacion`, `030_PersonasGeneral*`, `031_CuentaRegistroPublicacion.dtsx` | `mapeo_directo` | `alta` |
| `cdc.fn_cdc_get_Personas_CuentaRegistroGrupoProductoCancelacion_Publicacion` | `Personas.CuentaRegistroGrupoProductoCancelacion`, `Personas.CuentaRegistroPublicacion` | `031_CuentaRegistroPublicacion.dtsx` | `mapeo_directo` | `alta` |
| `cdc.fn_cdc_get_Productos_Ajuste_Publicacion` | `Productos.Ajuste` | `040_Productos.dtsx`, `Horus_Productos_Ajuste*.dtsx` | `mapeo_directo` | `alta` |
| `cdc.fn_cdc_get_Productos_Contrato_Publicacion` | `Productos.Contrato` | `040_Productos.dtsx`, `Horus_Productos_Contrato.dtsx` | `mapeo_directo` | `alta` |
| `cdc.fn_cdc_get_Productos_ContratoMensajeWarrant_Publicacion` | `Activos.ActivoCertificadoDepositoWarrantPublicacion`, `Mensajes.MensajeCertificadoDepositoWarrant`, `Productos.ProductoWarrant` | `Activos_ActivoCertificadoDepositoWarrantPublicacion.dtsx`, `MensajesGeneral.InsertMensajeWarrant` | `mapeo_probable` | `media` |

## Hallazgos

- `Personas`, `Productos` y `General` tienen los casos mas limpios de la tanda porque varias funciones CDC tienen tabla AP5 homonima o tabla `*Publicacion` cercana.
- `Compensacion` es el dominio mas difuso: PBP expone funciones CDC muy especificas, pero AP5 consolida la salida en tablas publicadas de margen, derivacion o parametros.
- `ComprobantesGeneral` no conserva los nombres `ComprobanteVenta` y `ComprobanteVentaDetalle` en AP5; los destinos documentables son `ComprobantePublicacion` y `ComprobanteDetallePublicacion`.
- `Contabilidad` consolida `Movimiento` y `MovimientoDetalle` en `MovimientoPublicacionHistorico`, con procedimientos `MergeMovimientoPublicacion` y `MergeMovimientoDetallePublicacion`.
- `Productos.ContratoMensajeWarrant` cruza dominios: nace como producto/contrato en Clearing, pero en AP5 aparece vinculado a activos Warrant y mensajes Warrant.

## Implicancia para la documentacion

Esta tanda confirma que no siempre hay una relacion 1:1 entre funcion CDC y tabla AP5. En varios dominios el nombre CDC representa la entidad fuente de PBP, mientras que AP5 publica una vista funcional, historica o enriquecida con otro nombre.

Para la documentacion final, conviene mantener tres niveles:

- `directo`: funcion CDC y tabla AP5 alineadas por nombre o por `*Publicacion`.
- `probable`: destino AP5 funcionalmente equivalente, pero sin consumidor exacto observado.
- `ambiguo`: hay uso del dato en AP5, pero el destino final no queda cerrado.

## Proxima profundizacion sugerida

1. Profundizar los CDC de `Compensacion` con baja confianza, especialmente bonificaciones, grupo producto y limite de posicion abierta.
2. Validar si `Contabilidad.MergeMovimientoPublicacion` y `Contabilidad.MergeMovimientoDetallePublicacion` son consumidores directos del servicio CDC o procedimientos auxiliares.
3. Conectar `Productos.ContratoMensajeWarrant` con el circuito completo de `Activos_ActivoCertificadoDepositoWarrantPublicacion.dtsx` y `MensajesGeneral.InsertMensajeWarrant`.

## Artefactos de soporte

- [cdc-mapeo-segunda-tanda.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/cdc-mapeo-segunda-tanda.csv)
- [cdc-funciones-inventario.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/cdc-funciones-inventario.csv)

## Fichas CDC de la tanda

- [Compensacion.BonificacionPorPlazo](fichas/compensacion-bonificacionporplazo-publicacion.md)
- [Compensacion.GrupoEscenarioPorcentajeBonificacionPorPlazo](fichas/compensacion-grupoescenarioporcentajebonificacionporplazo-publicacion.md)
- [Compensacion.GrupoProducto](fichas/compensacion-grupoproducto-publicacion.md)
- [Compensacion.Margen](fichas/compensacion-margen-publicacion.md)
- [Compensacion.MargenEntreProductoNivel](fichas/compensacion-margenentreproductonivel-publicacion.md)
- [Compensacion.MargenLimitePosicionAbierta](fichas/compensacion-margenlimiteposicionabierta-publicacion.md)
- [Compensacion.MargenProducto](fichas/compensacion-margenproducto-publicacion.md)
- [Compensacion.ParametroContrato](fichas/compensacion-parametrocontrato-publicacion.md)
- [Compensacion.PorcentajeMontoDrpPorCuenta](fichas/compensacion-porcentajemontodrpporcuenta-publicacion.md)
- [ComprobantesGeneral.ComprobanteVenta](fichas/comprobantesgeneral-comprobanteventa-publicacion.md)
- [ComprobantesGeneral.ComprobanteVentaDetalle legacy](fichas/comprobantesgeneral-comprobanteventadetalle-publicacion-old.md)
- [Contabilidad.Movimiento](fichas/contabilidad-movimiento-publicacion.md)
- [Contabilidad.MovimientoDetalle](fichas/contabilidad-movimientodetalle-publicacion.md)
- [General.CotizacionMoneda](fichas/general-cotizacionmoneda-publicacion.md)
- [General.Proceso](fichas/general-proceso-publicacion.md)
- [Personas.CuentaNeteo](fichas/personas-cuentaneteo-publicacion.md)
- [Personas.CuentaRegistro](fichas/personas-cuentaregistro-publicacion.md)
- [Personas.CuentaRegistroGrupoProductoCancelacion](fichas/personas-cuentaregistrogrupoproductocancelacion-publicacion.md)
- [Productos.Ajuste](fichas/productos-ajuste-publicacion.md)
- [Productos.Contrato](fichas/productos-contrato-publicacion.md)
- [Productos.ContratoMensajeWarrant](fichas/productos-contratomensajewarrant-publicacion.md)
