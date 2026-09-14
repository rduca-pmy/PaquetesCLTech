# Mapeo CDC - primera tanda

## Alcance

Esta primera tanda cruza funciones CDC de `Clearing.sql` contra tablas y procedimientos candidatos en `Publicacion.sql` para los dominios:

- `Registro`
- `Contribucion`
- `Mensajes`
- `MensajesGeneral`

## Resumen

- Funciones CDC analizadas: `14`
- Mapeos directos: `11`
- Mapeos probables: `2`
- Mapeos ambiguos: `1`
- Sin destino AP5 identificado: `0`
- Fichas CDC generadas para esta tanda: `14`

## Matriz CDC -> AP5

| Funcion CDC | Tabla AP5 candidata | Procedimiento o mecanismo AP5 candidato | Clasificacion | Confianza |
| --- | --- | --- | --- | --- |
| `cdc.fn_cdc_get_Registro_OperacionCartera_Publicacion` | `Registro.OperacionCarteraPublicacionHistorico`, `Registro.OperacionCarteraPublicacion`, `Registro.OperacionCarteraOnlinePublicacion` | `Registro.MergeOperacionCarteraPublicacion`, `Registro.MergeOperacionCarteraPublicacionActual`, `Registro.MergeOperacionCarteraOnlinePublicacion` | `mapeo_directo` | `alta` |
| `cdc.fn_cdc_get_Registro_OperacionCartera_Publicacion_old` | `Registro.OperacionCarteraPublicacionHistorico`, `Registro.OperacionCarteraPublicacion` | `Registro.MergeOperacionCarteraPublicacion` | `mapeo_directo` | `media` |
| `cdc.fn_cdc_get_Registro_CancelacionCartera_Publicacion` | `Registro.OperacionCarteraCanceladaHistorico`, `Registro.OperacionCarteraCancelada` | `Registro.MergeCancelacionCarteraPublicacion`, `Registro.MergeCancelacionCarteraPublicacionActual` | `mapeo_directo` | `alta` |
| `cdc.fn_cdc_get_Registro_RelacionOperacionAFijar_Publicacion` | `Registro.RelacionOperacionesAFijar` | `Registro_RelacionOperacionesAFijar.dtsx` | `mapeo_directo` | `alta` |
| `cdc.fn_cdc_get_Registro_AccionOperacion_Publicacion` | `Registro.OperacionCarteraPublicacion`, `Registro.OperacionCarteraPublicacionHistorico` | pendiente de identificar | `mapeo_ambiguo` | `media` |
| `cdc.fn_cdc_get_Contribucion_AltaCuentaMercadoExterno_Publicacion` | `Contribucion.AltaCuentaMercadoExterno` | `Contribucion.MergeAltaCuentaMercadoExterno` | `mapeo_directo` | `alta` |
| `cdc.fn_cdc_get_Contribucion_CambioEstadoCuenta_Publicacion` | `Contribucion.CambioEstadoCuenta` | `Contribucion.MergeCambioEstadoCuenta` | `mapeo_directo` | `alta` |
| `cdc.fn_cdc_get_Contribucion_Cancelacion_Publicacion` | `Contribucion.Cancelacion` | `Contribucion.MergeCancelacion` | `mapeo_directo` | `alta` |
| `cdc.fn_cdc_get_Contribucion_Cuenta_Publicacion` | `Contribucion.Cuenta`, `Personas.CuentaRegistroPublicacion` | `Contribucion.InsertCuenta`, `Contribucion.InsertCuentas`, `Personas.MergeCuentaRegistroPublicacion` | `mapeo_probable` | `media` |
| `cdc.fn_cdc_get_Contribucion_MargenEntrega_Publicacion` | `Contribucion.MargenEntrega` | `Contribucion_MargenEntrega.dtsx` | `mapeo_probable` | `media` |
| `cdc.fn_cdc_get_Mensajes_MensajeCompensacionDepositariaDetalle_Publicacion` | `Mensajes.MensajeCompensacionDepositariaDetalle` | `Mensajes.InsertMensajeCompensacionMTMDepositarias`, `MensajesGeneral.MergeMensajePublicacion` | `mapeo_directo` | `alta` |
| `cdc.fn_cdc_get_Mensajes_MensajeDepositoIVA_Publicacion` | `Mensajes.MensajeDepositoIva`, `Mensajes.MensajeDepositoIvaDetalle` | `Mensajes.InsertMensajeDepositoDeIVA`, `Mensajes.InsertMensajeDepositoDeIVADetalle`, `MensajesGeneral.MergeMensajePublicacion` | `mapeo_directo` | `alta` |
| `cdc.fn_cdc_get_Mensajes_MensajeTransferenciaCuotaParte_Publicacion` | `Mensajes.MensajeTransferenciaCuotaparteIngreso`, `Mensajes.MensajeTransferenciaCuotaparteEgreso` | `Mensajes.InsertMensajeTransferenciaCuotaparteIngreso`, `Mensajes.InsertMensajeTransferenciaCuotaparteEgreso`, `MensajesGeneral.MergeMensajePublicacion` | `mapeo_directo` | `alta` |
| `cdc.fn_cdc_get_MensajesGeneral_Mensaje_Publicacion` | `MensajesGeneral.MensajePublicacion`, `MensajesGeneral.MensajePublicacionHistorico` | `MensajesGeneral.MergeMensajePublicacion` | `mapeo_directo` | `alta` |

## Hallazgos

- `Mensajes` y `MensajesGeneral` no tenian evidencia SSIS directa, pero si tienen funciones CDC y procedimientos AP5 candidatos.
- `Registro.OperacionCartera` y `Registro.CancelacionCartera` no llegan a AP5 con el mismo nombre exacto, sino como tablas de publicacion e historico.
- `Contribucion.AltaCuentaMercadoExterno`, `Contribucion.CambioEstadoCuenta` y `Contribucion.Cancelacion` son los casos mas limpios de la tanda porque tienen funcion CDC, tabla AP5 y `Merge*` especifico.
- `Contribucion.Cuenta` requiere mas cuidado porque AP5 muestra inserts de cuenta y tambien una relacion con `Personas.MergeCuentaRegistroPublicacion`.
- `Registro.AccionOperacion` queda como ambiguo: la funcion existe, pero no se encontro una tabla AP5 homonima ni un `Merge*` especifico en esta pasada.

## Implicancia para la documentacion

Esta tanda cambia la lectura de cobertura de `Mensajes` y `MensajesGeneral`: aunque en SSIS no aparecian como sincronizados, si tienen un camino CDC documentable desde PBP.

Para `Contribucion`, la tanda confirma que varias tablas marcadas como `sin_evidencia_ssis` no son necesariamente locales AP5; algunas parecen alimentarse por CDC.

## Proxima profundizacion sugerida

1. Profundizar `Contribucion.Cuenta` para determinar si el destino final principal es `Contribucion.Cuenta`, `Personas.CuentaRegistroPublicacion` o ambos.
2. Resolver `Registro.AccionOperacion` buscando el consumidor AP5 exacto del payload CDC.
3. Avanzar con la segunda tanda CDC sobre `Compensacion`, `Productos`, `Personas`, `General`, `ComprobantesGeneral` y `Contabilidad`.

## Artefactos de soporte

- [cdc-mapeo-primer-tanda.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/cdc-mapeo-primer-tanda.csv)
- [cdc-funciones-inventario.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/cdc-funciones-inventario.csv)

## Fichas CDC de la tanda

- [Registro.OperacionCartera](fichas/registro-operacioncartera-publicacion.md)
- [Registro.OperacionCartera legacy](fichas/registro-operacioncartera-publicacion-old.md)
- [Registro.CancelacionCartera](fichas/registro-cancelacioncartera-publicacion.md)
- [Registro.RelacionOperacionAFijar](fichas/registro-relacionoperacionafijar-publicacion.md)
- [Registro.AccionOperacion](fichas/registro-accionoperacion-publicacion.md)
- [Contribucion.AltaCuentaMercadoExterno](fichas/contribucion-altacuentamercadoexterno-publicacion.md)
- [Contribucion.CambioEstadoCuenta](fichas/contribucion-cambioestadocuenta-publicacion.md)
- [Contribucion.Cancelacion](fichas/contribucion-cancelacion-publicacion.md)
- [Contribucion.Cuenta](fichas/contribucion-cuenta-publicacion.md)
- [Contribucion.MargenEntrega](fichas/contribucion-margenentrega-publicacion.md)
- [Mensajes.MensajeCompensacionDepositariaDetalle](fichas/mensajes-mensajecompensaciondepositariadetalle-publicacion.md)
- [Mensajes.MensajeDepositoIVA](fichas/mensajes-mensajedepositoiva-publicacion.md)
- [Mensajes.MensajeTransferenciaCuotaParte](fichas/mensajes-mensajetransferenciacuotaparte-publicacion.md)
- [MensajesGeneral.Mensaje](fichas/mensajesgeneral-mensaje-publicacion.md)
