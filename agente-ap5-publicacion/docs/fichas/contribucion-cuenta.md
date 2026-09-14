# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `Cuenta`
- Esquema destino: `Contribucion`
- Clasificacion: `sincronizada`
- Dominio funcional: `Contribucion`
- Nivel de confianza: `media`

## Respuesta corta

La tabla `Contribucion.Cuenta` muestra evidencia de mantenimiento desde `Contribucion_Cuenta.dtsx`. En el paquete se observa lectura previa sobre la tabla y un `UPDATE [Contribucion].[Cuenta]`, aunque en esta pasada no quedo visible un `OpenRowset` de destino explicito.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Contribucion_Cuenta.dtsx` | mantenimiento principal | recurrente | paquete activo |

## Mecanismo tecnico

- Tipo de carga: `update`
- Tarea o data flow: `Updates`
- Stored procedure: no observado en la evidencia principal
- SQL relevante: `UPDATE [Contribucion].[Cuenta]`
- Tabla destino: `[Contribucion].[Cuenta]`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| lectura previa | `Contribucion_Cuenta.dtsx` | componentes de consulta | aparecen varias lecturas `FROM [Contribucion].[Cuenta]` |
| update | `Contribucion_Cuenta.dtsx` | `Updates` | aparece `UPDATE [Contribucion].[Cuenta]` |

## Hechos observados

- El paquete es activo en `Publicacion.dtproj`.
- La tabla aparece explicitamente en consultas y update.

## Inferencias

- La carga parece mas de mantenimiento o ajuste puntual que de reconstruccion total.

## Dudas abiertas

- Si existe un flujo de insercion por otra via.
- Si esta tabla se completa en parte por contribuciones y en parte por otro circuito.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita de update sobre la tabla destino.
- Riesgo de error: medio, porque no se observo en esta ficha un `OpenRowset` directo.
- Proxima validacion sugerida: revisar si existe otra variante o un flujo complementario para altas.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Contribucion_Cuenta.dtsx`
- Fecha de analisis: `2026-08-11`
