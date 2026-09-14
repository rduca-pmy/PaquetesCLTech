# Esquema Productos

## Resumen

- Tablas en `Publicacion.sql`: `44`
- Tablas con evidencia en SSIS: `38`
- Tablas sin evidencia en SSIS: `6`

## Lectura inicial

Esquema muy grande y con cobertura alta. Se apoya tanto en paquetes propios (`040_Productos`, `Productos_*`) como en jobs de `SecurityList`, `Horus`, `MarketData` y otros dominios que reutilizan productos.

## Paquetes relevantes

- `040_Productos.dtsx`
- `100_SecurityList*.dtsx`
- `Horus_Productos_*.dtsx`
- `Productos_ContratoAFijarPublicacion.dtsx`
- `Productos_FondoComunInversion.dtsx`
- `Productos_FondoComunInversionPublicacion.dtsx`
- `Productos_InstrumentoDigital.dtsx`
- `Productos_TarifaDevengada.dtsx`
- `Productos_TarifaPublicacion.dtsx`
- `Productos_ValoresOTCAgro.dtsx`

## Paquetes fuera de `dtproj`

- `Horus_Productos_Ajuste (1).dtsx`
- `Horus_Productos_Ajuste_.dtsx`
- `Horus_VolatilidadImplicitaOperada.dtsx`
- `Productos_FondoComunInversionPublicacionTipoPersona.dtsx`

## Matriz inicial de tablas

| Tabla | Paquete o paquetes principales | Evidencia observada |
| --- | --- | --- |
| `Productos.Ajuste` | `040_Productos.dtsx`, `Horus_Productos_Ajuste*` | `DELETE`, `UPDATE`, `OpenRowset` |
| `Productos.ContratoLicitacionEspecie` | `991_Licitacion.dtsx` | `DELETE`, `UPDATE`, `OpenRowset` |
| `Productos.Licitacion` | `991_Licitacion.dtsx` | `DELETE`, `UPDATE`, `OpenRowset` |
| `Productos.Subyacente` | `040_Productos.dtsx` y paquetes FCI | `OpenRowset` |
| `Productos.Contrato` | `040_Productos.dtsx`, `Horus_Productos_Contrato.dtsx` | `UPDATE`, `OpenRowset` |
| `Productos.Disponible` | `040_Productos.dtsx` | `UPDATE`, `OpenRowset` |
| `Productos.Futuro` | `040_Productos.dtsx` | `UPDATE`, `OpenRowset` |
| `Productos.Forward` | `040_Productos.dtsx` | `DELETE`, `UPDATE`, `OpenRowset` |
| `Productos.ForwardOTC` | `040_Productos.dtsx` | `DELETE`, `UPDATE`, `OpenRowset` |
| `Productos.Opcion` | `040_Productos.dtsx` | `UPDATE`, `OpenRowset` |
| `Productos.OpcionOTC` | `040_Productos.dtsx` | `UPDATE`, `OpenRowset` |
| `Productos.ContratoAFijarPublicacion` | `Productos_ContratoAFijarPublicacion.dtsx` | `UPDATE`, `OpenRowset` |
| `Productos.FondoComunInversionPublicacion` | `Productos_FondoComunInversionPublicacion.dtsx` | `UPDATE`, `OpenRowset` |
| `Productos.FondoComunInversionPublicacionTipoPersona` | `Productos_FondoComunInversionPublicacionTipoPersona.dtsx` | `OpenRowset` |
| `Productos.ListaContrato` | `100_SecurityList*.dtsx`, `_100_SecurityList.dtsx` | `OpenRowset` |
| `Productos.ListaContratoCombinado` | `100_SecurityList*.dtsx`, `_100_SecurityList.dtsx` | `OpenRowset` |
| `Productos.Valuacion` | `040_Productos.dtsx` | `DELETE`, `OpenRowset` |
| `Productos.ConversionContrato` | `090_ConversionContrato.dtsx` | `UPDATE`, `OpenRowset` |
| `Productos.InstrumentoDigital` | `Productos_InstrumentoDigital.dtsx` | `UPDATE`, `OpenRowset` |
| `Productos.TarifaDevengada` | `Productos_TarifaDevengada.dtsx` | `OpenRowset` |
| `Productos.TarifaDevengadaStage` | `Productos_TarifaDevengada.dtsx` | `OpenRowset` |
| `Productos.TarifaPublicacion` | `Productos_TarifaPublicacion.dtsx` | `OpenRowset` |
| `Productos.ValoresOTCAgro` | `Productos_ValoresOTCAgro.dtsx` | `OpenRowset` |
| `Productos.AdministracionNotificacion` | `Parametros_NotificacionAdministracion.dtsx` | `OpenRowset` |
| `Productos.NotificacionProductos` | `Parametros_NotificacionAdministracion.dtsx` | `OpenRowset` |
| `Productos.NotificacionCanales` | `Parametros_NotificacionAdministracion.dtsx` | `OpenRowset` |

## Tablas sin evidencia observada

- `Productos.SerieRentaFijaPublicacion`
- `Productos.SerieRentaVariablePublicacion`
- `Productos.ReposCategoriaAforo`
- `Productos.Emision`
- `Productos.CategoriaSerie`
- `Productos.ProductoWarrant`

## Nota

`Productos` es otro gran candidato a profundizacion posterior, porque articula muchos circuitos del modelo.

## Artefactos de soporte

- [productos-tablas-matriz.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/productos-tablas-matriz.csv)
- [productos-paquete-tabla-matriz.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/productos-paquete-tabla-matriz.csv)
