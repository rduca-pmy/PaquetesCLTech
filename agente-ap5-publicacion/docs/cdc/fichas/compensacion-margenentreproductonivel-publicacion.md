# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Compensacion_MargenEntreProductoNivel_Publicacion`
- Esquema inferido: `Compensacion`
- Objeto inferido: `MargenEntreProductoNivel`
- Clasificacion: `mapeo_probable`
- Nivel de confianza: `media`

## Respuesta corta

Publica reglas o valores de margen entre productos por nivel. AP5 no tiene tabla homonima, pero el candidato mas cercano es `Compensacion.MargenDetalleGrupoProducto`.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Compensacion_MargenEntreProductoNivel_Publicacion` | funcion activa o no validada |
| tabla PBP inferida | `Compensacion.MargenEntreProductoNivel` | entidad fuente |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Compensacion.MargenDetalleGrupoProducto` | destino candidato | media | tabla AP5 de detalle de margen por grupo/producto |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe funcion CDC de publicacion |
| matriz SSIS | `data/compensacion-tablas-matriz.csv` | `MargenDetalleGrupoProducto` se carga por `Compensacion_MargenDetalleGrupoProducto.dtsx` |

## Hechos observados

- No existe tabla AP5 `MargenEntreProductoNivel`.
- Existe tabla AP5 de detalle por grupo/producto.

## Inferencias

- El objeto CDC podria alimentar un detalle ya transformado para AP5.

## Dudas abiertas

- Validar columnas para confirmar equivalencia entre nivel PBP y detalle AP5.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-segunda-tanda.csv`
- Fecha de analisis: `2026-09-11`
