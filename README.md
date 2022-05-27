# API PARA NEXTCONNECTOR
El siguiente documento pretende detallar  las APIS de SAP S/4 HANA que necesita el conector de Odoo para el correcto funcionamiento de la integración.

# CLIENTES 

- GET /customers 
- GET /customer

## GET /customers
El método retorna el listado de clientes que hay que importar a Odoo

**Ejemplo Python request**

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
Como respuesta se obtiene un listado de códigos de clientes por sincronizar a Odoo, estos códigos serán utilizados 
en el llamado del siguiente método. 

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
El método retorna los datos/campos de un cliente especifico que se envíen como parámetro en el body.

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
Como respuesta se obtiene los campos del cliente que deben ser registrados en el cliente que se está consultando para sincronizar a Odoo

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




# ARTICULOS 

- GET /items 
- GET /item

## GET /items
El método retorna el listado de artículos que hay que importar a Odoo

**Ejemplo Python request**

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
Como respuesta se obtiene un listado de códigos de artículos por sincronizar a Odoo, estos códigos serán utilizados 
en el llamado del siguiente método. 

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
El método retorna los datos/campos de un artículo especifico que se envíen como parámetro en el body.

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



# STOCK 

- GET /stock 

## GET /stock
El método retorna el listado de artículos con su cantidad de stock disponible

**Ejemplo Python request**

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
Como respuesta se obtiene un listado de códigos de artículos con su cantidad de stock disponible.

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



# LISTAS DE PRECIOS

- GET /listprices 
- GET /listprice

## GET /listprices
El método retorna el listado de listas de precios a sincronizar en Odoo

**Ejemplo Python request**

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
Como respuesta se obtiene un listado de listas de precios por sincronizar a Odoo, estos códigos serán utilizados 
en el llamado del siguiente método. 

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
El método retorna una lista de artículos y su precio. Recibe como parámetro un código de lista precios para filtrar el resultado

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
Como respuesta se obtiene el listado de artículos con su precio. 

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


# RESUMEN ESTADO DE CUENTA 

- GET /customer/balance 

## GET /customer/balance 
El método retorna la información de la deuda y limite de crédito del cliente.

**Ejemplo Python request**

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
Como respuesta se obtiene la información de la deuda y limite de crédito del cliente.

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

# ENVIO DE CLIENTE

- POST /customer 

## POST /customer 
El método recibe una estructura JSON de cabecera/detalle para leer los datos necesarios para crear/actualizar un cliente en SAP.
Dentro de la misma estructura se puede enviar un detalle de direcciones de entrega, direcciones de facturación y contactos. 

**Ejemplo Python request**

```python
import requests

url = "/api/customr"

payload = {
  "credentials": {
    "user": "userapi", 
    "password": "pass_api"
  }, 
  "record": {
      "id":"CL1039",
      "record_type":"customer",
      "fields":[
          {
            "name":"CardType",
            "value":0,
            "type":"enum",
            "enumtype":"BoCardTypes"
          },
          {
            "name":"CardCode",
            "value":"CL1039"
          },
          {
            "name":"CardName",
            "value":"Movilway Nicaragua, S.A."
          },
          {
            "name":"LicTradNum",
            "value":"J0310000189706"
          },
          {
            "name":"E_Mail",
            "value":""
          },
          {
            "name":"Phone1",
            "value":""
          }
      ],
      "sublists":[
          {
            "sublist_id":"address",
            "lines":[
                {
                  "line_id":"address_1",
                  "fields":[
                      {
                        "name":"AdresType",
                        "value":"delivery"
                      },
                      {
                        "name":"AddressLabel",
                        "value":"Managua"
                      },
                      {
                        "name":"Street",
                        "value":"Semaforos Villa Fontana 1c Este 75mts al Norte, Edificio OPUS III, 3er Nivel."
                      },
                      {
                        "name":"City",
                        "value":""
                      },
                      {
                        "name":"State",
                        "value":""
                      },
                      {
                        "name":"Country",
                        "value":"NI"
                      }
                  ]
                },
                {
                  "line_id":"address_1",
                  "fields":[
                      {
                        "name":"AdresType",
                        "value":"billing"
                      },
                      {
                        "name":"AddressLabel",
                        "value":"Movilway Nicaragua-Entrega"
                      },
                      {
                        "name":"Street",
                        "value":"Semaforos Villa Fontana 1c Este 75mts al Norte, Edificio OPUS III, 3er Nivel."
                      },
                      {
                        "name":"City",
                        "value":""
                      },
                      {
                        "name":"State",
                        "value":""
                      },
                      {
                        "name":"Country",
                        "value":"NI"
                      }
                  ]
                }
            ]
          },
          {
            "sublist_id":"contacts",
            "lines":[
                {
                  "line_id":"contact_1",
                  "fields":[
                      {
                        "name":"Name",
                        "value":"Roxana Joselyn Rodriguez Gomez"
                      },
                      {
                        "name":"E_MailL",
                        "value":"rjrodriguezg@movilway.com"
                      },
                      {
                        "name":"Tel1",
                        "value":"7602-2222"
                      },
                      {
                        "name":"FirstName",
                        "value":"Roxana"
                      },
                      {
                        "name":"MiddleName",
                        "value":"Joselyn"
                      },
                      {
                        "name":"LastName",
                        "value":"Rodriguez Gomez"
                      },
                      {
                        "name":"Position",
                        "value":"Recursos Humanos"
                      },
                      {
                        "name":"Address",
                        "value":"Roxana Joselyn Rodriguez Gomez"
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
Como respuesta se obtiene un id único de la base de datos el cual sera actualizado en Odoo para dejar trazabilidad. 
Si el cliente se esta creando por primera vez no se envía el campo "id", en caso se le envíe el campo "id" se asumen que el cliente existe y sera actualizado.

**Ejemplo Respuesta en JSON**
```python
{ 
  "id_erp": "CL1039", 
  "code": "0", 
  "message": null
}
```

# ENVIO DE PEDIDO Y FACTURA

- POST /transaction 

## POST /transaction 
El método recibe una estructura JSON de cabecera/detalle para leer los datos necesarios para crear una transacción comercial en SAP.
Para saber si lo que se envía es una factura o una orden de venta se debe leer el campo  >> "record_type" enviado como parámetro en la petición.
el cual puede tener los siguiente valores: 
  "saleorder"
  "invoice"

**Ejemplo Python request**

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
Como respuesta se obtiene un id único de la base de datos el cual sera actualizado en Odoo para dejar trazabilidad

**Ejemplo Respuesta en JSON**
```python
{
  "id_erp": "34567", 
  "code": "0", 
  "message": null
}
```


# ENVIO DE PAGO

- POST /payment 

## POST /payment 
El método recibe una estructura JSON de cabecera para leer los datos necesarios para crear una transacción de pago en SAP.

**Ejemplo Python request**

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
Como respuesta se obtiene un id único de la base de datos el cual sera actualizado en Odoo para dejar trazabilidad

**Ejemplo Respuesta en JSON**
```python
{ 
  "id_erp": "34567", 
  "code": "0", 
  "message": null
}
```


# ESTADO DE DESPACHO DE PEDIDO

- GET /transaction/status/shipping 

## GET /transaction/status/shipping 
El método retorna el estado de despacho de una orden de venta enviado como parámetro en el body.
Sed espera recibir las siguientes opciones
  - pending
  - delivery_partial
  - delivery

**Ejemplo Python request**

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


# FACTURAS Y NOTAS DE CREDITO

- GET /transactions 
- GET /transaction

## GET /transactions
El método retorna el listado documentos generados a partir de una fecha enviada.

**Ejmplo Python request**

```python
import requests

url = "/api/records/transactions"

payload = {
  "credentials": {
    "user": "userapi", 
    "password": "pass_api"
  }, 
  "record": {
    "id": "", 
    "record_type": "transactions", 
    "fields": [
      {"date_from": "2022-05-05"}
    ]
   }
}

headers = {
    'content-type': "application/json" 
}

response = requests.request("GET", url, data=payload, headers=headers)

print(response.text)
```
Como respuesta se obtiene un listado de listas de precios por sincronizar a Odoo, estos códigos serán utilizados 
en el llamado del siguiente método. 

**Ejemplo Respuesta en JSON**
```python
{
  "list_data": [{
    "id": "transactions", 
    "data": [
      {id:'34567', "record_type": "invoice"},
      {id:'34568', "record_type": "creditnote"},
      {id:'34569', "record_type": "creditnote"},
    ]}
  ], 
  "id_erp": null, 
  "code": "0", 
  "message": null
}
```

## GET /transaction
El método retorna en una estructura JSON de cabecera/detalle con la información necesaria para crear el documento comercial en Odoo

**Ejemplo Python request**
```python
import requests

url = "/api/records/transaction"

payload = {
  "credentials": {
    "user": "userapi", 
    "password": "pass_api"
  }, 
  "record": {
    "id": "34567", 
    "record_type": "invoice", 
    "fields": []
   }
}

headers = {
    'content-type': "application/json" 
}

response = requests.request("GET", url, data=payload, headers=headers)

print(response.text)
```
Como respuesta se obtiene el listado de artículos con su precio. 

**Ejemplo Respuesta en JSON**
```python
{
  "list_data": [{
    "id": "34567", 
    "data": [
          {
          "id":"34567",
          "record_type":"invoice",
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
                            "name":"LineTotal",
                            "value":180,
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
     ]
    }], 
  "id_erp": "34567", 
  "code": "0", 
  "message": null
}
```