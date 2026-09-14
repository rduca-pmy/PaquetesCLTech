# Inventario inicial de paquetes

## Corte del inventario

- Fecha de relevamiento: `2026-08-10`
- Ruta relevada: `IntegrationServices/Publicacion`
- Fuente de proyecto: `Publicacion.dtproj`
- Fuentes logicas complementarias: `Clearing.sql`, `Publicacion.sql`

## Totales iniciales

- Archivos `.dtsx` detectados en carpeta: `137`
- Paquetes declarados en `Publicacion.dtproj`: `120`
- Diferencia observada: `17`

## Interpretacion inicial de la diferencia

- Existen archivos `.dtsx` que no necesariamente integran el proyecto activo.
- Es probable que parte de la diferencia corresponda a variantes duplicadas, pruebas, historicos o paquetes legacy.
- Hasta no revisar caso por caso, esa diferencia debe tratarse como una fuente de ambiguedad del inventario.

## Agrupacion inicial por dominio aparente

| Grupo | Cantidad |
| --- | ---: |
| Numerados | 40 |
| Contribucion | 14 |
| Personas | 12 |
| Registro | 10 |
| Horus | 9 |
| MarketData | 8 |
| Productos | 8 |
| Activos | 6 |
| Compensacion | 5 |
| Comprobantes | 5 |
| Parametros | 2 |
| Rol | 2 |
| Simulacion | 2 |
| CanceladasManuales | 1 |
| Contabilidad | 1 |
| Contrato | 1 |
| DatosIniciales | 1 |
| EndOfDay | 1 |
| General | 1 |
| LibroDeOrdenes | 1 |
| MovimientoPublicacion | 1 |
| Operaciones | 1 |
| Ordenes | 1 |
| Persona | 1 |
| Proceso | 1 |
| StockWatch | 1 |
| Otros | 1 |

## Esquemas detectados en AP5

Segun `Publicacion.sql`, la base `Acsa_Publicacion` expone estos esquemas:

- `Activos`
- `Compensacion`
- `ComprobantesGeneral`
- `Contabilidad`
- `Contribucion`
- `General`
- `MarketData`
- `Mensajes`
- `MensajesGeneral`
- `Parametros`
- `Personas`
- `PersonasGeneral`
- `Productos`
- `Registro`
- `Sistema`

## Esquemas detectados en PBP

Segun `Clearing.sql`, la base `Acsa_Clearing` expone estos esquemas:

- `Activos`
- `cdc`
- `Compensacion`
- `Comprobantes`
- `ComprobantesGeneral`
- `Contabilidad`
- `Contribucion`
- `General`
- `Mensajes`
- `MensajesGeneral`
- `Parametros`
- `Personas`
- `PersonasGeneral`
- `Productos`
- `Registro`
- `registros`
- `Sistema`

## Hallazgos iniciales a documentar

- La organizacion nominal de muchos paquetes coincide con esquemas funcionales presentes en las bases.
- `Publicacion.sql` agrega el esquema `MarketData`, visible tambien en varios paquetes.
- `Clearing.sql` contiene el esquema `cdc`, lo que confirma que el circuito completo debera incluir una fase posterior orientada a CDC.
- La base de datos debe tratarse como fuente principal de logica junto con SSIS, no como mero soporte estructural.

## Criterio operativo a partir de este inventario

1. Priorizar paquetes presentes en `Publicacion.dtproj`.
2. Marcar por separado paquetes no declarados en el proyecto activo.
3. Empezar por dominios con mayor densidad y mejor trazabilidad nominal.
4. Cruce posterior contra objetos reales en `Publicacion.sql` y `Clearing.sql`.

## Paquetes que requieren atencion especial

Estos nombres sugieren posible duplicacion, variante o revision manual:

- `100_SecurityList (2).dtsx`
- `Contribucion_DepositoIvaPublicacion (1).dtsx`
- `Horus_Productos_Ajuste (1).dtsx`
- `Horus_Productos_Ajuste_.dtsx`
- `_100_SecurityList.dtsx`
- `MovimientoPublicacionUpdateTesting.dtsx`
- `030_PersonasGeneralViejo.dtsx`

## Proximo paso recomendado

Construir la matriz inicial `paquete -> tabla destino AP5`, comenzando por paquetes presentes en `Publicacion.dtproj` y con nombre fuertemente alineado a un esquema funcional.
