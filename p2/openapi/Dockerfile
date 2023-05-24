FROM swaggerapi/swagger-ui:latest
RUN mkdir /aos
COPY openapi.yaml /aos/
ENV SWAGGER_JSON /aos/openapi.yaml
EXPOSE 8080
