# API PARA NEXTCONNECTOR

# IMPORTACION DE CLIENTES 

- GET customers 
- GET customer

## GET /customers
El metodo retorna el listado de clientes que hay que importar a Odoo

**Ejmplo Python request**

```python
import requests

url = "/api/records/customers"

payload = {
  "credentials": {
    "user": "userapi", 
    "password": "pass_api"
  }, 
  "record": {
    "id": "", 
    "record_type": "customer", 
    "fields": []
   }
}

headers = {
    'content-type': "application/json" 
}

response = requests.request("GET", url, data=payload, headers=headers)

print(response.text)
```
Como respuesta se obtiene un listado de codigos de clientes por sincronizar a Odoo, estos codigos seran utilizados 
en el llamado del siguiente metodo. 

**Ejemplo Respuesta en JSON**
```python
{
  "list_data": [{"id": "customers", "data": ['C001','C002','C003']}], 
  "id_erp": null, 
  "code": "0", 
  "message": null
}
```

## GET /customer
El metodo retorna los datos/campos de un cliente especifico que se envie como parametro en el body.

**Ejemplo Python request**
```python
import requests

url = "/api/records/customer"

payload = {
  "credentials": {
    "user": "userapi", 
    "password": "pass_api"
  }, 
  "record": {
    "id": "C001", 
    "record_type": "customer", 
    "fields": []
   }
}

headers = {
    'content-type': "application/json" 
}

response = requests.request("GET", url, data=payload, headers=headers)

print(response.text)
```
Como respuesta se obtiene los campos del cliente que deben ser registrados en el cliente que se consultando para sincronizar a Odoo

**Ejemplo Respuesta en JSON**
```python
{
  "list_data": [{
    "id": "customer", 
    "data": [
      {"code":"C001", "name":"Victor Pincay", "email":"prueba@gmail.com", "vat":"12345678"}
     ]
    }], 
  "id_erp": "C001", 
  "code": "0", 
  "message": null
}
```




# IMPORTACION DE ARTICULOS 

- GET items 
- GET item

## GET /items
El metodo retorna el listado de articulos que hay que importar a Odoo

**Ejmplo Python request**

```python
import requests

url = "/api/records/items"

payload = {
  "credentials": {
    "user": "userapi", 
    "password": "pass_api"
  }, 
  "record": {
    "id": "", 
    "record_type": "item", 
    "fields": []
   }
}

headers = {
    'content-type': "application/json" 
}

response = requests.request("GET", url, data=payload, headers=headers)

print(response.text)
```
Como respuesta se obtiene un listado de codigos de articulos por sincronizar a Odoo, estos codigos seran utilizados 
en el llamado del siguiente metodo. 

**Ejemplo Respuesta en JSON**
```python
{
  "list_data": [{"id": "items", "data": ['SKU001','SKU002','SKU003']}], 
  "id_erp": null, 
  "code": "0", 
  "message": null
}
```

## GET /item
El metodo retorna los datos/campos de un articulos especifico que se envie como parametro en el body.

**Ejemplo Python request**
```python
import requests

url = "/api/records/customer"

payload = {
  "credentials": {
    "user": "userapi", 
    "password": "pass_api"
  }, 
  "record": {
    "id": "SKU001", 
    "record_type": "item", 
    "fields": []
   }
}

headers = {
    'content-type': "application/json" 
}

response = requests.request("GET", url, data=payload, headers=headers)

print(response.text)
```
Como respuesta se obtiene los campos del articulo que deben ser registrados en Odoo

**Ejemplo Respuesta en JSON**
```python
{
  "list_data": [{
    "id": "customer", 
    "data": [
      {"code":"SKU001", "name":"PC DELL", "price":100, "category":"computers"}
     ]
    }], 
  "id_erp": "SKU001", 
  "code": "0", 
  "message": null
}
```



# IMPORTACION DE STOCK 

- GET stock 

## GET /items
El metodo retorna el lista de articulos con su cantidad de stock disponible

**Ejmplo Python request**

```python
import requests

url = "/api/records/stock"

payload = {
  "credentials": {
    "user": "userapi", 
    "password": "pass_api"
  }, 
  "record": {
    "id": "", 
    "record_type": "stock", 
    "fields": []
   }
}

headers = {
    'content-type': "application/json" 
}

response = requests.request("GET", url, data=payload, headers=headers)

print(response.text)
```
Como respuesta se obtiene un listado de codigos de articulos con su cantidad de stock disponible.

**Ejemplo Respuesta en JSON**
```python
{
  "list_data": [{
    "id": "stock", 
    "data": [
      {"code":"SKU001", "qty_done":100},
      {"code":"SKU002", "qty_done":50},
      {"code":"SKU003", "qty_done":80}
     ]
    }], 
  "id_erp": "", 
  "code": "0", 
  "message": null
}
```



# IMPORTACION DE LISTA DE PRECIOS

- GET listprices 
- GET listprice

## GET /listprices
El metodo retorna el listado de listas de precios a sincronizar en Odoo

**Ejmplo Python request**

```python
import requests

url = "/api/records/listprices"

payload = {
  "credentials": {
    "user": "userapi", 
    "password": "pass_api"
  }, 
  "record": {
    "id": "", 
    "record_type": "listprices", 
    "fields": []
   }
}

headers = {
    'content-type': "application/json" 
}

response = requests.request("GET", url, data=payload, headers=headers)

print(response.text)
```
Como respuesta se obtiene un listado de listas de precios por sincronizar a Odoo, estos codigos seran utilizados 
en el llamado del siguiente metodo. 

**Ejemplo Respuesta en JSON**
```python
{
  "list_data": [{"id": "items", "data": ['LP PVP','LP LEVEL 2','LP LEVEL 3']}], 
  "id_erp": null, 
  "code": "0", 
  "message": null
}
```

## GET /item
El metodo retorna una lista de articulos y su precio. Recibe como parametro un codigo de lista precios para filtrar el resultado

**Ejemplo Python request**
```python
import requests

url = "/api/records/listprice"

payload = {
  "credentials": {
    "user": "userapi", 
    "password": "pass_api"
  }, 
  "record": {
    "id": "LP PVP", 
    "record_type": "listprice", 
    "fields": []
   }
}

headers = {
    'content-type': "application/json" 
}

response = requests.request("GET", url, data=payload, headers=headers)

print(response.text)
```
Como respuesta se obtiene el listado de articulos con su precio. 

**Ejemplo Respuesta en JSON**
```python
{
  "list_data": [{
    "id": "listprice", 
    "data": [
      {"code":"SKU001", "price":100}, 
      {"code":"SKU002", "price":50}, 
      {"code":"SKU003", "price":99}
     ]
    }], 
  "id_erp": "LP PVP", 
  "code": "0", 
  "message": null
}
```


