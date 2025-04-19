

# ENDPOINTS USANDO JSON:API

## Endpoint de cambio de estado para el registro de la visita del vendedor 


```bash
curl -X 'PATCH' \
  'http://127.0.0.1:8080/api/customer_visits/2/' \
  -H 'accept: application/vnd.api+json' \
  -H 'Content-Type: application/json' \
  -d '{
  "data": {
    "attributes": {
      "status": "completed"
    },
    "type": "CustomerVisit",
    "id": "2"
  }
}'
```

### Respuesta

```json
{
  "data": {
    "attributes": {
      "created_at": 1680000700,
      "customer_id": 2,
      "notes": "Visita para evaluar el servicio postventa.",
      "outcomes": "Retroalimentaci\u00f3n positiva, solicitar mayor informaci\u00f3n.",
      "salesperson_id": 11,
      "status": "completed",
      "updated_at": 1680000700,
      "visit_date": 1680000700
    },
    "id": "2",
    "links": {
      "self": "/api/customer_visits/2/"
    },
    "relationships": {
      "customer": {
        "data": null,
        "links": {
          "self": "/api/customer_visits/2/customer"
        }
      }
    },
    "type": "CustomerVisit"
  },
  "included": [],
  "jsonapi": {
    "version": "1.0"
  },
  "links": {
    "self": "/api/customer_visits/2/"
  },
  "meta": {
    "count": 1,
    "instance_meta": {},
    "limit": 250,
    "total": 1
  }
}
```


## Endpoint para listar las visitas a cliente de un vendedor 
### Ejemplo:

- customer_id = 1
- salesperson_id = 10


```bash
curl -X 'GET' \
  'http://127.0.0.1:8080/api/customer_visits/?include=customer&fields%5BCustomerVisit%5D=salesperson_id%2Ccustomer_id%2Cvisit_date%2Cstatus%2Cnotes%2Coutcomes%2Ccreated_at%2Cupdated_at&page%5Boffset%5D=0&page%5Blimit%5D=10&sort=id&filter%5Bsalesperson_id%5D=10&filter%5Bcustomer_id%5D=1' \
  -H 'accept: application/vnd.api+json' \
  -H 'Content-Type: application/json'
```

### RESPUESTA

```json
{
  "data": [
    {
      "attributes": {
        "created_at": 1743735322,
        "customer_id": 1,
        "notes": "Visita para evaluar el servicio postventa.",
        "outcomes": "Retroalimentaci\u00f3n positiva, solicitar mayor informaci\u00f3n.",
        "salesperson_id": 10,
        "status": "scheduled",
        "updated_at": 1743735322,
        "visit_date": 1680000600
      },
      "id": "3",
      "links": {
        "self": "/api/customer_visits/3/"
      },
      "relationships": {
        "customer": {
          "data": {
            "id": "1",
            "type": "Customer"
          },
          "links": {
            "self": "/api/customer_visits/3/customer"
          }
        }
      },
      "type": "CustomerVisit"
    }
  ],
  "included": [
    {
      "attributes": {
        "address": "Cra. 16a #85 34 Piso 2, Chapinero, Bogot\u00e1, Cundinamarca",
        "business_name": "Empresa Gamma",
        "business_type": "Retail",
        "country": "Colombia",
        "created_at": 1680000000,
        "credit_limit": 10000.0,
        "payment_terms": "Net 30",
        "salesperson_id": 0,
        "tax_id": "TAX123",
        "updated_at": 1680000000,
        "user_id": 1
      },
      "id": "1",
      "links": {
        "self": "/api/customers/1/"
      },
      "relationships": {
        "segment_assignments": {
          "data": [],
          "links": {
            "self": "/api/customers/1/segment_assignments"
          }
        },
        "visits": {
          "data": [],
          "links": {
            "self": "/api/customers/1/visits"
          }
        }
      },
      "type": "Customer"
    }
  ],
  "jsonapi": {
    "version": "1.0"
  },
  "links": {
    "self": "/api/customer_visits/?include=customer&fields[CustomerVisit]=salesperson_id,customer_id,visit_date,status,notes,outcomes,created_at,updated_at&sort=id&filter[salesperson_id]=10&filter[customer_id]=1&page[offset]=0&page[limit]=10"
  },
  "meta": {
    "count": 1,
    "limit": 10,
    "total": 1
  }
}
```



## Endpoint para consultar ruta de visita por fecha - debe tener direcciones reales

### Ejemplo:

- customer_id = 1
- salesperson_id = 10
- visit_date = 1680000600

```bash
curl -X 'GET' \
  'http://127.0.0.1:8080/api/customer_visits/?include=customer&fields%5BCustomerVisit%5D=salesperson_id%2Ccustomer_id%2Cvisit_date%2Cstatus%2Cnotes%2Coutcomes%2Ccreated_at%2Cupdated_at&page%5Boffset%5D=0&page%5Blimit%5D=10&sort=id&filter%5Bsalesperson_id%5D=10&filter%5Bvisit_date%5D=1680000600' \ 
  -H 'accept: application/vnd.api+json' \
  -H 'Content-Type: application/json'
```

### RESPUESTA

```json
{
  "data": [
    {
      "attributes": {
        "created_at": 1680000600,
        "customer_id": 2,
        "notes": "Reuni\u00f3n para discutir nuevos productos.",
        "outcomes": "Inter\u00e9s alto, seguimiento programado.",
        "salesperson_id": 10,
        "status": "completed",
        "updated_at": 1745038419,
        "visit_date": 1680000600
      },
      "id": "1",
      "links": {
        "self": "/api/customer_visits/1/"
      },
      "relationships": {
        "customer": {
          "data": {
            "id": "2",
            "type": "Customer"
          },
          "links": {
            "self": "/api/customer_visits/1/customer"
          }
        }
      },
      "type": "CustomerVisit"
    },
    {
      "attributes": {
        "created_at": 1743735322,
        "customer_id": 1,
        "notes": "Visita para evaluar el servicio postventa.",
        "outcomes": "Retroalimentaci\u00f3n positiva, solicitar mayor informaci\u00f3n.",
        "salesperson_id": 10,
        "status": "scheduled",
        "updated_at": 1743735322,
        "visit_date": 1680000600
      },
      "id": "3",
      "links": {
        "self": "/api/customer_visits/3/"
      },
      "relationships": {
        "customer": {
          "data": {
            "id": "1",
            "type": "Customer"
          },
          "links": {
            "self": "/api/customer_visits/3/customer"
          }
        }
      },
      "type": "CustomerVisit"
    }
  ],
  "included": [
    {
      "attributes": {
        "address": "Cra. 16a #85 34 Piso 2, Chapinero, Bogot\u00e1, Cundinamarca",
        "business_name": "Empresa Gamma",
        "business_type": "Retail",
        "country": "Colombia",
        "created_at": 1680000000,
        "credit_limit": 10000.0,
        "payment_terms": "Net 30",
        "salesperson_id": 0,
        "tax_id": "TAX123",
        "updated_at": 1680000000,
        "user_id": 1
      },
      "id": "1",
      "links": {
        "self": "/api/customers/1/"
      },
      "relationships": {
        "segment_assignments": {
          "data": [],
          "links": {
            "self": "/api/customers/1/segment_assignments"
          }
        },
        "visits": {
          "data": [],
          "links": {
            "self": "/api/customers/1/visits"
          }
        }
      },
      "type": "Customer"
    },
    {
      "attributes": {
        "address": "Cl. 163 #15-82, Bogot\u00e1",
        "business_name": "Empresa Beta",
        "business_type": "Wholesale",
        "country": "Colombia",
        "created_at": 1680000100,
        "credit_limit": 20000.0,
        "payment_terms": "Net 45",
        "salesperson_id": 0,
        "tax_id": "TAX456",
        "updated_at": 1680000100,
        "user_id": 2
      },
      "id": "2",
      "links": {
        "self": "/api/customers/2/"
      },
      "relationships": {
        "segment_assignments": {
          "data": [],
          "links": {
            "self": "/api/customers/2/segment_assignments"
          }
        },
        "visits": {
          "data": [],
          "links": {
            "self": "/api/customers/2/visits"
          }
        }
      },
      "type": "Customer"
    }
  ],
  "jsonapi": {
    "version": "1.0"
  },
  "links": {
    "self": "/api/customer_visits/?include=customer&fields[CustomerVisit]=salesperson_id,customer_id,visit_date,status,notes,outcomes,created_at,updated_at&sort=id&filter[salesperson_id]=10&filter[visit_date]=1680000600&page[offset]=0&page[limit]=10"
  },
  "meta": {
    "count": 2,
    "limit": 10,
    "total": 2
  }
}
```





# ENDPOINTS USANDO API RPC


## 1. Cambiar estado a 'completed'

```bash
curl -X PATCH http://localhost:8080/api/visit/1/status \
     -H "Content-Type: application/json" \
     -d '{"status": "completed"}'
```

### RESPUESTA

```json
{
  "id": 1,
  "status": "completed"
}
```

## 2. Listar visitas de vendedor 10 a un cliente 1

```bash
curl -X GET "http://localhost:8080/api/visits?salespersonId=10&customerId=1"
```


### RESPUESTA

```json
[
  {
    "customer_id": 1,
    "id": 3,
    "notes": "Visita para evaluar el servicio postventa.",
    "status": "scheduled",
    "visit_date": 1680000600
  }
]

```

## 3. Obtener ruta de visitas del 2023‑03‑28 para vendedor 10

```bash
curl -X GET "http://localhost:8080/api/visits/route?salespersonId=10&date=2023-03-28"
```

### RESPUESTA

```json
[
  {
    "customer": {
      "address": "Cra. 16a #85 34 Piso 2, Chapinero, Bogot\u00e1, Cundinamarca",
      "country": "Colombia",
      "id": 1,
      "name": "Empresa Gamma"
    },
    "status": "scheduled",
    "visit_id": 3,
    "visit_time": 1680000600
  },
  {
    "customer": {
      "address": "Cl. 163 #15-82, Bogot\u00e1",
      "country": "Colombia",
      "id": 2,
      "name": "Empresa Beta"
    },
    "status": "completed",
    "visit_id": 1,
    "visit_time": 1680000600
  }
]
```
