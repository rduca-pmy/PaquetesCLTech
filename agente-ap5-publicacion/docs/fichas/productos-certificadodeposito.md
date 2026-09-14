# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `CertificadoDeposito`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.CertificadoDeposito` se llena mediante `040_Productos.dtsx`. La evidencia observada es un `OpenRowset` directo al destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `040_Productos.dtsx` | carga principal | recurrente | paquete troncal del esquema |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga de tipos de producto
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Productos].[CertificadoDeposito]`
- Tablas relacionadas: `Productos.Producto`, `Productos.Contrato`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `040_Productos.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La tabla aparece dentro del set general de subtipos del paquete `040`.
- No se observaron paquetes especializados adicionales.

## Inferencias

- Se publica como subtipo del universo de instrumentos/contratos de AP5.

## Dudas abiertas

- Si esta tabla se complementa funcionalmente con tablas del esquema `Activos`.

## Clasificacion final

- Motivo de clasificacion: destino explicito en paquete maestro.
- Riesgo de error: bajo.
- Proxima validacion sugerida: contrastar con `Activos.ActivoCertificadoDepositoWarrantPublicacion`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `040_Productos.dtsx`
- Fecha de analisis: `2026-08-11`
