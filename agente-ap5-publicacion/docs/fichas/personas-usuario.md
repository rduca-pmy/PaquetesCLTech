# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `Usuario`
- Esquema destino: `Personas`
- Clasificacion: `sincronizada`
- Dominio funcional: `Personas`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Personas.Usuario` se llena mediante `Personas_Usuario.dtsx`, paquete que ademas mantiene tablas relacionadas del mismo subdominio como `UsuarioAcciones` y `UsuarioMultiRol`. La evidencia observable incluye borrado puntual por clave, `OpenRowset` al destino y `UPDATE` sobre `Personas.Usuario`.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Personas_Usuario.dtsx` | carga y mantenimiento de usuarios | recurrente | tambien toca `UsuarioAcciones` y `UsuarioMultiRol` |

## Mecanismo tecnico

- Tipo de carga: `delete puntual + insert/update`
- Tarea o data flow: `DELETE Usuarios`, `Inserts & Updates Usuarios`, `Inserts Usuarios Accion`, `Inserts Usuarios MultiRol`
- Stored procedure: no observado en la evidencia principal
- SQL relevante: `delete from [Personas].[Usuario] where UsuarioID = ?`, `UPDATE [Personas].[Usuario]`
- Tablas relacionadas en AP5: `Personas.UsuarioAcciones`, `Personas.UsuarioMultiRol`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| delete puntual | `Personas_Usuario.dtsx` | `DELETE Usuarios` | aparece `delete from [Personas].[Usuario] where UsuarioID = ?` |
| tabla destino | `Personas_Usuario.dtsx` | `Inserts & Updates Usuarios` | `OpenRowset` apunta a `[Personas].[Usuario]` |
| update | `Personas_Usuario.dtsx` | comando SQL de destino | aparece `UPDATE [Personas].[Usuario]` |
| subtabla relacionada | `Personas_Usuario.dtsx` | `Inserts Usuarios Accion` | `OpenRowset` apunta a `[Personas].[UsuarioAcciones]` |
| subtabla relacionada | `Personas_Usuario.dtsx` | `Inserts Usuarios MultiRol` | `OpenRowset` apunta a `[Personas].[UsuarioMultiRol]` |

## Hechos observados

- El paquete tiene conexiones `Clearing` y `Publicacion`.
- La tabla `Usuario` aparece como destino explicito.
- El job modela un subdominio, no solo una tabla aislada.

## Inferencias

- Este paquete probablemente publica la vista operativa de usuarios finales o internos consumida por AP5.

## Dudas abiertas

- Que origen exacto en `Clearing` alimenta usuarios, acciones y multirol.
- Si `UsuarioAcciones` y `UsuarioMultiRol` deben documentarse como fichas separadas o como subfichas del mismo job.

## Clasificacion final

- Motivo de clasificacion: destino explicito con `DELETE`, `OpenRowset` y `UPDATE`.
- Riesgo de error: bajo.
- Proxima validacion sugerida: reconstruir origenes y claves de negocio del paquete.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Personas_Usuario.dtsx`
- Fecha de analisis: `2026-08-10`
