# Esquema Mensajes

## Resumen

- Tablas en `Publicacion.sql`: `31`
- Tablas con evidencia en SSIS: `0`
- Tablas sin evidencia en SSIS: `31`

## Lectura inicial

No se observo evidencia SSIS directa sobre tablas del esquema `Mensajes` dentro de `IntegrationServices/Publicacion`. Esto sugiere que su circuito de carga probablemente no pase por estos paquetes, o no lo haga de forma explicita.

## Matriz inicial de tablas

No se detectaron tablas de `Mensajes` con `OpenRowset`, `DELETE` o `UPDATE` explicito dentro de `IntegrationServices/Publicacion`.

## Tablas sin evidencia observada

Todas las tablas del esquema quedaron sin evidencia en esta fase, incluyendo:

- `MensajeReasignacionCuenta`
- `MensajeLiquidacionCompensacion`
- `MensajeGarantia`
- `MensajeTransferencia`
- `MensajeCompraVentaDolares`
- `MensajeCompensacionDepositaria`
- `MensajeDepositoIva`
- `MensajeRetencionesRecibidas`

## Nota

Es un fuerte candidato a ser cubierto mas adelante desde el circuito de mensajeria o CDC, no desde jobs SSIS de publicacion.

## Artefactos de soporte

- [mensajes-tablas-matriz.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/mensajes-tablas-matriz.csv)
