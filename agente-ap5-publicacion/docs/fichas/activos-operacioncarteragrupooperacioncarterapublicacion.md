# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `OperacionCarteraGrupoOperacionCarteraPublicacion`
- Esquema destino: `Activos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Activos / Registro`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Activos.OperacionCarteraGrupoOperacionCarteraPublicacion` se llena mediante `Activos_GrupoOperacionCartera.dtsx`. La evidencia observada es un `OpenRowset` directo al destino, con nombre de paquete y tabla estrechamente relacionados.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Activos_GrupoOperacionCartera.dtsx` | carga principal | recurrente | paquete especifico de relacion entre operacion y grupo |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga de relacion operacion/grupo
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Activos].[OperacionCarteraGrupoOperacionCarteraPublicacion]`
- Tablas relacionadas: `Registro.OperacionCartera*`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `Activos_GrupoOperacionCartera.dtsx` | componente destino | `OpenRowset` apunta a la tabla destino |

## Hechos observados

- El paquete es muy especifico y su nombre casi replica la tabla.
- La relacion paquete-tabla es directa.

## Inferencias

- La tabla modela una asociacion publicada entre operaciones de cartera y grupos operativos.

## Dudas abiertas

- Si el origen funcional proviene de `Clearing` desde una tabla relacional o de una vista armada.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita y paquete especializado.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar el origen en `Clearing.sql` de la relacion de grupos.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Activos_GrupoOperacionCartera.dtsx`
- Fecha de analisis: `2026-08-11`
