# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `Persona`
- Esquema destino: `PersonasGeneral`
- Clasificacion: `sincronizada`
- Dominio funcional: `PersonasGeneral`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `PersonasGeneral.Persona` se llena mediante `PersonasGeneral_Persona.dtsx`. El paquete muestra `Delete Persona`, varios `OpenRowset` al destino y una logica de insercion apoyada en `PersonaIDPublicacion` y `Get Max PersonaID Publicacion`.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `PersonasGeneral_Persona.dtsx` | carga principal | recurrente | paquete activo y especifico |

## Mecanismo tecnico

- Tipo de carga: `delete + insert/openrowset`
- Tarea o data flow: `Delete Persona`, `Insert`, `Get Max PersonaID Publicacion`
- Stored procedure: no observado en la evidencia principal
- Tabla destino: `[PersonasGeneral].[Persona]`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| delete previo | `PersonasGeneral_Persona.dtsx` | `Delete Persona` | el paquete tiene una tarea nombrada explicitamente |
| tabla destino | `PersonasGeneral_Persona.dtsx` | componente destino | `OpenRowset` apunta a `[PersonasGeneral].[Persona]` |
| logica de identidad | `PersonasGeneral_Persona.dtsx` | `PersonaIDPublicacion` / `Get Max PersonaID Publicacion` | sugiere control de identificador publicado |

## Hechos observados

- La tabla destino aparece explicitamente varias veces.
- El paquete es activo en `dtproj`.

## Inferencias

- La entidad `Persona` parece ser el eje maestro de `PersonasGeneral`.

## Dudas abiertas

- Si el control de `PersonaIDPublicacion` implica una traduccion de claves entre PBP y AP5.

## Clasificacion final

- Motivo de clasificacion: destino explicito con tareas funcionales claras en paquete especifico.
- Riesgo de error: bajo.
- Proxima validacion sugerida: relacionar esta tabla con el esquema `Personas`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `PersonasGeneral_Persona.dtsx`
- Fecha de analisis: `2026-08-11`
