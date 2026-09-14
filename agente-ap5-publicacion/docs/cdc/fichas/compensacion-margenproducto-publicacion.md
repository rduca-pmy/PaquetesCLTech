# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Compensacion_MargenProducto_Publicacion`
- Esquema inferido: `Compensacion`
- Objeto inferido: `MargenProducto`
- Clasificacion: `mapeo_probable`
- Nivel de confianza: `media`

## Respuesta corta

Publica margenes por producto desde PBP. AP5 no conserva el nombre exacto, pero tiene tablas de margen por grupo/producto y margenes por contrato.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Compensacion_MargenProducto_Publicacion` | funcion activa o no validada |
| tabla PBP inferida | `Compensacion.MargenProducto` | entidad fuente |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Compensacion.MargenDetalleGrupoProducto` | destino candidato | media | detalle de margen por grupo/producto |
| `Compensacion.MargenesContrato` | destino relacionado | media | tabla AP5 de margenes por contrato |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe funcion CDC de publicacion |
| matriz SSIS | `data/compensacion-tablas-matriz.csv` | existen paquetes para `MargenDetalleGrupoProducto` y `MargenesContrato` |

## Hechos observados

- No existe tabla AP5 `Compensacion.MargenProducto`.
- Hay destinos AP5 cercanos por dominio.

## Inferencias

- La funcion CDC podria alimentar la granularidad de margen que AP5 materializa con otro nombre.

## Dudas abiertas

- Validar si el consumidor final es margen por contrato o detalle por grupo/producto.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-segunda-tanda.csv`
- Fecha de analisis: `2026-09-11`
