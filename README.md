Subsistema_2: Gestión de los vehículos que son propiedad de los clientes y que se reparan y/o revisan en el taller. Cada vehículo estará identificado de forma única por su VIN.

#get: sirven para consultar o solicitar información
#post: ingresar o enviar registros (al rellenar datos)
#put: actualizar un registro (valida respecto a id y actualiza)
#delete: (borra segun el id de un registro)
#options: proporciona la lista de los métodos HTTP soportados por el      endpoint especificado

parameters:
  - $ref: '#/components/parameters/pageParam'->si hay 100 datos y queremos obtener del 10 al 19 se envia el valor 2
  - $ref: '#/components/parameters/orderParam'->el campo por el cual queremos ordenar los resultados (ejem: matricula)
    - $ref: '#/components/parameters/orderingParam'->el orden por el que queremos ordenar (ascendente o descendente)


# SWAGGER-UI
docker run -d -p 8000:8080 --rm --name aos2023_ui -e SWAGGER_JSON=/aos/openapi.yaml -v C:\Users\Alicia\Documents\Uni\2022-2023\SEGUNDO_CUATRI\AOS\p1_subs2\openapi:/aos swaggerapi/swagger-ui

# MOCK
docker run --init --rm -it -p 80:4010 --name aos2023_mock -v C:\Users\Alicia\Documents\Uni\2022-2023\SEGUNDO_CUATRI\AOS\p1_subs2\openapi:/aos stoplight/prism:4 mock --cors -h 0.0.0.0 "/aos/openapi.yaml"


y luego usar: curl -i -v -X GET http://localhost/vehiculos


