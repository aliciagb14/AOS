FROM swaggerapi/swagger-ui:latest
RUN mkdir /aos
COPY openapi.yaml /aos/
COPY clientes.yaml /aos/
COPY vehiculos.yaml /aos/
COPY trabajos.yaml /aos/
COPY facturas.yaml /aos/
COPY logs.yaml /aos/
COPY notificaciones.yaml /aos/
COPY recambios.yaml /aos/

ENV SWAGGER_JSON=/aos/openapi.yaml
EXPOSE 8080
