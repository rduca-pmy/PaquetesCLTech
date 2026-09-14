# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Compensacion_GrupoProducto_Publicacion`
- Esquema inferido: `Compensacion`
- Objeto inferido: `GrupoProducto`
- Clasificacion: `mapeo_ambiguo`
- Nivel de confianza: `baja`

## Respuesta corta

La funcion publica cambios de grupos de producto desde PBP, pero AP5 no tiene tabla `Compensacion.GrupoProducto`. El dato aparece como atributo descriptivo en circuitos de productos y listas de contratos.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Compensacion_GrupoProducto_Publicacion` | funcion activa o no validada |
| tabla PBP inferida | `Compensacion.GrupoProducto` | entidad fuente |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Productos.Contrato` | dominio relacionado | baja | usa descripcion de grupo producto en circuitos de productos |
| `Productos.ListaContrato` | dominio relacionado | baja | aparece en `_100_SecurityList.dtsx` |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe funcion CDC de publicacion |
| paquete AP5 | `IntegrationServices/Publicacion/_100_SecurityList.dtsx` | referencias a `GrupoProductoDescripcion` |

## Hechos observados

- No existe tabla AP5 `Compensacion.GrupoProducto`.
- El dato se observa como atributo enriquecedor en contratos.

## Inferencias

- El CDC podria mantener una dimension fuente usada para enriquecer productos, no una tabla AP5 propia.

## Dudas abiertas

- Confirmar si se materializa en alguna tabla auxiliar no homonima antes de llegar a `Productos`.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `IntegrationServices/Publicacion`, `data/cdc-mapeo-segunda-tanda.csv`
- Fecha de analisis: `2026-09-11`
