# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `MovimientoCustodiaNoProcesadoPublicacion`
- Esquema destino: `Activos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Activos / Custodia`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Activos.MovimientoCustodiaNoProcesadoPublicacion` se llena mediante `Activos_MovimientoCustodiaNoProcesadoPublicacion.dtsx`, archivo hoy fuera de `dtproj`. La evidencia encontrada es un `OpenRowset` directo al destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Activos_MovimientoCustodiaNoProcesadoPublicacion.dtsx` | carga principal | recurrente | paquete fuera de `dtproj`, pero explicitamente ligado a la tabla |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: publicacion de movimientos de custodia no procesados
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Activos].[MovimientoCustodiaNoProcesadoPublicacion]`
- Tablas relacionadas: `Activos.MovimientoPublicacion`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `Activos_MovimientoCustodiaNoProcesadoPublicacion.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- El archivo no esta declarado en el proyecto activo.
- La relacion tecnica con la tabla es explicita.

## Inferencias

- La tabla cubre un circuito de excepcion o pendiente de proceso dentro de custodia.

## Dudas abiertas

- Si el paquete sigue vigente o fue absorbido por otra implementacion.

## Clasificacion final

- Motivo de clasificacion: destino explicito, con advertencia por estar fuera de `dtproj`.
- Riesgo de error: bajo en la relacion tecnica, medio en la vigencia operativa.
- Proxima validacion sugerida: confirmar si existe reemplazo dentro del proyecto actual.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Activos_MovimientoCustodiaNoProcesadoPublicacion.dtsx`
- Fecha de analisis: `2026-08-11`
