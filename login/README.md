# Login

## Login Cliente <a name="login-cliente"></a>
`POST /login-cliente`
| Atributo | Tipo | Requerido | Descripción |
| ------ | ------ | ------ | ------ |
| email | string | SI | El correo electrónico con el que el cliente se registró. |
| contrasena | string | SI | La para inicio de sesión; debe de ir en texto plano (sin encriptar). |

### Ejemplos

#### Petición exitosa:

Petición

``` sh
curl --request POST 'http://<URL_BUS>/login-cliente' \
--header 'Content-Type:application/json' \
--data-raw '{
    "email":"eder@usac.com",
    "contrasena":"SuperSegura"
}' 
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
    "message": "Usuario autenticado de manera exitosa."
}

```

#### Petición incompleta:

Petición

``` sh
curl --request POST 'http://<URL_BUS>/login-cliente' \
--header 'Content-Type:application/json' \
--data-raw '{
    "email":"eder@usac.com"
}' 
```

Respuesta:

``` json
// 400
{
    "status": "fail",
    "message": "No se encontró el campo obligatorio 'contrasena'."
}

```

#### Petición Fallida (Error manejable):

Petición

``` sh
curl --request POST 'http://<URL_BUS>/login-cliente' \
--header 'Content-Type:application/json' \
--data-raw '{
    "email":"nadie@usac.com",
    "contrasena":"SuperSegura",
}' 
```
Respuesta:
``` json
// 401
{
    "status": "error",
    "message": "Las contraseña es incorrecta o el usuario no existe."
}

```

#### Petición Fallida (Error no manejable):

Petición

``` sh
curl --request POST 'http://<URL_BUS>/login-cliente' \
--header 'Content-Type:application/json' \
--data-raw '{
    "email":"eder@usac.com",
    "contrasena":"SuperSegura"
}' 
```
Respuesta:
``` json
// 500
{
    "status": "error",
    "message": "Ocurrió un error inesperado."
}

```
## Login Proveedor <a name="login-proveedor"></a>
`POST /login-proveedor`
| Atributo | Tipo | Requerido | Descripción |
| ------ | ------ | ------ | ------ |
| email | string | SI | El correo electrónico con el que el cliente se registró. |
| contrasena | string | SI | La para inicio de sesión; debe de ir en texto plano (sin encriptar). |

### Ejemplos

#### Petición exitosa:

Petición

``` sh
curl --request POST 'http://<URL_BUS>/login-proveedor' \
--header 'Content-Type:application/json' \
--data-raw '{
    "email":"eder@proveedor.com",
    "contrasena":"SuperSegura"
}' 
```

Respuesta:

``` json
// 200
{
    "status": "success",

    "data": {
        "id": 100,
        "nombre":"Eder",
        "apellido":"García",
        "empresa":"USAC",
        "email":"eder@proveedor.com",
        "contrasena":"SuperSegura",
        "empresa":"Ciudad universitaria (USAC) Campus Central Z12."
    },
    "message": "Usuario autenticado de manera exitosa."
}
```

#### Petición incompleta:

Petición

``` sh
curl --request POST 'http://<URL_BUS>/login-proveedor' \
--header 'Content-Type:application/json' \
--data-raw '{
    "email":"eder@proveedor.com"
}' 
```

Respuesta:

``` json
// 400
{
    "status": "fail",
    "message": "No se encontró el campo obligatorio 'contrasena'."
}

```

#### Petición Fallida (Error manejable):

Petición

``` sh
curl --request POST 'http://<URL_BUS>/login-proveedor' \
--header 'Content-Type:application/json' \
--data-raw '{
    "email":"nadie@proveedor.com",
    "contrasena":"SuperSegura",
}' 
```
Respuesta:
``` json
// 401
{
    "status": "error",
    "message": "Las contraseña es incorrecta o el usuario no existe."
}

```

#### Petición Fallida (Error no manejable):

Petición

``` sh
curl --request POST 'http://<URL_BUS>/login-proveedor' \
--header 'Content-Type:application/json' \
--data-raw '{
    "email":"eder@proveedor.com",
    "contrasena":"SuperSegura"
}' 
```
Respuesta:
``` json
// 500
{
    "status": "error",
    "message": "Ocurrió un error inesperado."
}
```