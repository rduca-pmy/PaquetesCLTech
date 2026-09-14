# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Productos_Contrato_Publicacion`
- Esquema inferido: `Productos`
- Objeto inferido: `Contrato`
- Clasificacion: `mapeo_directo`
- Nivel de confianza: `alta`

## Respuesta corta

Publica contratos desde PBP. AP5 tiene tabla homonima `Productos.Contrato` y paquetes relacionados como `040_Productos.dtsx` y `Horus_Productos_Contrato.dtsx`.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Productos_Contrato_Publicacion` | funcion activa o no validada |
| tabla PBP inferida | `Productos.Contrato` | entidad fuente |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Productos.Contrato` | destino principal | alta | tabla AP5 homonima |
| `040_Productos.dtsx` | mecanismo relacionado | alta | paquete general de productos |
| `Horus_Productos_Contrato.dtsx` | mecanismo relacionado | media | paquete especifico observado |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe funcion CDC de publicacion |
| tabla AP5 | `Publicacion.sql` | existe `Productos.Contrato` |
| matriz SSIS | `data/productos-tablas-matriz.csv` | `Contrato` tiene paquetes asociados |

## Hechos observados

- Tabla homonima y evidencia de sincronizacion previa.

## Inferencias

- Es un mapeo directo entre entidad fuente y tabla AP5.

## Dudas abiertas

- Confirmar si el CDC cubre todos los tipos de contrato o solo una variante.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-segunda-tanda.csv`
- Fecha de analisis: `2026-09-11`
