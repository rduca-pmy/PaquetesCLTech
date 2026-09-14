# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Compensacion_Margen_Publicacion`
- Esquema inferido: `Compensacion`
- Objeto inferido: `Margen`
- Clasificacion: `mapeo_probable`
- Nivel de confianza: `media`

## Respuesta corta

Publica cambios de margen desde PBP. AP5 no tiene tabla `Compensacion.Margen`, pero si tablas `MargenPublicacion` y `MargenPublicacionHistorico`, por lo que se relaciona con ese circuito.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Compensacion_Margen_Publicacion` | funcion activa o no validada |
| tabla PBP inferida | `Compensacion.Margen` | entidad fuente |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Compensacion.MargenPublicacion` | destino candidato | media | tabla publicada del dominio margen |
| `Compensacion.MargenPublicacionHistorico` | destino candidato | media | cargada por `999_MargenPublicacion*.dtsx` |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe funcion CDC de publicacion |
| tabla AP5 | `Publicacion.sql` | existen `Compensacion.MargenPublicacion` y `Compensacion.MargenPublicacionHistorico` |
| matriz SSIS | `data/compensacion-tablas-matriz.csv` | `MargenPublicacionHistorico` tiene paquetes asociados |

## Hechos observados

- No se encontro `Compensacion.MergeMargen`.
- El destino AP5 usa sufijo `Publicacion`.

## Inferencias

- La funcion CDC probablemente alimenta o dispara la publicacion de margenes.

## Dudas abiertas

- Confirmar si el CDC carga la tabla actual, la historica o ambas.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/compensacion-tablas-matriz.csv`, `data/cdc-mapeo-segunda-tanda.csv`
- Fecha de analisis: `2026-09-11`
