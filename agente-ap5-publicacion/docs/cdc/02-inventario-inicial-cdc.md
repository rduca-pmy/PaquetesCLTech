# Inventario inicial de funciones CDC

## Resumen

- Funciones CDC detectadas en `Clearing.sql`: `35`
- Procedimientos CDC detectados en `Clearing.sql`: `0`
- Tablas CDC detectadas en `Clearing.sql`: `1`
- Tabla tecnica detectada: `cdc.TableOffset`

## Lectura inicial

El esquema `cdc` de `Clearing.sql` contiene un conjunto relevante de funciones `fn_cdc_get_*_Publicacion` orientadas a dominios ya conocidos en AP5. La mayor concentracion inicial aparece en:

- `Compensacion`
- `Contribucion`
- `Registro`
- `Mensajes`

Esto refuerza la idea de que la fase CDC es complementaria a la fase SSIS y especialmente importante para los dominios donde el relevamiento por paquetes fue incompleto.

## Distribucion inicial por esquema inferido

| Esquema inferido | Cantidad de funciones CDC |
| --- | ---: |
| `Compensacion` | `9` |
| `ComprobantesGeneral` | `2` |
| `Contabilidad` | `2` |
| `Contribucion` | `5` |
| `General` | `2` |
| `Mensajes` | `3` |
| `MensajesGeneral` | `1` |
| `Personas` | `3` |
| `Productos` | `3` |
| `Registro` | `5` |

## Ejemplos representativos

| Funcion CDC | Lectura inicial |
| --- | --- |
| `cdc.fn_cdc_get_Registro_OperacionCartera_Publicacion` | candidata directa para profundizar el circuito de `Registro` |
| `cdc.fn_cdc_get_Contribucion_Cuenta_Publicacion` | complemento natural de la ficha `Contribucion.Cuenta` |
| `cdc.fn_cdc_get_Productos_Contrato_Publicacion` | candidata para relacionar origen PBP con publicacion de contratos |
| `cdc.fn_cdc_get_MensajesGeneral_Mensaje_Publicacion` | clave para abrir la fase de `MensajesGeneral`, hoy sin evidencia SSIS |
| `cdc.fn_cdc_get_Mensajes_MensajeDepositoIVA_Publicacion` | sugiere un puente entre mensajeria y publicacion |

## Hallazgos iniciales

- Existen variantes legacy, por ejemplo `fn_cdc_get_Registro_OperacionCartera_Publicacion_old`.
- El patron de nombres es bastante consistente y permite agrupar por dominio funcional.
- `Mensajes` y `MensajesGeneral`, que en SSIS quedaron sin evidencia, si muestran funciones CDC candidatas.
- `Contribucion` tambien gana relevancia en esta fase, porque su cobertura SSIS habia quedado baja.

## Proxima iteracion sugerida

1. Tomar `Registro`, `Contribucion` y `Mensajes` como primera tanda de profundizacion CDC.
2. Cruzar cada funcion con tablas ya documentadas en AP5.
3. Crear una ficha CDC estandar para cada funcion o familia de funciones.

## Avance posterior

La primera tanda ya fue iniciada y se documento en:

- [03-mapeo-primer-tanda-cdc.md](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/docs/cdc/03-mapeo-primer-tanda-cdc.md)
- [cdc-mapeo-primer-tanda.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/cdc-mapeo-primer-tanda.csv)

## Artefactos de soporte

- [cdc-funciones-inventario.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/cdc-funciones-inventario.csv)
