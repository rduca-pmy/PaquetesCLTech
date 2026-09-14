# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `MovimientoPublicacionExtension`
- Esquema destino: `Activos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Activos / Movimientos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Activos.MovimientoPublicacionExtension` se llena desde `510_MovimientoPublicacion.dtsx`. La evidencia es un `OpenRowset` directo al destino dentro del mismo job que publica `MovimientoPublicacion`.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `510_MovimientoPublicacion.dtsx` | carga principal | recurrente | paquete troncal de movimientos publicados |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: extension de movimientos publicados
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Activos].[MovimientoPublicacionExtension]`
- Tablas relacionadas: `Activos.MovimientoPublicacion`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `510_MovimientoPublicacion.dtsx` | componente destino | `OpenRowset` apunta a `[Activos].[MovimientoPublicacionExtension]` |

## Hechos observados

- La tabla se carga en el mismo paquete base que la tabla principal de movimientos.
- Su nombre sugiere un bloque de atributos complementarios.

## Inferencias

- Funciona como extension o desnormalizacion de datos para la vista publicada del movimiento.

## Dudas abiertas

- Si comparte clave primaria con `MovimientoPublicacion` o si opera como tabla hija.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita dentro del paquete principal de movimientos.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar el modelo de claves en `Publicacion.sql`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `510_MovimientoPublicacion.dtsx`
- Fecha de analisis: `2026-08-11`
