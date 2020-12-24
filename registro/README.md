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

### Ejemplos

Petición éxitosa:

``` sh
curl --request POST --header Content-Type:application/json --data '{"nombre":"Eder", "apellido":"García", "email":"eder@usac.com", "contrasena":"SuperSegura", "celular":12345678}' "http://<URL_BUS>/registrar-cliente"
```

Respuesta:

``` json
// 200
 {
    "status": "success",

    "data": {
        "id": 1,
        "nombre":"Eder",
        "apellido":"García",
        "email":"eder@usac.com",
        "contrasena":"SuperSegura",
        "celular":12345678
    },
 
    "message": "Usuario creado de manera exitosa.",
}

```

Petición incompleta:

``` sh
curl --request POST --header Content-Type:application/json --data '{"nombre":"Eder", "apellido":"García", "email":"eder@usac.com"}' "http://<URL_BUS>/registrar-cliente"
```

Respuesta:

``` json
// 400
 {
    "status": "fail",
    "message": "No se encontró el campo obligatorio 'contrasena'.",
}

```

Petición Fallida:

``` sh
curl --request POST --header Content-Type:application/json --data '{"nombre":"Eder", "apellido":"García", "email":"eder@usac.com", "contrasena":"SuperSegura", "celular":12345678}' "http://<URL_BUS>/registrar-cliente"
```
Respuesta:
``` json
// 409
 {
    "status": "error",
    "message": "Ya existe un usuario registrado con ese correo electrónico.",
}

```

Petición Fallida:

``` sh
curl --request POST --header Content-Type:application/json --data '{"nombre":"Otro", "apellido":"Usuario", "email":"usuario@usac.com", "contrasena":"SuperSegura", "celular":12345678}' "http://<URL_BUS>/registrar-cliente"
```
Respuesta:
``` json
// 500
 {
    "status": "error",
    "message": "Ocurrió un error inesperado.",
}

```
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