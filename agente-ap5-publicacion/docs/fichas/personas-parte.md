# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `Parte`
- Esquema destino: `Personas`
- Clasificacion: `sincronizada`
- Dominio funcional: `Personas`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Personas.Parte` se llena mediante `990_PersonasParte.dtsx`, un paquete especializado que reutiliza la misma tabla destino para distintas familias de parte. La evidencia observable muestra multiples bloques de `DELETE` e `INSERT` sobre `OpenRowset` a `Personas.Parte`.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `990_PersonasParte.dtsx` | carga especializada de partes | recurrente | procesa varias clases de parte dentro del mismo job |

## Mecanismo tecnico

- Tipo de carga: `delete + insert`
- Tarea o data flow: bloques como `Cuenta de Negociacion`, `Cuenta de Neteo`, `Cuenta de Registro`, `Cuenta MAV`, `Miembro Compensador`, `Participante`, `Participante ACVN`, `Participante DMA`
- Stored procedure: no observado en la evidencia principal
- SQL relevante: tareas de `DELETE *` seguidas de `INSERT *` por subtipo funcional
- Tabla destino: `OpenRowset` repetido hacia `[Personas].[Parte]`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `990_PersonasParte.dtsx` | multiples componentes `INSERT *` | `OpenRowset` apunta reiteradamente a `[Personas].[Parte]` |
| bloques funcionales | `990_PersonasParte.dtsx` | `Cuenta de Negociacion`, `Cuenta de Neteo`, `Cuenta de Registro`, `Cuenta MAV`, `Miembro Compensador`, `Participante` y variantes | el paquete segmenta la carga por tipo de parte |

## Hechos observados

- El paquete es especifico y activo.
- La misma tabla destino se usa en varios subflujos dentro del job.
- La estructura sugiere una tabla polimorfica o consolidada de partes.

## Inferencias

- `Personas.Parte` parece ser una tabla concentradora de diferentes entidades homologadas como "parte" para consumo de AP5.

## Dudas abiertas

- Que claves de tipificacion diferencian internamente cada subtipo de parte.
- Si existe una tabla maestra de tipos o clasificaciones complementaria.

## Clasificacion final

- Motivo de clasificacion: destino explicito y repetido en un paquete especializado.
- Riesgo de error: bajo.
- Proxima validacion sugerida: identificar el atributo que distingue subtipos dentro de `Parte`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `990_PersonasParte.dtsx`
- Fecha de analisis: `2026-08-10`
