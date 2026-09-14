# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `Accion`
- Esquema destino: `Sistema`
- Clasificacion: `sincronizada`
- Dominio funcional: `Sistema`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Sistema.Accion` se llena desde `010_Sistema.dtsx`, paquete troncal del esquema `Sistema`. La evidencia observada muestra un bloque funcional `Accion` y varios `OpenRowset` apuntando explicitamente a la tabla destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `010_Sistema.dtsx` | carga principal | recurrente | paquete troncal del esquema |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: bloque `Accion`
- Stored procedure: no observado en la evidencia principal
- Tabla destino: `[Sistema].[Accion]`
- Tablas cercanas en el mismo paquete: `Sistema.AccionContribucion`, `Sistema.CadenaAprobacion`, `Sistema.Cargo`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| bloque funcional | `010_Sistema.dtsx` | `Accion` | el paquete identifica explicitamente el subflujo |
| tabla destino | `010_Sistema.dtsx` | componentes destino | `OpenRowset` apunta varias veces a `[Sistema].[Accion]` |

## Hechos observados

- El paquete es activo en `Publicacion.dtproj`.
- `010_Sistema.dtsx` organiza varias tablas maestras del esquema.

## Inferencias

- `Sistema.Accion` parece formar parte del set de catalogos base reutilizados por otros dominios.

## Dudas abiertas

- Si existe actualizacion puntual adicional que no haya quedado expuesta en esta pasada.

## Clasificacion final

- Motivo de clasificacion: destino explicito repetido en el paquete troncal del esquema.
- Riesgo de error: bajo.
- Proxima validacion sugerida: seguir con otras tablas maestras adyacentes como `Cargo` o `CadenaAprobacion`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `010_Sistema.dtsx`
- Fecha de analisis: `2026-08-11`
