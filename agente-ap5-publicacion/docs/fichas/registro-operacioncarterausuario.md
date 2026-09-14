# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `OperacionCarteraUsuario`
- Esquema destino: `Registro`
- Clasificacion: `sincronizada`
- Dominio funcional: `Registro / Operaciones`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Registro.OperacionCarteraUsuario` se llena mediante `Registro_OperacionCarteraUsuario.dtsx`. La evidencia encontrada es un `OpenRowset` directo a la tabla destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Registro_OperacionCarteraUsuario.dtsx` | carga principal | recurrente | paquete especifico de relacion operacion/usuario |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga de usuarios asociados a operaciones de cartera
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Registro].[OperacionCarteraUsuario]`
- Tablas relacionadas: `Personas.Usuario`, `Registro.OperacionCarteraExtension`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `Registro_OperacionCarteraUsuario.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- El paquete es exclusivo de esta relacion.
- La tabla vincula claramente operaciones con usuarios publicados en AP5.

## Inferencias

- Se trata de una tabla de cruce para trazabilidad operativa o visualizacion de responsables.

## Dudas abiertas

- Si la asociacion refleja usuario creador, operador, aprobador u otros roles.

## Clasificacion final

- Motivo de clasificacion: paquete especializado con destino explicito.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar las columnas de rol de usuario en la tabla.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Registro_OperacionCarteraUsuario.dtsx`
- Fecha de analisis: `2026-08-11`
