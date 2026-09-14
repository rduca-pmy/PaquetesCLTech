# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `Finalidad`
- Esquema destino: `Parametros`
- Clasificacion: `sincronizada`
- Dominio funcional: `Parametros`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Parametros.Finalidad` se llena desde `015_Parametros.dtsx`. En la evidencia relevada aparecen `OpenRowset` al destino, varias lecturas sobre la tabla y un `UPDATE [Parametros].[Finalidad]`.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `015_Parametros.dtsx` | carga principal | recurrente | paquete activo y troncal del esquema |

## Mecanismo tecnico

- Tipo de carga: `openrowset + update`
- Tarea o data flow: bloque `Finalidad`
- Stored procedure: no observado en la evidencia principal
- SQL relevante: `UPDATE [Parametros].[Finalidad]`
- Tabla destino: `[Parametros].[Finalidad]`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| bloque funcional | `015_Parametros.dtsx` | `Finalidad` | el paquete tiene un bloque identificado por nombre |
| tabla destino | `015_Parametros.dtsx` | componente destino | `OpenRowset` apunta a `[Parametros].[Finalidad]` |
| update | `015_Parametros.dtsx` | comando SQL | aparece `UPDATE [Parametros].[Finalidad]` |

## Hechos observados

- El paquete es activo en `Publicacion.dtproj`.
- La tabla aparece varias veces dentro del bloque funcional.

## Inferencias

- `Parametros.Finalidad` es un catalogo publicado desde PBP para consumo transversal en AP5.

## Dudas abiertas

- Si existe limpieza previa no visible en esta pasada.

## Clasificacion final

- Motivo de clasificacion: destino explicito con update en paquete troncal del esquema.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar otras tablas catalogo del mismo paquete.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `015_Parametros.dtsx`
- Fecha de analisis: `2026-08-11`
