# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Contribucion_MargenEntrega_Publicacion`
- Esquema inferido: `Contribucion`
- Objeto inferido: `MargenEntrega`
- Clasificacion: `mapeo_probable`
- Nivel de confianza: `media`

## Respuesta corta

La funcion CDC arma informacion de margen de entrega desde PBP y la relaciona con cuentas, grupos, productos, contratos y operaciones. AP5 tiene `Contribucion.MargenEntrega` y un paquete SSIS asociado, pero no se encontro un `MergeMargenEntrega` claro en esta pasada.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Contribucion_MargenEntrega_Publicacion` | funcion activa o no validada |
| tabla PBP | `Contribucion.MargenEntrega` | tabla base inferida |
| tabla AP5 candidata | `Contribucion.MargenEntrega` | tabla homonima en `Publicacion.sql` |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Contribucion.MargenEntrega` | destino probable | media | tabla homonima en AP5 |
| `Contribucion_MargenEntrega.dtsx` | mecanismo SSIS relacionado | media | paquete ya detectado como cargador de la tabla |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe `cdc.fn_cdc_get_Contribucion_MargenEntrega_Publicacion` |
| enriquecimiento | `Clearing.sql` | usa cuentas, `Compensacion.GrupoEscenario`, `Compensacion.GrupoProducto`, contratos y operaciones |
| tabla AP5 | `Publicacion.sql` | existe `Contribucion.MargenEntrega` |
| evidencia SSIS | `data/contribucion-tablas-matriz.csv` | `Contribucion_MargenEntrega.dtsx` toca la tabla |

## Hechos observados

- Hay tabla homonima en AP5.
- Tambien hay paquete SSIS relacionado con la misma tabla.
- No se encontro receptor `Merge*` especifico en `Publicacion.sql`.

## Inferencias

- CDC podria ser origen incremental o disparador de cambios, mientras que SSIS podria recomponer o actualizar la tabla publicada.

## Dudas abiertas

- Confirmar si el paquete SSIS consume datos derivados de CDC.
- Buscar un receptor de payload que no use prefijo `Merge`.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-primer-tanda.csv`, `data/contribucion-tablas-matriz.csv`
- Fecha de analisis: `2026-08-27`
