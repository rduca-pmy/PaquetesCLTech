# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Contribucion_Cuenta_Publicacion`
- Esquema inferido: `Contribucion`
- Objeto inferido: `Cuenta`
- Clasificacion: `mapeo_probable`
- Nivel de confianza: `media`

## Respuesta corta

La funcion CDC publica cambios de `Contribucion.Cuenta` desde PBP. AP5 tiene tabla homonima, pero tambien aparecen procedimientos de insercion de cuenta y una relacion con `Personas.MergeCuentaRegistroPublicacion`; por eso se clasifica como mapeo probable y no como cierre definitivo.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Contribucion_Cuenta_Publicacion` | funcion activa o no validada |
| tabla CT | `cdc.Contribucion_Cuenta_CT` | fuente CDC observada |
| tabla PBP | `Contribucion.Cuenta` | tabla base inferida |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Contribucion.Cuenta` | destino probable | media | tabla homonima en AP5 |
| `Personas.CuentaRegistroPublicacion` | destino relacionado probable | media | aparece `Personas.MergeCuentaRegistroPublicacion` leyendo `Contribucion.Cuenta` |
| `Contribucion.InsertCuenta` | procedimiento relacionado | media | inserta registros en `Contribucion.Cuenta` |
| `Contribucion.InsertCuentas` | procedimiento relacionado | media | insercion masiva o variante |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | lee `cdc.Contribucion_Cuenta_CT` |
| tabla AP5 | `Publicacion.sql` | existe `Contribucion.Cuenta` |
| procedimientos AP5 | `Publicacion.sql` | existen `Contribucion.InsertCuenta`, `Contribucion.InsertCuentas` y `Personas.MergeCuentaRegistroPublicacion` |

## Hechos observados

- No se encontro un `Contribucion.MergeCuenta` simetrico.
- `Contribucion.Cuenta` se cruza con la publicacion de cuentas registro.
- La tabla ya tenia evidencia SSIS parcial por `Contribucion_Cuenta.dtsx`, pero no alcanza para cerrar el circuito CDC completo.

## Inferencias

- La funcion CDC podria alimentar `Contribucion.Cuenta` y, a partir de ahi, participar en la actualizacion de `Personas.CuentaRegistroPublicacion`.

## Dudas abiertas

- Determinar que procedimiento AP5 recibe especificamente el payload de esta funcion CDC.
- Ver si el circuito CDC y el paquete `Contribucion_Cuenta.dtsx` son complementarios o alternativos.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-primer-tanda.csv`, `docs/fichas/contribucion-cuenta.md`
- Fecha de analisis: `2026-08-27`
