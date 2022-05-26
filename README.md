# API PARA NEXTCONNECTOR
El siguiente documento pretende detallar las APIS que tiene el NextConnector del lado de SAP para la comunicacion con Odoo.

# IMPORTACION DE CLIENTES 

- GET /customers 
- GET /customer

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

- GET /items 
- GET /item

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
    "id": "item", 
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

- GET /stock 

## GET /stock
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



# IMPORTACION DE LISTAS DE PRECIOS

- GET /listprices 
- GET /listprice

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

## GET /listprice
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


# IMPORTACION DE RESUMEN DE ESTADO DE CUENTA DE CLIENTE 

- GET /customer/balance 

## GET /customer/balance 
El metodo retorna la informacion de la deuda y limite de credito del cliente.

**Ejmplo Python request**

```python
import requests

url = "/api/customer/balance"

payload = {
  "credentials": {
    "user": "userapi", 
    "password": "pass_api"
  }, 
  "record": {
    "id": "C001", 
    "record_type": "balance", 
    "fields": []
   }
}

headers = {
    'content-type': "application/json" 
}

response = requests.request("GET", url, data=payload, headers=headers)

print(response.text)
```
Como respuesta se obtiene la informacion de la deuda y limite de credito del cliente.

**Ejemplo Respuesta en JSON**
```python
{
  "list_data": [{
    "id": "stock", 
    "data": [
      {"credilimit":100, "balance":60, "dueblance":30}
     ]
    }], 
  "id_erp": "", 
  "code": "0", 
  "message": null
}
```


# ENVIO DE ORDEN DE VENTA Y FACTURA

- POST /transaction 

## POST /transaction 
El metodo recibe una estructura JSON de cabecera/detalle para enviar los datos necesarios para crear una transaccion comercial en SAP.
Para saber si lo que se envia es una factura o una orden de venta se debe leer el campo  >> "record_type" enviado como parametro en la peticion.
el cual puede tener los siguiente valores: 
  "saleorder"
  "invoice"

**Ejmplo Python request**

```python
import requests

url = "/api/transaction"

payload = {
  "credentials": {
    "user": "userapi", 
    "password": "pass_api"
  }, 
  "record": {
   "id":"S00008",
   "record_type":"saleorder",
   "fields":[
      {
         "name":"CardCode",
         "value":"CL1039"
      },
      {
         "name":"NumAtCard",
         "value":"S00008"
      },
      {
         "name":"Comments",
         "value":"S00008"
      },
      {
         "name":"DocDate",
         "value":"2022-05-26"
      },
      {
         "name":"DocTotal",
         "value":207.0
      },
      {
         "name":"ShipToCode",
         "value":"Movilway-Entrega"
      }
   ],
   "sublists":[
      {
         "sublist_id":"items",
         "lines":[
            {
               "line_id":"items_21",
               "fields":[
                  {
                     "name":"ItemCode",
                     "value":"SER0032"
                  },
                  {
                     "name":"Quantity",
                     "value":1.0,
                     "type":"float"
                  },
                  {
                     "name":"Price",
                     "value":180.0,
                     "type":"float"
                  },
                  {
                     "name":"WhsCode",
                     "value":"01"
                  },
                  {
                     "name":"DiscPrcnt",
                     "value":0.0,
                     "type":"float"
                  },
                  {
                     "name":"TaxCode",
                     "value":"IVA"
                  }
               ]
            }
         ]
      }
   ]
}
  
}

headers = {
    'content-type': "application/json" 
}

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)
```
Como respuesta se obtiene un id unico de la base de datos el cual sera actualizado en Odoo para dejar trazavilidad

**Ejemplo Respuesta en JSON**
```python
{
  "id_erp": "34567", 
  "code": "0", 
  "message": null
}
```


# ENVIO DE PAGO DE CLIENTE

- POST /payment 

## POST /payment 
El metodo recibe una estructura JSON de cabecera para enviar los datos necesarios para crear una transaccion de pago en SAP.

**Ejmplo Python request**

```python
import requests

url = "/api/payment"

payload = {
  "credentials": {
    "user": "userapi", 
    "password": "pass_api"
  }, 
  "record": {
   "id":"S00008",
   "record_type":"payment",
   "fields":[
      {
         "name":"CardCode",
         "value":"CL1039"
      },
      {
         "name":"TrsfrRef",
         "value":"S00008"
      },
      {
         "name":"DocDate",
         "value":"2022-05-26"
      },
      {
         "name":"TrsfrDate",
         "value":"2022-05-26"
      },
      {
         "name":"TrsfrAcct",
         "value":"200045631"
      },
      {
         "name":"TrsfrSum",
         "value":207.0
      },
   ]
}
  
}

headers = {
    'content-type': "application/json" 
}

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)
```
Como respuesta se obtiene un id unico de la base de datos el cual sera actualizado en Odoo para dejar trazavilidad

**Ejemplo Respuesta en JSON**
```python
{ 
  "id_erp": "34567", 
  "code": "0", 
  "message": null
}
```


# IMPORTACION ESTA DE DESPACHO DE ORDEN DE VENTA

- GET /transaction/status/shipping 

## GET /transaction/status/shipping 
El metodo retorna el estado de despacho de una orden de venta enviado como parametro en el body.
Sed espera recibir las siguientes opciones
  - pending
  - delivery_partial
  - delivery

**Ejmplo Python request**

```python
import requests

url = "/api/transaction/status/shipping"

payload = {
  "credentials": {
    "user": "userapi", 
    "password": "pass_api"
  }, 
  "record": {
    "id": "444567", 
    "record_type": "status_shipping", 
    "fields": []
   }
}

headers = {
    'content-type': "application/json" 
}

response = requests.request("GET", url, data=payload, headers=headers)

print(response.text)
```
Como respuesta se obtiene el estado de despacho de la orden de venta.

**Ejemplo Respuesta en JSON**
```python
{
  "list_data": [{
    "id": "444567", 
    "data": [
      {"status_shipping":"pending"}
     ]
    }], 
  "id_erp": "444567", 
  "code": "0", 
  "message": null
}
```
