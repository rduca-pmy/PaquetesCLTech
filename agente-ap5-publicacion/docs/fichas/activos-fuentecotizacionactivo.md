# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `FuenteCotizacionActivo`
- Esquema destino: `Activos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Activos / Cotizaciones`
- Nivel de confianza: `media`

## Respuesta corta

La tabla `Activos.FuenteCotizacionActivo` muestra evidencia de carga en `920_Activos.dtsx` y tambien en `Operaciones_CancelacionManual.dtsx`. En ambos casos aparece `OpenRowset` al destino, pero el reparto funcional entre ambos paquetes todavia requiere validacion.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `920_Activos.dtsx` | carga principal probable | recurrente | paquete troncal del maestro de activos |
| `Operaciones_CancelacionManual.dtsx` | actualizacion o consumo especializado | recurrente | paquete de otro dominio que tambien toca la tabla |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga de fuentes de cotizacion
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Activos].[FuenteCotizacionActivo]`
- Tablas relacionadas: `Activos.Activo`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `920_Activos.dtsx` | componente destino | `OpenRowset` apunta a la tabla |
| tabla destino | `Operaciones_CancelacionManual.dtsx` | componente destino o flujo auxiliar | reaparece `OpenRowset` al mismo destino |

## Hechos observados

- La tabla no depende de un solo paquete.
- El paquete troncal de activos parece ser la fuente mas confiable para la carga base.

## Inferencias

- Puede tratarse de un catalogo publicado que luego es reutilizado o ajustado por circuitos operativos.

## Dudas abiertas

- Si `Operaciones_CancelacionManual.dtsx` actualiza realmente la tabla o solo la usa como apoyo tecnico.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita, aunque distribuida en mas de un paquete.
- Riesgo de error: medio.
- Proxima validacion sugerida: inspeccionar el componente exacto dentro de `Operaciones_CancelacionManual.dtsx`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `920_Activos.dtsx`
- Fecha de analisis: `2026-08-11`
