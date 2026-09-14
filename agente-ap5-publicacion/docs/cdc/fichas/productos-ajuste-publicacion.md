# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Productos_Ajuste_Publicacion`
- Esquema inferido: `Productos`
- Objeto inferido: `Ajuste`
- Clasificacion: `mapeo_directo`
- Nivel de confianza: `alta`

## Respuesta corta

Publica ajustes de productos desde PBP. AP5 tiene tabla homonima `Productos.Ajuste` y paquetes relacionados.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Productos_Ajuste_Publicacion` | funcion activa o no validada |
| tabla PBP inferida | `Productos.Ajuste` | entidad fuente |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Productos.Ajuste` | destino principal | alta | tabla AP5 homonima |
| `040_Productos.dtsx` | mecanismo relacionado | alta | paquete general de productos |
| `Horus_Productos_Ajuste*.dtsx` | mecanismo relacionado | media | variantes observadas |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe funcion CDC de publicacion |
| tabla AP5 | `Publicacion.sql` | existe `Productos.Ajuste` |
| matriz SSIS | `data/productos-tablas-matriz.csv` | `Ajuste` tiene paquetes asociados |

## Hechos observados

- Tabla homonima y evidencia SSIS previa.

## Inferencias

- CDC puede ser via incremental del mismo dominio cubierto por paquetes.

## Dudas abiertas

- Confirmar prioridad operativa entre CDC y paquetes Horus.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-segunda-tanda.csv`
- Fecha de analisis: `2026-09-11`
