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

