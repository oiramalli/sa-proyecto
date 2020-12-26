# Comprar

## Realizar Compra <a name="realizar-compra"></a>
`POST /realizar-compra`
| Atributo | Tipo | Requerido | Descripción |
| ------ | ------ | ------ | ------ |
| id_cliente | number | SI | Identificador del cliente que está relizando la compra. |
| productos | `{ id_producto: number, cantidad: number }[]` | SI | Un arreglo que contiene el listado de productos a comprar (identificador de cada producto y la cantidad a comprar). |

### Ejemplos

#### Petición exitosa (Venta en tienda):

Petición

``` sh
curl --request POST 'http://<URL_BUS>/realizar-compra' \
--header 'Content-Type:application/json' \
--data-raw '{
    "id_cliente": 1,
    "productos": [
        {
            "id_producto": 1,
            "cantidad": 5
        },
        {
            "id_producto": 3,
            "cantidad": 1
        },
        {
            "id_producto": 5,
            "cantidad": 2
        },
        {
            "id_producto": 10,
            "cantidad": 2
        }
    ]
}' 
```

Respuesta:

``` json
// 200
{
    "status": "success",
    "message": "Se ha relizado la compra de manera exitosa."
}
```

#### Petición incompleta (Cliente faltante):

Petición

``` sh
curl --request POST 'http://<URL_BUS>/realizar-compra' \
--header 'Content-Type:application/json' \
--data-raw '{
    "productos": [
        {
            "id_producto": 1,
            "cantidad": 5
        },
        {
            "id_producto": 3,
            "cantidad": 1
        },
        {
            "id_producto": 5,
            "cantidad": 2
        },
        {
            "id_producto": 10,
            "cantidad": 2
        }
    ]
}' 
```

Respuesta:

``` json
// 400
{
    "status": "fail",
    "message": "No se encontró el campo obligatorio 'id_cliente'."
}

```

#### Petición incompleta (Datos de producto faltantes):

Petición

``` sh
curl --request POST 'http://<URL_BUS>/realizar-compra' \
--header 'Content-Type:application/json' \
--data-raw '{
    "id_cliente": 1,
    "productos": [
        {
            "id_producto": 1,
            "cantidad": 5
        },
        {
            "id_producto": 3,
            "cantidad": 1
        },
        {
            "id_producto": 5,
        },
        {
            "id_producto": 10,
            "cantidad": 2
        }
    ]
}' 
```

Respuesta:

``` json
// 400
{
    "status": "fail",
    "message": "Hace falta un atributo en uno o mas productos."
}

```

#### Petición Fallida (Error manejable):

Petición

``` sh
curl --request POST 'http://<URL_BUS>/realizar-compra' \
--header 'Content-Type:application/json' \
--data-raw '{
    "id_cliente": 1,
    "productos": [
        {
            "id_producto": 1,
            "cantidad": 5
        },
        {
            "id_producto": 3,
            "cantidad": 1
        },
        {
            "id_producto": 5,
            "cantidad": 2
        },
        {
            "id_producto": 10,
            "cantidad": 2
        }
    ]
}' 
```

Respuesta:

``` json
// 409
{
    "status": "fail",
    "message": "No hay suficientes unidades del producto con identificador 5 para completar esta venta."
}
```

#### Petición Fallida (Error no manejable):

Petición

``` sh
curl --request POST 'http://<URL_BUS>/realizar-compra' \
--header 'Content-Type:application/json' \
--data-raw '{
    "id_cliente": 1,
    "productos": [
        {
            "id_producto": 1,
            "cantidad": 5
        },
        {
            "id_producto": 3,
            "cantidad": 1
        },
        {
            "id_producto": 5,
            "cantidad": 2
        },
        {
            "id_producto": 10,
            "cantidad": 2
        }
    ]
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
