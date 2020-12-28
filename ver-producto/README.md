# Ver Productos

El `precio_venta` que se enviará del servidor al cliente ya debe de tener incluído el 10% de recargo.

## Ver todos los productos <a name="ver-todos-los-productos"></a>
`GET /ver-productos`

Ver todos los productos de todas las categorías.

### Ejemplos

#### Petición exitosa

Petición

``` sh
curl --request GET 'http://<URL_BUS>/ver-productos'
```

Respuesta:

``` json
// 200
{
    "status": "success",
    "data": [
        {
        "id_producto": 1,
        "nombre": "Monitor LGU32",
        "descripcion": "Monitor LG de 32 pulgadas 4k@240HZ",
        "stock": 50,
        "precio_venta": 2000,
        "foto": "https://www.lg.com/us/images/monitors/md05602277/gallery/1100-1.jpg",
        "fecha_subasta": null,
        "precio_inicial_subasta": null,
        "precio_compralo_ahora": null
        },
        {
        "id_producto": 10,
        "nombre": "Teclado TUF gaming-7",
        "descripcion": "Teclado mecánico óptico de gaming TUF Gaming K7 con resistencia IP56 contra polvo y líquidos, aluminio aeronáutico e iluminación Aura Sync",
        "stock": 60,
        "precio_venta": null,
        "foto": "https://www.asus.com/media/global/products/VhfjeAw84tomuPVC/P_setting_xxx_0_90_end_500.png",
        "fecha_subasta": 1608886800,
        "precio_inicial_subasta": 150,
        "precio_compralo_ahora": 500
        },
        {
        "id_producto": 100,
        "nombre": "Mouse TUF gaming-M5",
        "descripcion": "ASUS TUF Gaming M5 ratón para juegos RGB ergonómico con sensor óptico de nivel de juego, recubrimiento duradero, interruptores Omron para uso rudo e iluminación Aura Sync",
        "stock": 70,
        "precio_venta": 550,
        "foto": "https://www.asus.com/media/global/products/07G77lBcB8Yo5R8y/P_setting_000_1_90_end_500.png",
        "fecha_subasta": 1608886800,
        "precio_inicial_subasta": 250,
        "precio_compralo_ahora": 600
        }
    ]
}
```

## Ver productos de categoría 'Fase 3' (Descontinuado) <a name="ver-productos-fase-3"></a>
`GET /ver-productos-fase-3 (DESCONTINUADO)`

***Este endpoint ya no será implementado. Se utilizará `/ver-productos` en su lugar; cada grupo puede hacer un filtrado de categorías de manera independiente para poder ver los productos creados mediante integración entre grupos.***
Todos los productos de la categoría predeterminada, se sugiere el nombre "Fase 3" para esta categoría.

#### Petición exitosa

Petición

``` sh
curl --request GET 'http://<URL_BUS>/ver-productos-fase-3'
```

Respuesta:

``` json
// 200
{
    "status": "success",
    "data": [
        {
        "id_producto": 1,
        "nombre": "Monitor LGU32",
        "descripcion": "Monitor LG de 32 pulgadas 4k@240HZ",
        "stock": 50,
        "precio_venta": 2000,
        "foto": "https://www.lg.com/us/images/monitors/md05602277/gallery/1100-1.jpg",
        "fecha_subasta": null,
        "precio_inicial_subasta": null,
        "precio_compralo_ahora": null
        },
        {
        "id_producto": 10,
        "nombre": "Teclado TUF gaming-7",
        "descripcion": "Teclado mecánico óptico de gaming TUF Gaming K7 con resistencia IP56 contra polvo y líquidos, aluminio aeronáutico e iluminación Aura Sync",
        "stock": 60,
        "precio_venta": null,
        "foto": "https://www.asus.com/media/global/products/VhfjeAw84tomuPVC/P_setting_xxx_0_90_end_500.png",
        "fecha_subasta": 1608886800,
        "precio_inicial_subasta": 150,
        "precio_compralo_ahora": 500
        },
        {
        "id_producto": 100,
        "nombre": "Mouse TUF gaming-M5",
        "descripcion": "ASUS TUF Gaming M5 ratón para juegos RGB ergonómico con sensor óptico de nivel de juego, recubrimiento duradero, interruptores Omron para uso rudo e iluminación Aura Sync",
        "stock": 70,
        "precio_venta": 550,
        "foto": "https://www.asus.com/media/global/products/07G77lBcB8Yo5R8y/P_setting_000_1_90_end_500.png",
        "fecha_subasta": 1608886800,
        "precio_inicial_subasta": 250,
        "precio_compralo_ahora": 600
        }
    ]
}
```

## Ver un producto <a name="ver-producto"></a>
`GET /ver-producto?id_producto=val`

val debe de ser de tipo número.

#### Petición exitosa

Petición

``` sh
curl --request GET 'http://<URL_BUS>/ver-producto?id_producto=1'
```

Respuesta:

``` json
// 200
{
    "status": "success",
    "data": {
        "id_producto": 1,
        "nombre": "Monitor LGU32",
        "descripcion": "Monitor LG de 32 pulgadas 4k@240HZ",
        "stock": 50,
        "precio_venta": 2000,
        "foto": "https://www.lg.com/us/images/monitors/md05602277/gallery/1100-1.jpg",
        "fecha_subasta": null,
        "precio_inicial_subasta": null,
        "precio_compralo_ahora": null
    }
}
```

#### Petición Fallida (Error manejable)

Petición

``` sh
curl --request GET 'http://<URL_BUS>/ver-producto?id_producto=300'
```

Respuesta:

``` json
// 400
{
    "status": "fail",
    "message": "No existe producto."
}
```

#### Petición Fallida (Error no manejable)

Petición

``` sh
curl --request GET 'http://<URL_BUS>/ver-producto?id_producto=xyz'
```

Respuesta:

``` json
// 500
{
    "status": "error",
    "message": "Ocurrió un error inseperado."
}
```