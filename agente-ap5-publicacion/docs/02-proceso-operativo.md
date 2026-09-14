# Proceso operativo

## Flujo general

1. Inventariar paquetes del proyecto `Publicacion`.
2. Cruzar el inventario con `Publicacion.dtproj` para distinguir paquetes activos, variantes y posibles legacies.
3. Analizar cada paquete y extraer comandos, tablas y SPs relevantes.
4. Apoyar la interpretacion con `Clearing.sql` y `Publicacion.sql` cuando la logica viva en base de datos.
5. Detectar la o las tablas destino de AP5.
6. Clasificar si la operacion corresponde a sincronizacion o a logica interna.
7. Consolidar una ficha por tabla o relacion documentable.
8. Revisar inconsistencias y dejar preguntas abiertas.

## Unidad de trabajo recomendada

La unidad base de avance debe ser:

- un paquete `.dtsx`, para el analisis tecnico
- una tabla AP5, para la documentacion final

## Artefactos intermedios sugeridos

- inventario de paquetes
- matriz paquete -> tabla destino
- matriz tabla destino -> paquetes
- lista de tablas locales AP5
- lista de casos ambiguos

## Convenciones de documentacion

- Hecho: dato observado directamente en el paquete.
- Inferencia: conclusion razonable a partir de evidencia parcial.
- Duda: punto que requiere validacion funcional o tecnica.

## Criterio de cierre por ficha

Una ficha se considera lista cuando contiene:

- tabla destino identificada
- paquete o paquetes asociados
- mecanismo tecnico de carga
- evidencia puntual
- clasificacion
- observaciones y dudas

## Riesgos conocidos

- un paquete puede tocar varias tablas destino
- puede haber paquetes duplicados, variantes de testing o versiones legacy
- una tabla puede llenarse por mas de un paquete
- parte de la logica puede estar delegada a stored procedures no visibles en el `.dtsx`
- la diferencia entre archivos `.dtsx` y paquetes declarados en `Publicacion.dtproj` puede introducir ruido si no se distingue proyecto activo vs variantes
- algunos nombres de paquete pueden no reflejar con precision la tabla destino real

## Orden recomendado para comenzar la documentacion real

1. Paquetes de alta claridad por nombre y destino directo.
2. Paquetes con `Merge*` o `Insert*` evidentes.
3. Paquetes multiproposito o con varias tablas.
4. Casos historicos, testing o legacy.

## Extension para fase CDC

Cuando se pase a CDC, el flujo recomendado cambia a:

1. Inventariar funciones del esquema `[cdc]` en `Clearing.sql`.
2. Agrupar funciones por dominio funcional inferido.
3. Cruzar cada funcion con tablas y fichas AP5 ya documentadas.
4. Marcar si el mapeo es directo, probable, ambiguo o aun no identificado.
5. Consolidar el circuito completo `PBP -> CDC -> AP5`.
