# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Compensacion_ParametroContrato_Publicacion`
- Esquema inferido: `Compensacion`
- Objeto inferido: `ParametroContrato`
- Clasificacion: `mapeo_directo`
- Nivel de confianza: `alta`

## Respuesta corta

Publica parametros de contrato desde PBP. AP5 los materializa como `Compensacion.ParametroContratoPublicacion`, con paquete especifico ya relevado.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Compensacion_ParametroContrato_Publicacion` | funcion activa o no validada |
| tabla PBP inferida | `Compensacion.ParametroContrato` | entidad fuente |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Compensacion.ParametroContratoPublicacion` | destino principal | alta | tabla AP5 con sufijo `Publicacion` |
| `Compensacion_ParametroContratoPublicacion.dtsx` | mecanismo relacionado | alta | paquete especifico |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe funcion CDC de publicacion |
| tabla AP5 | `Publicacion.sql` | existe `Compensacion.ParametroContratoPublicacion` |
| matriz SSIS | `data/compensacion-tablas-matriz.csv` | paquete `Compensacion_ParametroContratoPublicacion.dtsx` |

## Hechos observados

- El nombre de AP5 agrega sufijo `Publicacion`.
- La relacion es directa por dominio y por tabla destino.

## Inferencias

- CDC y paquete podrian ser caminos complementarios o historicos para mantener la misma entidad publicada.

## Dudas abiertas

- Determinar si el consumidor CDC reemplaza o convive con el paquete.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/compensacion-tablas-matriz.csv`, `data/cdc-mapeo-segunda-tanda.csv`
- Fecha de analisis: `2026-09-11`
