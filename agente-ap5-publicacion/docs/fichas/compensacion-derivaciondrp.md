# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `DerivacionDRP`
- Esquema destino: `Compensacion`
- Clasificacion: `sincronizada`
- Dominio funcional: `Compensacion`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Compensacion.DerivacionDRP` se llena mediante `Compensacion_DerivacionDRP.dtsx`. En el paquete se observan varios bloques de `Insert & Update` que apuntan explicitamente a la misma tabla por `OpenRowset`, incluyendo flujos diferenciados para AP5 y Clearing.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Compensacion_DerivacionDRP.dtsx` | carga principal | recurrente | paquete activo y especifico |

## Mecanismo tecnico

- Tipo de carga: `openrowset` con logica de insert/update
- Tarea o data flow: `Insert & Update`, `Insert & Update CL to AP5`, `Insert & Update Cl to Cl`
- Stored procedure: no observado en la evidencia principal
- SQL relevante: lectura previa `select * from [Compensacion].[DerivacionDRP]`
- Tabla destino: `[Compensacion].[DerivacionDRP]`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `Compensacion_DerivacionDRP.dtsx` | `Insert & Update` | `OpenRowset` apunta a `[Compensacion].[DerivacionDRP]` |
| tabla destino | `Compensacion_DerivacionDRP.dtsx` | `Insert & Update CL to AP5` | `OpenRowset` apunta a `[Compensacion].[DerivacionDRP]` |
| tabla destino | `Compensacion_DerivacionDRP.dtsx` | `Insert & Update Cl to Cl` | `OpenRowset` apunta a `[Compensacion].[DerivacionDRP]` |

## Hechos observados

- El paquete es activo en `Publicacion.dtproj`.
- La tabla aparece varias veces como destino explicito.
- Hay una lectura previa de la misma tabla para comparacion o merge logico.

## Inferencias

- El paquete parece mantener distintas vistas o etapas de derivacion dentro del mismo circuito.

## Dudas abiertas

- Si existen filtros por fecha o limpieza previa no capturada en esta ficha.
- Que diferencia funcional exacta existe entre los tres subflujos observados.

## Clasificacion final

- Motivo de clasificacion: destino explicito y repetido en paquete especifico.
- Riesgo de error: bajo.
- Proxima validacion sugerida: reconstruir el origen en `Clearing` y el significado de cada subflujo.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Compensacion_DerivacionDRP.dtsx`
- Fecha de analisis: `2026-08-11`
