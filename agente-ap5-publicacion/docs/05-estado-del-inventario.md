# Estado del inventario

## Resumen operativo

- Total de archivos `.dtsx` en carpeta: `137`
- Total de paquetes declarados en `Publicacion.dtproj`: `120`
- Total de archivos fuera del proyecto activo: `17`

## Definiciones

- `activo_dtproj`: el archivo `.dtsx` figura declarado en `Publicacion.dtproj`.
- `fuera_dtproj`: el archivo `.dtsx` existe en la carpeta pero no figura declarado en `Publicacion.dtproj`.

## Implicancia para el analisis

El inventario tecnico debe priorizar los paquetes `activo_dtproj`, porque son los que componen el proyecto SSIS formalmente definido. Los `fuera_dtproj` no se descartan, pero deben leerse como variantes, pruebas, historicos o artefactos auxiliares hasta demostrar lo contrario.

## Archivos fuera del proyecto activo

- `510_MovimientoPublicacion_7Dias.dtsx`
- `510_MovimientoPublicacionHistorico.dtsx`
- `800_GarantiasOpcionesMerval.dtsx`
- `Activos_MovimientoCustodiaNoProcesadoPublicacion.dtsx`
- `Contabilidad_CalcularWidgets.dtsx`
- `Contribucion_DepositoIvaPublicacion.dtsx`
- `Contribucion_OfertaEntrega.dtsx`
- `Contribucion_RelacionOperacionesAFijar.dtsx`
- `Horus_Productos_Ajuste (1).dtsx`
- `Horus_Productos_Ajuste_.dtsx`
- `Horus_VolatilidadImplicitaOperada.dtsx`
- `LibroDeOrdenes.dtsx`
- `MovimientoPublicacionUpdateTesting.dtsx`
- `Persona_PersonaHistorico.dtsx`
- `Personas_ArchivoPublicacion.dtsx`
- `Personas_CuentaRegistroCoTitularUpdate.dtsx`
- `Productos_FondoComunInversionPublicacionTipoPersona.dtsx`

## Lectura inicial del desfasaje

- Hay nombres que sugieren testing o uso auxiliar, por ejemplo `MovimientoPublicacionUpdateTesting`.
- Hay variantes que parecen duplicadas o alternativas, por ejemplo `Horus_Productos_Ajuste.dtsx`, `Horus_Productos_Ajuste (1).dtsx` y `Horus_Productos_Ajuste_.dtsx`.
- Hay casos donde el proyecto activo referencia una variante numerada y no la variante nominal, como `Contribucion_DepositoIvaPublicacion (1).dtsx` versus `Contribucion_DepositoIvaPublicacion.dtsx`.

## Artefacto de soporte

El catalogo completo del inventario, con estado y grupo nominal, se deja en:

- [inventario-paquetes.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/inventario-paquetes.csv)

## Avance de fichas detalladas

- Fecha de corte de este avance: `2026-08-11`
- Fichas totales actualmente generadas en `docs/fichas`: `84`
- Esquemas cerrados a nivel de fichas para tablas con `sincronizacion_explicita`: `Personas`, `Activos`, `Productos`, `Registro`
- Validacion realizada: no quedaron tablas con `sincronizacion_explicita` sin ficha propia dentro de esos cuatro esquemas

## Implicancia del avance

Con esta tanda ya queda cubierta la parte mas pesada del relevamiento por paquetes SSIS sobre tablas publicadas de AP5. Los esquemas `Activos`, `Productos` y `Registro` ahora tienen ficha por tabla sincronizada, manteniendo el mismo template y el mismo criterio de evidencia usado en `Personas`.
