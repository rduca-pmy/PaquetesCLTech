# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `FondoComunInversionPublicacionTipoPersona`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos / FCI`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.FondoComunInversionPublicacionTipoPersona` se llena mediante `Productos_FondoComunInversionPublicacionTipoPersona.dtsx`, archivo fuera de `dtproj`. La evidencia visible es un `OpenRowset` directo al destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Productos_FondoComunInversionPublicacionTipoPersona.dtsx` | carga principal | recurrente | paquete fuera de `dtproj`, especializado por tipo de persona |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: publicacion FCI por tipo de persona
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Productos].[FondoComunInversionPublicacionTipoPersona]`
- Tablas relacionadas: `Productos.FondoComunInversionPublicacion`, `Productos.Subyacente`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `Productos_FondoComunInversionPublicacionTipoPersona.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- El archivo no esta declarado en el proyecto activo.
- La relacion tecnica con la tabla es directa y clara.

## Inferencias

- Puede tratarse de un complemento operativo para segmentar la publicacion de FCI por clase de cliente.

## Dudas abiertas

- Si el paquete sigue vigente o fue reemplazado por otra implementacion.

## Clasificacion final

- Motivo de clasificacion: destino explicito, con salvedad por estar fuera de `dtproj`.
- Riesgo de error: bajo en la relacion tecnica, medio en la vigencia operativa.
- Proxima validacion sugerida: confirmar despliegue actual de este archivo.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Productos_FondoComunInversionPublicacionTipoPersona.dtsx`
- Fecha de analisis: `2026-08-11`
