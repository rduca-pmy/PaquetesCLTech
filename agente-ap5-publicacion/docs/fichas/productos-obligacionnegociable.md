# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `ObligacionNegociable`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.ObligacionNegociable` se llena mediante `040_Productos.dtsx`. La evidencia visible es un `OpenRowset` directo al destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `040_Productos.dtsx` | carga principal | recurrente | paquete troncal del esquema |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga general de productos
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Productos].[ObligacionNegociable]`
- Tablas relacionadas: `Productos.Titulo`, `Productos.Contrato`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `040_Productos.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La tabla se carga en el mismo lote que otros instrumentos.
- No se detectaron paquetes alternativos.

## Inferencias

- Se publica como subtipo especifico del universo de titulos o contratos.

## Dudas abiertas

- Si existe enriquecimiento posterior fuera del flujo SSIS observado.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita en paquete troncal.
- Riesgo de error: bajo.
- Proxima validacion sugerida: mapear su relacion exacta con `Titulo`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `040_Productos.dtsx`
- Fecha de analisis: `2026-08-11`
