# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Personas_CuentaRegistroGrupoProductoCancelacion_Publicacion`
- Esquema inferido: `Personas`
- Objeto inferido: `CuentaRegistroGrupoProductoCancelacion`
- Clasificacion: `mapeo_directo`
- Nivel de confianza: `alta`

## Respuesta corta

Publica la relacion entre cuenta registro y grupo producto de cancelacion. AP5 tiene tabla homonima y ademas la usa como insumo de `CuentaRegistroPublicacion`.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Personas_CuentaRegistroGrupoProductoCancelacion_Publicacion` | funcion activa o no validada |
| tabla PBP inferida | `Personas.CuentaRegistroGrupoProductoCancelacion` | entidad fuente |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Personas.CuentaRegistroGrupoProductoCancelacion` | destino principal | alta | tabla AP5 homonima |
| `Personas.CuentaRegistroPublicacion` | destino relacionado | media | el paquete consulta esta tabla para enriquecer la publicacion |
| `031_CuentaRegistroPublicacion.dtsx` | mecanismo relacionado | media | referencia la tabla como insumo |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe funcion CDC de publicacion |
| tabla AP5 | `Publicacion.sql` | existe `Personas.CuentaRegistroGrupoProductoCancelacion` |
| paquete AP5 | `IntegrationServices/Publicacion/031_CuentaRegistroPublicacion.dtsx` | referencia la tabla como fuente auxiliar |

## Hechos observados

- La matriz SSIS previa no tenia carga directa para esta tabla.
- CDC explica una posible via de sincronizacion.

## Inferencias

- Es un buen ejemplo de tabla AP5 sin evidencia SSIS directa que podria llenarse por CDC.

## Dudas abiertas

- Confirmar si la tabla se actualiza exclusivamente por CDC.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/personas-tablas-matriz.csv`, `data/cdc-mapeo-segunda-tanda.csv`
- Fecha de analisis: `2026-09-11`
