# Registro

## Registrar Cliente <a name="registrar-cliente"></a>
`POST /registrar-cliente`
| Atributo | Tipo | Requerido | Descripción |
| ------ | ------ | ------ | ------ |
| nombre | string | SI | El nombre del cliente que se está creando. |
| apellido | string | NO | El apellido del cliente que se está creando. |
| email | string | SI | El correo electrónico del cliente que se está creando. Este se utilizará para el inicio de sesión. |
| contrasena | string | SI | La contraseña del cliente que se está creando; debe de ir en texto plano (sin encriptar). |
| celular | number | NO | El número de celular del cliente que se está creando. |

## Registrar Proveedor <a name="registrar-proveedor"></a>
`POST /registrar-proveedor`
| Atributo | Tipo | Requerido | Descripción |
| ------ | ------ | ------ | ------ |
| nombre | string | SI | El nombre del proveedor que se está creando. |
| apellido | string | NO | El apellido del proveedor que se está creando. |
| empresa | string | SI | La empresa a la que pertenece el proveedor que se está creando. |
| email | string | SI | El correo electrónico del proveedor que se está creando. Este se utilizará para el inicio de sesión. |
| contrasena | string | SI | La contraseña del proveedor que se está creando; debe de ir en texto plano (sin encriptar). |
| direccion | string | NO | La dirección del proveedor que se está creando. |