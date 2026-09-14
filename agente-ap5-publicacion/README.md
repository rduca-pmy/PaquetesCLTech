# Agente IA para Documentacion de Sincronizaciones AP5

Este proyecto organiza el relevamiento de como se llenan las tablas de `Publicacion` (AP5) a partir de los paquetes SSIS ubicados en `IntegrationServices/Publicacion`, usando como apoyo los esquemas `Clearing.sql` y `Publicacion.sql`.

## Objetivo

Responder de forma trazable estas dos preguntas:

- Como se llenan las tablas de AP5
- Cuales son las tablas que se llenan en AP5

## Alcance de esta fase

- Repositorio analizado: `IntegrationServices`
- Carpeta considerada: `IntegrationServices/Publicacion`
- Esquemas base de analisis: `Clearing.sql` y `Publicacion.sql`
- Criterio actual: jobs y paquetes SSIS
- Criterio diferido: funciones CDC de PBP y circuitos de mensajeria / contribucion
- Nota arquitectonica: la mayor parte de la logica funcional vive en base de datos; los fronts no son la fuente principal para reconstruir circuitos

## Mapa del proyecto

### Base metodologica

- [Contexto y alcance](docs/00-contexto-y-alcance.md)
- [Arquitectura de arneses](docs/01-arquitectura-de-arneses.md)
- [Proceso operativo](docs/02-proceso-operativo.md)
- [Criterios de extraccion](docs/03-criterios-de-extraccion.md)
- [Inventario inicial de paquetes](docs/04-inventario-inicial-paquetes.md)
- [Estado del inventario](docs/05-estado-del-inventario.md)
- [Registro de arneses](harnesses/registry.yaml)
- [Schema de ficha](schemas/ficha-sincronizacion.schema.json)
- [Template de ficha](templates/ficha-sincronizacion-tabla.md)

### Fase CDC

- [Contexto y alcance CDC](docs/cdc/00-contexto-y-alcance-cdc.md)
- [Metodologia CDC](docs/cdc/01-metodologia-cdc.md)
- [Inventario inicial de funciones CDC](docs/cdc/02-inventario-inicial-cdc.md)
- [Mapeo CDC primera tanda](docs/cdc/03-mapeo-primer-tanda-cdc.md)
- [Mapeo CDC segunda tanda](docs/cdc/04-mapeo-segunda-tanda-cdc.md)
- [Template de ficha CDC](templates/ficha-cdc-relacion.md)
- [cdc-funciones-inventario.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/cdc-funciones-inventario.csv)
- [cdc-mapeo-primer-tanda.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/cdc-mapeo-primer-tanda.csv)
- [cdc-mapeo-segunda-tanda.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/cdc-mapeo-segunda-tanda.csv)

### Resumen general

- [Resumen del resto de esquemas](docs/esquemas/00-resumen-resto-esquemas.md)
- [inventario-paquetes.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/inventario-paquetes.csv)
- [esquemas-restantes-resumen.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/esquemas-restantes-resumen.csv)

## Cobertura por esquema

| Esquema | Tablas totales | Con evidencia SSIS | Con ficha | Estado actual |
| --- | ---: | ---: | ---: | --- |
| `MarketData` | `1` | `1` | `1` | ejemplo completo, sin matriz CSV propia aun |
| `Personas` | `42` | `35` | `5` | matriz completa, fichas parciales |
| `PersonasGeneral` | `32` | `32` | `1` | matriz completa, ficha puntual |
| `Activos` | `20` | `17` | `17` | cerrado a nivel de fichas sincronizadas |
| `Compensacion` | `12` | `10` | `1` | matriz completa, ficha puntual |
| `ComprobantesGeneral` | `9` | `8` | `1` | matriz completa, ficha puntual |
| `Contabilidad` | `4` | `1` | `1` | matriz completa, ficha puntual |
| `Contribucion` | `38` | `9` | `1` | matriz completa, requiere fase posterior |
| `General` | `19` | `19` | `1` | matriz completa, ficha puntual |
| `Mensajes` | `31` | `0` | `0` | sin evidencia SSIS en esta fase |
| `MensajesGeneral` | `5` | `0` | `0` | sin evidencia SSIS en esta fase |
| `Parametros` | `32` | `16` | `1` | matriz completa, ficha puntual |
| `Productos` | `44` | `38` | `38` | cerrado a nivel de fichas sincronizadas |
| `Registro` | `29` | `15` | `15` | cerrado a nivel de fichas sincronizadas |
| `Sistema` | `90` | `56` | `1` | matriz completa, ficha puntual |

### Lectura rapida de cobertura

- Los esquemas mas avanzados en fichas son `Activos`, `Productos` y `Registro`.
- `Personas` y `PersonasGeneral` ya tienen buena base de matriz, pero todavia admiten mas fichas.
- `Mensajes` y `MensajesGeneral` siguen sin evidencia directa desde `IntegrationServices/Publicacion`.
- `Contribucion` necesita una segunda fase porque su cobertura por paquetes SSIS es baja para el tamano del esquema.

## Esquemas documentados

### Esquemas con matriz propia

- [MarketData](docs/esquemas/marketdata.md)
- [Personas](docs/esquemas/personas.md)
- [Activos](docs/esquemas/activos.md)
- [Compensacion](docs/esquemas/compensacion.md)
- [ComprobantesGeneral](docs/esquemas/comprobantesgeneral.md)
- [Contabilidad](docs/esquemas/contabilidad.md)
- [Contribucion](docs/esquemas/contribucion.md)
- [General](docs/esquemas/general.md)
- [Mensajes](docs/esquemas/mensajes.md)
- [MensajesGeneral](docs/esquemas/mensajesgeneral.md)
- [Parametros](docs/esquemas/parametros.md)
- [PersonasGeneral](docs/esquemas/personasgeneral.md)
- [Productos](docs/esquemas/productos.md)
- [Registro](docs/esquemas/registro.md)
- [Sistema](docs/esquemas/sistema.md)

### Matrices CSV por esquema

- [Personas](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/personas-tablas-matriz.csv)
- [Activos](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/activos-tablas-matriz.csv)
- [Compensacion](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/compensacion-tablas-matriz.csv)
- [ComprobantesGeneral](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/comprobantesgeneral-tablas-matriz.csv)
- [Contabilidad](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/contabilidad-tablas-matriz.csv)
- [Contribucion](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/contribucion-tablas-matriz.csv)
- [General](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/general-tablas-matriz.csv)
- [Mensajes](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/mensajes-tablas-matriz.csv)
- [MensajesGeneral](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/mensajesgeneral-tablas-matriz.csv)
- [Parametros](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/parametros-tablas-matriz.csv)
- [PersonasGeneral](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/personasgeneral-tablas-matriz.csv)
- [Productos](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/productos-tablas-matriz.csv)
- [Registro](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/registro-tablas-matriz.csv)
- [Sistema](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/sistema-tablas-matriz.csv)

### Matrices paquete -> tabla

- [Personas](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/personas-paquete-tabla-matriz.csv)
- [Activos](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/activos-paquete-tabla-matriz.csv)
- [Productos](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/productos-paquete-tabla-matriz.csv)
- [Registro](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/registro-paquete-tabla-matriz.csv)

## Fichas detalladas

### MarketData

- [InformacionDeMercado](docs/fichas/marketdata-informacion-de-mercado.md)

### Personas

- [CuentaDepositariaPublicacion](docs/fichas/personas-cuentadepositariapublicacion.md)
- [CuentaRegistroPublicacion](docs/fichas/personas-cuentaregistropublicacion.md)
- [DatosPatrimoniales](docs/fichas/personas-datospatrimoniales.md)
- [Parte](docs/fichas/personas-parte.md)
- [Usuario](docs/fichas/personas-usuario.md)

### PersonasGeneral

- [Persona](docs/fichas/personasgeneral-persona.md)

### Activos

- [Activo](docs/fichas/activos-activo.md)
- [ActivoCertificadoDepositoWarrantPublicacion](docs/fichas/activos-activocertificadodepositowarrantpublicacion.md)
- [ActivoPublicacion](docs/fichas/activos-activopublicacion.md)
- [ActivoPublicacionCuentaDepositaria](docs/fichas/activos-activopublicacioncuentadepositaria.md)
- [ActivoPublicacionFinalidad](docs/fichas/activos-activopublicacionfinalidad.md)
- [ActivoPublicacionMoneda](docs/fichas/activos-activopublicacionmoneda.md)
- [AvalPublicacion](docs/fichas/activos-avalpublicacion.md)
- [FondoCuentaDepositaria](docs/fichas/activos-fondocuentadepositaria.md)
- [FondoFinalidad](docs/fichas/activos-fondofinalidad.md)
- [FuenteCotizacionActivo](docs/fichas/activos-fuentecotizacionactivo.md)
- [GarantiasOpcionesMerval](docs/fichas/activos-garantiasopcionesmerval.md)
- [MovimientoCustodiaNoProcesadoPublicacion](docs/fichas/activos-movimientocustodianoprocesadopublicacion.md)
- [MovimientoPublicacion](docs/fichas/activos-movimientopublicacion.md)
- [MovimientoPublicacionExtension](docs/fichas/activos-movimientopublicacionextension.md)
- [OperacionCarteraGrupoOperacionCarteraPublicacion](docs/fichas/activos-operacioncarteragrupooperacioncarterapublicacion.md)
- [PortfolioDetalle](docs/fichas/activos-portfoliodetalle.md)
- [TipoMensajeCuentaDepositaria](docs/fichas/activos-tipomensajecuentadepositaria.md)

### Productos

- [Accion](docs/fichas/productos-accion.md)
- [AdministracionNotificacion](docs/fichas/productos-administracionnotificacion.md)
- [Ajuste](docs/fichas/productos-ajuste.md)
- [Caucion](docs/fichas/productos-caucion.md)
- [CertificadoDeposito](docs/fichas/productos-certificadodeposito.md)
- [Contrato](docs/fichas/productos-contrato.md)
- [ContratoAFijarPublicacion](docs/fichas/productos-contratoafijarpublicacion.md)
- [ContratoLicitacionEspecie](docs/fichas/productos-contratolicitacionespecie.md)
- [ContratoPorDiferencia](docs/fichas/productos-contratopordiferencia.md)
- [ConversionContrato](docs/fichas/productos-conversioncontrato.md)
- [Disponible](docs/fichas/productos-disponible.md)
- [DisponibleDeFuturo](docs/fichas/productos-disponibledefuturo.md)
- [FideicomisoFinanciero](docs/fichas/productos-fideicomisofinanciero.md)
- [FondoComunInversion](docs/fichas/productos-fondocomuninversion.md)
- [FondoComunInversionPublicacion](docs/fichas/productos-fondocomuninversionpublicacion.md)
- [FondoComunInversionPublicacionTipoPersona](docs/fichas/productos-fondocomuninversionpublicaciontipopersona.md)
- [Forward](docs/fichas/productos-forward.md)
- [ForwardOTC](docs/fichas/productos-forwardotc.md)
- [Futuro](docs/fichas/productos-futuro.md)
- [GrupoProductoCancelacionProducto](docs/fichas/productos-grupoproductocancelacionproducto.md)
- [InstrumentoDigital](docs/fichas/productos-instrumentodigital.md)
- [Licitacion](docs/fichas/productos-licitacion.md)
- [ListaContrato](docs/fichas/productos-listacontrato.md)
- [ListaContratoCombinado](docs/fichas/productos-listacontratocombinado.md)
- [NotificacionCanales](docs/fichas/productos-notificacioncanales.md)
- [NotificacionProductos](docs/fichas/productos-notificacionproductos.md)
- [ObligacionNegociable](docs/fichas/productos-obligacionnegociable.md)
- [Opcion](docs/fichas/productos-opcion.md)
- [OpcionOTC](docs/fichas/productos-opcionotc.md)
- [Producto](docs/fichas/productos-producto.md)
- [Puerto](docs/fichas/productos-puerto.md)
- [Subyacente](docs/fichas/productos-subyacente.md)
- [TarifaDevengada](docs/fichas/productos-tarifadevengada.md)
- [TarifaDevengadaStage](docs/fichas/productos-tarifadevengadastage.md)
- [TarifaPublicacion](docs/fichas/productos-tarifapublicacion.md)
- [Titulo](docs/fichas/productos-titulo.md)
- [ValoresOTCAgro](docs/fichas/productos-valoresotcagro.md)
- [Valuacion](docs/fichas/productos-valuacion.md)

### Registro

- [AgrupamientoOfertaEntregaPublicacion](docs/fichas/registro-agrupamientoofertaentregapublicacion.md)
- [ConversionActivaPublicacion](docs/fichas/registro-conversionactivapublicacion.md)
- [LibroOrden](docs/fichas/registro-libroorden.md)
- [LiquidacionPublicacion](docs/fichas/registro-liquidacionpublicacion.md)
- [LiquidacionValoresHistorico](docs/fichas/registro-liquidacionvaloreshistorico.md)
- [OperacionCarteraCancelada](docs/fichas/registro-operacioncarteracancelada.md)
- [OperacionCarteraCanceladaHistorico](docs/fichas/registro-operacioncarteracanceladahistorico.md)
- [OperacionCarteraExtension](docs/fichas/registro-operacioncarteraextension.md)
- [OperacionCarteraMovimientoActivo](docs/fichas/registro-operacioncarteramovimientoactivo.md)
- [OperacionCarteraPublicacionHistorico](docs/fichas/registro-operacioncarterapublicacionhistorico.md)
- [OperacionCarteraUsuario](docs/fichas/registro-operacioncarterausuario.md)
- [Portfolio](docs/fichas/registro-portfolio.md)
- [PosicionCuotaPartistaPublicacion](docs/fichas/registro-posicioncuotapartistapublicacion.md)
- [RelacionOperacionesAFijar](docs/fichas/registro-relacionoperacionesafijar.md)
- [ReservaOfertaEntregaPublicacion](docs/fichas/registro-reservaofertaentregapublicacion.md)

### Otros esquemas con ficha puntual

- [Compensacion.DerivacionDRP](docs/fichas/compensacion-derivaciondrp.md)
- [ComprobantesGeneral.Entidad](docs/fichas/comprobantesgeneral-entidad.md)
- [Contabilidad.MovimientoPublicacionHistorico](docs/fichas/contabilidad-movimientopublicacionhistorico.md)
- [Contribucion.Cuenta](docs/fichas/contribucion-cuenta.md)
- [General.ConversionUnidadMedida](docs/fichas/general-conversionunidadmedida.md)
- [Parametros.Finalidad](docs/fichas/parametros-finalidad.md)
- [Sistema.Accion](docs/fichas/sistema-accion.md)

## Estado actual

- Ya existe matriz por esquema para toda la carpeta `IntegrationServices/Publicacion`
- Ya existe ficha detallada para las tablas sincronizadas relevadas en `Personas`, `Activos`, `Productos` y `Registro`
- Ya existe una carpeta separada `docs/cdc` para la fase `Clearing -> CDC -> AP5`
- Ya existe un inventario inicial de `35` funciones CDC en `Clearing.sql`
- Ya existe un primer mapeo CDC de `14` funciones para `Registro`, `Contribucion`, `Mensajes` y `MensajesGeneral`
- La primera tanda CDC ya tiene `14` fichas generadas en `docs/cdc/fichas`
- Ya existe un segundo mapeo CDC de `21` funciones para `Compensacion`, `Productos`, `Personas`, `General`, `ComprobantesGeneral` y `Contabilidad`
- La segunda tanda CDC ya tiene `21` fichas generadas en `docs/cdc/fichas`
- Los esquemas `Mensajes` y `MensajesGeneral` siguen sin evidencia SSIS directa en esta fase
- `Contribucion` requiere una fase posterior especifica por su dependencia probable de mensajeria y otros circuitos

## Siguiente paso sugerido

Profundizar los casos CDC con menor confianza para cerrar consumidor exacto, especialmente `Compensacion` y el circuito Warrant.

Quedan puntos abiertos de ambas tandas:

- `Contribucion.Cuenta`: distinguir si el circuito alimenta principalmente `Contribucion.Cuenta`, `Personas.CuentaRegistroPublicacion` o ambas.
- `Registro.AccionOperacion`: confirmar el consumidor AP5 exacto, porque por ahora quedo como mapeo ambiguo contra el circuito de operaciones de cartera.
- `Compensacion`: confirmar consumidores CDC de bonificaciones, grupo producto y limite de posicion abierta.
- `Productos.ContratoMensajeWarrant`: cerrar si el destino principal es `Activos.ActivoCertificadoDepositoWarrantPublicacion`, mensajes Warrant o ambos.
