# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `InformacionDeMercado`
- Esquema destino: `MarketData`
- Clasificacion: `sincronizada`
- Dominio funcional: `MarketData`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `MarketData.InformacionDeMercado` se llena mediante varios paquetes SSIS del proyecto `IntegrationServices/Publicacion` que leen desde `Clearing` y publican en `Publicacion`. Para este esquema, la evidencia observada muestra inserts, updates y deletes previos sobre la misma tabla, segun el subtipo de dato de mercado que procesa cada job.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `MarketData_Ajustes.dtsx` | Carga ajustes y variantes proyectadas | recurrente | limpia `TipoEntrada = 'D'` por fecha antes de recargar |
| `MarketData_AjustesRFX20.dtsx` | Carga ajustes RFX20 y proyectados | recurrente | limpia `TipoEntrada = 'D'` y `TipoEntrada = 'P'` |
| `MarketData_AjustesViejo.dtsx` | Variante legacy de ajustes | indeterminada | sigue declarado en `Publicacion.dtproj` |
| `MarketData_ClossingPrices.dtsx` | Carga precios de cierre | recurrente | usa insert y update sobre la tabla |
| `MarketData_CotizacionSpot.dtsx` | Carga cotizaciones spot | recurrente | usa insert y update sobre la tabla |
| `MarketData_InteresAbierto.dtsx` | Carga interes abierto | recurrente | borra `TipoEntrada IN('C')` por fecha antes de insertar |
| `MarketData_SoloAjustes.dtsx` | Carga ajustes con registro de proceso | recurrente | tambien inserta un registro en `General.Proceso` |
| `MarketData_SoloAjustes_SinProceso.dtsx` | Carga ajustes sin registrar proceso | recurrente | variante simplificada del job anterior |

## Mecanismo tecnico

- Tipo de carga: `insert + update + delete previo`, segun paquete
- Tarea o data flow: `Ajustes FCI Inserts & Updates`, `Cotizaciones Spot Inserts & Updates`, `Interes Abierto Inserts` y variantes equivalentes
- Stored procedure: no observado en la evidencia principal del ejemplo
- SQL relevante: `DELETE [MarketData].[InformacionDeMercado] ...`, `UPDATE [MarketData].[InformacionDeMercado] ...`
- Tabla o tablas origen en Clearing: no confirmadas aun a nivel de objeto exacto; si se confirma el uso de la conexion `Clearing`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `MarketData_CotizacionSpot.dtsx` | `INSERT Publicacion` | `OpenRowset` apunta a `[MarketData].[InformacionDeMercado]` |
| update | `MarketData_CotizacionSpot.dtsx` | comando SQL de destino | aparece `UPDATE [MarketData].[InformacionDeMercado]` |
| delete previo | `MarketData_InteresAbierto.dtsx` | `DELETE InformacionDeMercado` | borra `TipoEntrada IN('C')` por fecha antes de insertar |
| insert | `MarketData_InteresAbierto.dtsx` | `Interes Abierto Inserts` | inserta en `[MarketData].[InformacionDeMercado]` |
| delete previo | `MarketData_Ajustes.dtsx` | `Tarea Ejecutar SQL delete TipoEntrada D` | borra `TipoEntrada = 'D'` por fecha |
| delete previo | `MarketData_AjustesRFX20.dtsx` | `Tarea Ejecutar SQL delete TipoEntrada D` y `Tarea Ejecutar SQL delete TipoEntrada P` | limpia datos antes de recarga |
| tabla definida | `Publicacion.sql` | `CREATE TABLE` | el esquema `MarketData` contiene `InformacionDeMercado` |
| consumidor | `Publicacion.sql` | `MarketData.GetDatosDeMercado` | la funcion consulta `FROM MarketData.InformacionDeMercado` |

## Hechos observados

- `Publicacion.sql` define una unica tabla bajo el esquema `MarketData`: `InformacionDeMercado`.
- Los ocho paquetes `MarketData*` estan declarados en `Publicacion.dtproj`.
- Los paquetes relevados usan conexiones `Clearing` y `Publicacion`.
- En varios paquetes se observa `OpenRowset` directo hacia `[MarketData].[InformacionDeMercado]`.
- Tambien se observan comandos `UPDATE` y `DELETE` sobre la misma tabla.

## Inferencias

- `MarketData.InformacionDeMercado` funciona como tabla concentradora para distintos tipos de informacion de mercado publicada en AP5.
- El campo `TipoEntrada` probablemente segmenta subfamilias funcionales de datos como ajustes, interes abierto o datos proyectados.
- `MarketData_AjustesViejo.dtsx` podria ser una variante mantenida por compatibilidad o por historico, aunque sigue declarada en el proyecto.

## Dudas abiertas

- Que objetos exactos de `Clearing` alimentan cada paquete.
- Si todos los paquetes `MarketData*` siguen siendo ejecutados en produccion.
- Como mapear con precision funcional cada valor de `TipoEntrada`.
- Si existen restricciones temporales o particiones logicas complementarias fuera del paquete.

## Clasificacion final

- Motivo de clasificacion: la tabla aparece como destino explicito de varios paquetes que toman datos desde `Clearing` y escriben en `Publicacion`.
- Riesgo de error: bajo para la existencia de sincronizacion; medio para el detalle funcional fino por paquete.
- Proxima validacion sugerida: reconstruir la consulta origen de cada job y relacionarla con objetos de `Clearing.sql`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: paquetes `MarketData*.dtsx` y `Publicacion.sql`
- Fecha de analisis: `2026-08-10`
