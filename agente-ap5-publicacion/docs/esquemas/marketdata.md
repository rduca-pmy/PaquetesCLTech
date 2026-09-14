# Esquema MarketData

## Objetivo

Documentar un primer ejemplo completo de esquema AP5 y responder, para este caso:

- que tablas tiene el esquema en `Publicacion`
- cuales de esas tablas tienen jobs o paquetes asociados desde PBP
- con que evidencia tecnica se sostiene esa conclusion

## Fuente analizada

- Esquema SQL: `Publicacion.sql`
- Proyecto SSIS: `IntegrationServices/Publicacion/Publicacion.dtproj`
- Paquetes SSIS del dominio:
  - `MarketData_Ajustes.dtsx`
  - `MarketData_AjustesRFX20.dtsx`
  - `MarketData_AjustesViejo.dtsx`
  - `MarketData_ClossingPrices.dtsx`
  - `MarketData_CotizacionSpot.dtsx`
  - `MarketData_InteresAbierto.dtsx`
  - `MarketData_SoloAjustes.dtsx`
  - `MarketData_SoloAjustes_SinProceso.dtsx`

## Tablas detectadas en AP5

Segun `Publicacion.sql`, el esquema `MarketData` contiene una tabla:

| Tabla | Observacion inicial |
| --- | --- |
| `MarketData.InformacionDeMercado` | Tabla central del esquema y punto de convergencia de los paquetes relevados |

## Paquetes activos del proyecto

Los siguientes paquetes figuran declarados en `Publicacion.dtproj`:

| Paquete | Declarado en dtproj | Observacion |
| --- | --- | --- |
| `MarketData_Ajustes.dtsx` | Si | Job activo |
| `MarketData_AjustesRFX20.dtsx` | Si | Job activo |
| `MarketData_AjustesViejo.dtsx` | Si | Variante legacy aun declarada |
| `MarketData_ClossingPrices.dtsx` | Si | Job activo |
| `MarketData_CotizacionSpot.dtsx` | Si | Job activo |
| `MarketData_InteresAbierto.dtsx` | Si | Job activo |
| `MarketData_SoloAjustes.dtsx` | Si | Job activo |
| `MarketData_SoloAjustes_SinProceso.dtsx` | Si | Job activo |

## Conclusion del ejemplo

Para el esquema `MarketData`, la tabla `MarketData.InformacionDeMercado` si tiene jobs asociados desde PBP.

La evidencia observada muestra que los paquetes del dominio:

- leen desde la conexion `Clearing`
- escriben en la conexion `Publicacion`
- usan `OpenRowset` o comandos SQL sobre `[MarketData].[InformacionDeMercado]`
- en varios casos realizan logica de `insert`, `update` y `delete` por `TipoEntrada` y fecha

## Paquetes asociados a la tabla

| Tabla AP5 | Paquete | Tipo de operacion observada |
| --- | --- | --- |
| `MarketData.InformacionDeMercado` | `MarketData_Ajustes.dtsx` | insert, update y delete previo |
| `MarketData.InformacionDeMercado` | `MarketData_AjustesRFX20.dtsx` | insert, update y delete previo |
| `MarketData.InformacionDeMercado` | `MarketData_AjustesViejo.dtsx` | insert y update |
| `MarketData.InformacionDeMercado` | `MarketData_ClossingPrices.dtsx` | insert y update |
| `MarketData.InformacionDeMercado` | `MarketData_CotizacionSpot.dtsx` | insert y update |
| `MarketData.InformacionDeMercado` | `MarketData_InteresAbierto.dtsx` | delete previo e insert |
| `MarketData.InformacionDeMercado` | `MarketData_SoloAjustes.dtsx` | insert y update |
| `MarketData.InformacionDeMercado` | `MarketData_SoloAjustes_SinProceso.dtsx` | insert y update |

## Evidencias representativas

- `Publicacion.sql` define exactamente una tabla en el esquema `MarketData`: `MarketData.InformacionDeMercado`.
- `Publicacion.dtproj` declara los ocho paquetes `MarketData*` como parte del proyecto activo.
- `MarketData_CotizacionSpot.dtsx` contiene `OpenRowset` hacia `[MarketData].[InformacionDeMercado]` y un `UPDATE [MarketData].[InformacionDeMercado]`.
- `MarketData_InteresAbierto.dtsx` ejecuta `DELETE [MarketData].[InformacionDeMercado] WHERE TipoEntrada IN('C')` y luego inserta en la misma tabla.
- `MarketData_Ajustes.dtsx` y `MarketData_AjustesRFX20.dtsx` limpian e insertan filas por variantes de `TipoEntrada` como `D` y `P`.

## Lectura funcional inicial

La tabla `MarketData.InformacionDeMercado` parece operar como tabla concentradora de datos de mercado publicados en AP5, alimentada por varios jobs especializados segun subtipo de informacion:

- ajustes
- ajustes proyectados
- cotizaciones spot
- closing prices
- interes abierto

## Proxima profundizacion sugerida

1. Confirmar para cada paquete cual es la consulta origen exacta sobre `Clearing`.
2. Relacionar cada subtipo de carga con el significado de `TipoEntrada`.
3. Determinar si `MarketData_AjustesViejo.dtsx` sigue vigente funcionalmente o solo permanece declarado.
4. Cruzar la tabla con funciones consumidoras en `Publicacion.sql`, como `MarketData.GetDatosDeMercado`.
