# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `ReservaOfertaEntregaPublicacion`
- Esquema destino: `Registro`
- Clasificacion: `sincronizada`
- Dominio funcional: `Registro / Oferta entrega`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Registro.ReservaOfertaEntregaPublicacion` se llena mediante `Registro_ReservaOfertaEntregaPublicacion.dtsx`. La evidencia encontrada es un `OpenRowset` directo al destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Registro_ReservaOfertaEntregaPublicacion.dtsx` | carga principal | recurrente | paquete especifico del subdominio |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: publicacion de reservas de oferta/entrega
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Registro].[ReservaOfertaEntregaPublicacion]`
- Tablas relacionadas: `Registro.AgrupamientoOfertaEntregaPublicacion`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `Registro_ReservaOfertaEntregaPublicacion.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- El paquete es dedicado y claro por nombre.
- La tabla parece ser par funcional del agrupamiento de oferta/entrega.

## Inferencias

- La publicacion modela reservas u asignaciones previas dentro del circuito de entrega.

## Dudas abiertas

- Si la tabla refleja estado vigente, historico o ambos.

## Clasificacion final

- Motivo de clasificacion: paquete especializado con destino explicito.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar relacion de claves con `AgrupamientoOfertaEntregaPublicacion`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Registro_ReservaOfertaEntregaPublicacion.dtsx`
- Fecha de analisis: `2026-08-11`
