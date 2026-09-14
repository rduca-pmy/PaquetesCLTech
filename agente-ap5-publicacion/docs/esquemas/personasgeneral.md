# Esquema PersonasGeneral

## Resumen

- Tablas en `Publicacion.sql`: `32`
- Tablas con evidencia en SSIS: `32`
- Tablas sin evidencia en SSIS: `0`

## Lectura inicial

Esquema con cobertura total. Funciona como complemento estructural de `Personas` y aparece fuertemente ligado a `030_PersonasGeneral*` y `PersonasGeneral_Persona.dtsx`.

## Paquetes relevantes

- `030_PersonasGeneral.dtsx`
- `030_PersonasGeneralLight.dtsx`
- `030_PersonasGeneralViejo.dtsx`
- `PersonasGeneral_Persona.dtsx`
- tambien aparece en `PersonasEntrega.dtsx`, `Contribucion_MargenEntrega.dtsx`, `Productos_TarifaDevengada.dtsx` y `Productos_TarifaPublicacion.dtsx`

## Matriz inicial de tablas

| Tabla | Paquete o paquetes principales | Evidencia observada |
| --- | --- | --- |
| `PersonasGeneral.Actividad` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.AreaContacto` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.Autoridad` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.CargoPolitico` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.Contacto` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.ContactoTelefono` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.CuentaDepositaria` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralLight.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.Domicilio` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralLight.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.EntidadDepositaria` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralLight.dtsx`, `030_PersonasGeneralViejo.dtsx`, `Productos_TarifaDevengada.dtsx`, `Productos_TarifaPublicacion.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.Escala` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.ExclusionImpuesto` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.FacultadPoder` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.GrupoDeFirmas` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.GrupoEconomico` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.Persona` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralLight.dtsx`, `030_PersonasGeneralViejo.dtsx`, `PersonasGeneral_Persona.dtsx` | `OpenRowset`, `UPDATE` |
| `PersonasGeneral.PersonaImpuesto` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.Poder` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.Proveedor` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.Regimen` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.SubcuentaDepositaria` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralLight.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.Telefono` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.TipoAutoridad` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.TipoCuentaDepositaria` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralLight.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.TipoCuentaDepositariaTipoActivo` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralLight.dtsx` | `OpenRowset`, `SELECT` |
| `PersonasGeneral.TipoCuentaEntidad` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralLight.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `SELECT` |
| `PersonasGeneral.TipoDocumento` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralLight.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.TipoDomicilio` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralLight.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.TipoEntidadDepositaria` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralLight.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.TipoOrigenPoder` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.TipoServicio` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.TipoSocietario` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `PersonasGeneral.TipoTelefono` | `030_PersonasGeneral.dtsx`, `030_PersonasGeneralViejo.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |

## Nota

Es uno de los esquemas mejor soportados por SSIS en esta fase.

## Artefactos de soporte

- [personasgeneral-tablas-matriz.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/personasgeneral-tablas-matriz.csv)
