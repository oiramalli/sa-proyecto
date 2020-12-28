# Crear Producto

Todos los productos se deberán de crear en una categoría predeterminada, se sugiere el nombre "Fase 3" para esta categoría.

## Crear Producto Cliente <a name="crear-producto-cliente"></a>
`POST /crear-producto-cliente`
| Atributo | Tipo | Requerido | Descripción |
| ------ | ------ | ------ | ------ |
| id_cliente | number | SI | Identificador del cliente que está creando el producto. |
| nombre | string | SI | Nombre del producto a crear. |
| descripcion | string | NO | Descripción del producto a crear. |
| stock | number | SI | Cantidad de inventario del producto a crear. |
| precio_venta | number | NO | Precio de venta del producto (sin el 10% de recargo). ** |
| foto | string | SI | URL de la imagen a mostrar del producto. |
| fecha_subasta | timestamp | NO | Fecha en la que se terminará la subasta en forma de UNIX timestamp (En segundos).*, ** |
| precio_inicial_subasta | number | NO | Precio inicial de la subasta. ** |
| precio_compralo_ahora | number | NO | Precio de "Comprar ahora". ** |

***Nota: Los campos `fecha_subasta`, `precio_inicial_subasta` y `precio_compralo_ahora` forman parte del paylod por motivos de compatibilidad únicamente. NO se implementará ninguna funcionalidad de subastas entre grupos.***

\* Se utilizará UNIX timestamp (en segundos) ya que este no depende de zona horaria. Cada grupo deberá de ser responzable del manejo de la fecha en frontend y backend.

\*\* De no existir `precio_venta` en el payload, `fecha_subasta`, `precio_inicial_subasta` y `precio_compralo_ahora` se vuelven obligatorios
### Ejemplos

#### Petición exitosa (Venta en tienda):

Petición

``` sh
curl --request POST 'http://<URL_BUS>/crear-producto-cliente' \
--header 'Content-Type:application/json' \
--data-raw '{
    "id_cliente": 1,
    "nombre": "Monitor LGU32",
    "descripcion": "Monitor LG de 32 pulgadas 4k@240HZ",
    "stock": 50,
    "precio_venta": 2000,
    "foto": "https://www.lg.com/us/images/monitors/md05602277/gallery/1100-1.jpg"
}' 
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
    },
    "message": "Producto creado de manera exitosa."
}
```

#### Petición exitosa (Subasta):

Petición

``` sh
curl --request POST 'http://<URL_BUS>/crear-producto-cliente' \
--header 'Content-Type:application/json' \
--data-raw '{
    "id_cliente": 1,
    "nombre": "Monitor LGU32",
    "descripcion": "Monitor LG de 32 pulgadas 4k@240HZ",
    "stock": 50,
    "foto": "https://www.lg.com/us/images/monitors/md05602277/gallery/1100-1.jpg",
    "fecha_subasta": 1608886800,
    "precio_inicial_subasta": 150,
    "precio_compralo_ahora": 500
}' 
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
        "precio_venta": null,
        "foto": "https://www.lg.com/us/images/monitors/md05602277/gallery/1100-1.jpg",
        "fecha_subasta": 1608886800,
        "precio_inicial_subasta": 150,
        "precio_compralo_ahora": 500
    },
    "message": "Producto creado de manera exitosa."
}
```

#### Petición exitosa (Subasta y Venta en tienda):

Petición

``` sh
curl --request POST 'http://<URL_BUS>/crear-producto-cliente' \
--header 'Content-Type:application/json' \
--data-raw '{
    "id_cliente": 1,
    "nombre": "Monitor LGU32",
    "descripcion": "Monitor LG de 32 pulgadas 4k@240HZ",
    "stock": 50,
    "precio_venta": 200,
    "foto": "https://www.lg.com/us/images/monitors/md05602277/gallery/1100-1.jpg",
    "fecha_subasta": 1608886800,
    "precio_inicial_subasta": 150,
    "precio_compralo_ahora": 500
}' 
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
        "precio_venta": 200,
        "foto": "https://www.lg.com/us/images/monitors/md05602277/gallery/1100-1.jpg",
        "fecha_subasta": 1608886800,
        "precio_inicial_subasta": 150,
        "precio_compralo_ahora": 500
    },
    "message": "Producto creado de manera exitosa."
}
```

#### Petición incompleta:

Petición

``` sh
curl --request POST 'http://<URL_BUS>/crear-producto-cliente' \
--header 'Content-Type:application/json' \
--data-raw '{
    "id_cliente": 1,
    "nombre": "Monitor LGU32",
    "descripcion": "Monitor LG de 32 pulgadas 4k@240HZ",
    "stock": 50,
    "foto": "https://www.lg.com/us/images/monitors/md05602277/gallery/1100-1.jpg"
}' 
```

Respuesta:

``` json
// 400
{
    "status": "fail",
    "message": "Se esperaba obtener 'precio_venta' o 'fecha_subasta', 'precio_inicial_subasta' y 'precio_compralo_ahora'."
}

```

#### Petición Fallida (Error no manejable):

Petición

``` sh
curl --request POST 'http://<URL_BUS>/crear-producto-cliente' \
--header 'Content-Type:application/json' \
--data-raw '{
    "id_cliente": 1,
    "nombre": "Monitor LGU32",
    "descripcion": "Monitor LG de 32 pulgadas 4k@240HZ",
    "stock": 50,
    "precio_venta": 200,
    "foto": "https://www.lg.com/us/images/monitors/md05602277/gallery/1100-1.jpg",
    "fecha_subasta": 1608886800,
    "precio_inicial_subasta": 150,
    "precio_compralo_ahora": 500
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

## Crear Producto Proveedor <a name="crear-producto-proveedor"></a>
`POST /crear-producto-proveedor`
| Atributo | Tipo | Requerido | Descripción |
| ------ | ------ | ------ | ------ |
| id_proveedor | number | SI | Identificador del proveedor que está creando el producto. |
| nombre | string | SI | Nombre del producto a crear. |
| descripcion | string | NO | Descripción del producto a crear. |
| stock | number | SI | Cantidad de inventario del producto a crear. |
| precio_venta | number | NO | Precio de venta del producto (sin el 10% de recargo). ** |
| foto | string | SI | URL de la imagen a mostrar del producto. |
| fecha_subasta | timestamp | NO | Fecha en la que se terminará la subasta en forma de UNIX timestamp (En segundos).*, ** |
| precio_inicial_subasta | number | NO | Precio inicial de la subasta. ** |
| precio_compralo_ahora | number | NO | Precio de "Comprar ahora". ** |

***Nota: Los campos `fecha_subasta`, `precio_inicial_subasta` y `precio_compralo_ahora` forman parte del paylod por motivos de compatibilidad únicamente. NO se implementará ninguna funcionalidad de subastas entre grupos.***

\* Se utilizará UNIX timestamp (en segundos) ya que este no depende de zona horaria. Cada grupo deberá de ser responzable del manejo de la fecha en frontend y backend.

\*\* De no existir `precio_venta` en el payload, `fecha_subasta`, `precio_inicial_subasta` y `precio_compralo_ahora` se vuelven obligatorios
### Ejemplos

#### Petición exitosa (Venta en tienda):

Petición

``` sh
curl --request POST 'http://<URL_BUS>/crear-producto-proveedor' \
--header 'Content-Type:application/json' \
--data-raw '{
    "id_proveedor": 1,
    "nombre": "Monitor LGU32",
    "descripcion": "Monitor LG de 32 pulgadas 4k@240HZ",
    "stock": 50,
    "precio_venta": 2000,
    "foto": "https://www.lg.com/us/images/monitors/md05602277/gallery/1100-1.jpg"
}' 
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
    },
    "message": "Producto creado de manera exitosa."
}
```

#### Petición exitosa (Subasta):

Petición

``` sh
curl --request POST 'http://<URL_BUS>/crear-producto-proveedor' \
--header 'Content-Type:application/json' \
--data-raw '{
    "id_proveedor": 1,
    "nombre": "Monitor LGU32",
    "descripcion": "Monitor LG de 32 pulgadas 4k@240HZ",
    "stock": 50,
    "foto": "https://www.lg.com/us/images/monitors/md05602277/gallery/1100-1.jpg",
    "fecha_subasta": 1608886800,
    "precio_inicial_subasta": 150,
    "precio_compralo_ahora": 500
}' 
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
        "precio_venta": null,
        "foto": "https://www.lg.com/us/images/monitors/md05602277/gallery/1100-1.jpg",
        "fecha_subasta": 1608886800,
        "precio_inicial_subasta": 150,
        "precio_compralo_ahora": 500
    },
    "message": "Producto creado de manera exitosa."
}
```

#### Petición exitosa (Subasta y Venta en tienda):

Petición

``` sh
curl --request POST 'http://<URL_BUS>/crear-producto-proveedor' \
--header 'Content-Type:application/json' \
--data-raw '{
    "id_proveedor": 1,
    "nombre": "Monitor LGU32",
    "descripcion": "Monitor LG de 32 pulgadas 4k@240HZ",
    "stock": 50,
    "precio_venta": 200,
    "foto": "https://www.lg.com/us/images/monitors/md05602277/gallery/1100-1.jpg",
    "fecha_subasta": 1608886800,
    "precio_inicial_subasta": 150,
    "precio_compralo_ahora": 500
}' 
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
        "precio_venta": 200,
        "foto": "https://www.lg.com/us/images/monitors/md05602277/gallery/1100-1.jpg",
        "fecha_subasta": 1608886800,
        "precio_inicial_subasta": 150,
        "precio_compralo_ahora": 500
    },
    "message": "Producto creado de manera exitosa."
}
```

#### Petición incompleta:

Petición

``` sh
curl --request POST 'http://<URL_BUS>/crear-producto-proveedor' \
--header 'Content-Type:application/json' \
--data-raw '{
    "id_proveedor": 1,
    "nombre": "Monitor LGU32",
    "descripcion": "Monitor LG de 32 pulgadas 4k@240HZ",
    "stock": 50,
    "foto": "https://www.lg.com/us/images/monitors/md05602277/gallery/1100-1.jpg"
}' 
```

Respuesta:

``` json
// 400
{
    "status": "fail",
    "message": "Se esperaba obtener 'precio_venta' o 'fecha_subasta', 'precio_inicial_subasta' y 'precio_compralo_ahora'."
}

```

#### Petición Fallida (Error no manejable):

Petición

``` sh
curl --request POST 'http://<URL_BUS>/crear-producto-proveedor' \
--header 'Content-Type:application/json' \
--data-raw '{
    "id_proveedor": 1,
    "nombre": "Monitor LGU32",
    "descripcion": "Monitor LG de 32 pulgadas 4k@240HZ",
    "stock": 50,
    "precio_venta": 200,
    "foto": "https://www.lg.com/us/images/monitors/md05602277/gallery/1100-1.jpg",
    "fecha_subasta": 1608886800,
    "precio_inicial_subasta": 150,
    "precio_compralo_ahora": 500
}' 
```

Respuesta:

``` json
// 500
{
    "status": "error",
    "message": "Ocurrió un error inesperado."
}
