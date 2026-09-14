# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `ValoresOTCAgro`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos / OTC Agro`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.ValoresOTCAgro` se llena mediante `Productos_ValoresOTCAgro.dtsx`. La evidencia encontrada es un `OpenRowset` directo sobre la tabla destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Productos_ValoresOTCAgro.dtsx` | carga principal | recurrente | paquete especifico del subdominio OTC Agro |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga de valores OTC Agro
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Productos].[ValoresOTCAgro]`
- Tablas relacionadas: `Productos.ForwardOTC`, `Productos.Puerto`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `Productos_ValoresOTCAgro.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La tabla tiene un job dedicado.
- El nombre del paquete es consistente con el subtipo funcional.

## Inferencias

- Se publica como catalogo o estructura especifica del circuito OTC Agro.

## Dudas abiertas

- Si depende de maestros genericos de productos o de tablas de contribucion propias.

## Clasificacion final

- Motivo de clasificacion: paquete especializado con destino explicito.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar su relacion con contratos OTC del esquema.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Productos_ValoresOTCAgro.dtsx`
- Fecha de analisis: `2026-08-11`
