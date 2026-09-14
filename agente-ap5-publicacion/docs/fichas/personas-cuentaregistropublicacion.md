# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `CuentaRegistroPublicacion`
- Esquema destino: `Personas`
- Clasificacion: `sincronizada`
- Dominio funcional: `Personas`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Personas.CuentaRegistroPublicacion` se alimenta desde los paquetes generalistas `030_PersonasGeneral*` y tambien desde el paquete especifico `031_CuentaRegistroPublicacion.dtsx`. En la evidencia relevada, la tabla aparece como destino explicito por `OpenRowset`.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `030_PersonasGeneral.dtsx` | carga generalista | recurrente | comparte dominio con muchas tablas Personas |
| `030_PersonasGeneralLight.dtsx` | variante light | recurrente | probable ejecucion parcial o acotada |
| `030_PersonasGeneralViejo.dtsx` | variante legacy | indeterminada | aun activa en `dtproj` |
| `031_CuentaRegistroPublicacion.dtsx` | carga especifica | recurrente | foco exclusivo en la entidad |

## Mecanismo tecnico

- Tipo de carga: `insert/update observado por destino explicito`
- Tarea o data flow: flujos de `CuentaRegistroPublicacion` y tablas relacionadas
- Stored procedure: no observado en la evidencia principal
- SQL relevante: destino observado como `[Personas].[CuentaRegistroPublicacion]`
- Tabla relacionada: `Personas.CuentaRegistroEntidadBursatil`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `030_PersonasGeneral.dtsx` | componente destino | `OpenRowset` apunta a `[Personas].[CuentaRegistroPublicacion]` |
| tabla destino | `030_PersonasGeneralLight.dtsx` | componente destino | `OpenRowset` apunta a `[Personas].[CuentaRegistroPublicacion]` |
| tabla destino | `030_PersonasGeneralViejo.dtsx` | componente destino | `OpenRowset` apunta a `[Personas].[CuentaRegistroPublicacion]` |
| tabla destino | `031_CuentaRegistroPublicacion.dtsx` | componente destino | `OpenRowset` apunta a `[Personas].[CuentaRegistroPublicacion]` |

## Hechos observados

- La tabla aparece en varios paquetes activos.
- Existe un job especifico ademas del job generalista.
- La tabla parece estar cerca del nucleo relacional de cuentas y entidades bursatiles.

## Inferencias

- Este es un buen candidato para una siguiente fase de reconstruccion end-to-end, porque parece actuar como tabla de publicacion clave para cuentas de registro.

## Dudas abiertas

- Como se reparten funcionalmente `030_PersonasGeneral*` y `031_CuentaRegistroPublicacion.dtsx`.
- Si el job especifico complementa o reemplaza una parte del generalista.

## Clasificacion final

- Motivo de clasificacion: destino explicito repetido en paquetes activos, incluyendo uno especifico.
- Riesgo de error: bajo.
- Proxima validacion sugerida: comparar las consultas origen de `030_*` y `031_*`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `030_PersonasGeneral*.dtsx`, `031_CuentaRegistroPublicacion.dtsx`
- Fecha de analisis: `2026-08-10`
