# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `AgrupamientoOfertaEntregaPublicacion`
- Esquema destino: `Registro`
- Clasificacion: `sincronizada`
- Dominio funcional: `Registro / Oferta entrega`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Registro.AgrupamientoOfertaEntregaPublicacion` se llena mediante `Registro_AgrupamientoOfertaEntregaPublicacion.dtsx`. La evidencia relevada es un `OpenRowset` directo al destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Registro_AgrupamientoOfertaEntregaPublicacion.dtsx` | carga principal | recurrente | paquete especifico del subdominio |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: publicacion de agrupamientos de oferta/entrega
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Registro].[AgrupamientoOfertaEntregaPublicacion]`
- Tablas relacionadas: `Registro.ReservaOfertaEntregaPublicacion`, `Activos.Activo`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `Registro_AgrupamientoOfertaEntregaPublicacion.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- El paquete es dedicado y casi replica el nombre de la tabla.
- Tambien aparece `Activos.Activo` relacionado en la matriz general.

## Inferencias

- La tabla consolida agrupamientos visibles en AP5 para circuitos de oferta/entrega.

## Dudas abiertas

- Si existe dependencia con estados operativos o asignaciones posteriores.

## Clasificacion final

- Motivo de clasificacion: paquete especializado con destino explicito.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar su relacion con `ReservaOfertaEntregaPublicacion`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Registro_AgrupamientoOfertaEntregaPublicacion.dtsx`
- Fecha de analisis: `2026-08-11`
