# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `ActivoPublicacionFinalidad`
- Esquema destino: `Activos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Activos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Activos.ActivoPublicacionFinalidad` se llena mediante `200_ActivoFinalidad.dtsx`. La evidencia combina `UPDATE` y `OpenRowset`, indicando una carga que puede insertar y ajustar registros ya existentes.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `200_ActivoFinalidad.dtsx` | carga principal | recurrente | paquete numerado y especifico de finalidad por activo |

## Mecanismo tecnico

- Tipo de carga: `update + openrowset`
- Tarea o data flow: carga de finalidad por activo publicado
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `UPDATE [Activos].[ActivoPublicacionFinalidad]`
- Tablas relacionadas: `Activos.ActivoPublicacion`, `Parametros.Finalidad`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| update | `200_ActivoFinalidad.dtsx` | comando SQL | aparece `UPDATE [Activos].[ActivoPublicacionFinalidad]` |
| tabla destino | `200_ActivoFinalidad.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La tabla tiene un paquete dedicado.
- La carga es mas rica que un simple insert.

## Inferencias

- Se trata de un cruce publicado entre activos y finalidades operativas o regulatorias.

## Dudas abiertas

- Si la finalidad proviene directamente del maestro de activos o de un catalogo intermedio en `Clearing`.

## Clasificacion final

- Motivo de clasificacion: paquete especifico con destino explicito.
- Riesgo de error: bajo.
- Proxima validacion sugerida: rastrear el join con `Parametros.Finalidad`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `200_ActivoFinalidad.dtsx`
- Fecha de analisis: `2026-08-11`
