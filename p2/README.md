Enunciado:
----------
La consecución de este objetivo se planifica en las siguientes fases:
1. Publicación en un repositorio de código (Github, Gitlab, etc.) de la especificación de la API realizada (y corregida) en la práctica 1. Además, habrá que proporcionar un fichero Dockerfile para construir una imagen de contenedor para desplegar el servicio así como las dependencias del mismo (persistencia, librerías, etc.). La URL del repositorio se publicará en la wiki creada a tal efecto en el Moodle de la asignatura, para que el resto de equipos puedan acceder a él, antes del 9 de mayo a las 9:00. Recuerda que el resto de equipos van a integrar tu servicio, por lo que se valorará la documentación incluida en el repositorio.

2. Publicación de la imagen de contenedor del servicio en Docker Hub. Esto es necesario para la posterior integración del servicio en el despliegue de Kubernetes.

3. Breve memoria descriptiva con esquema de despliegue de todos los servicios, comunicaciones entre ellos, contenedores necesarios para cada uno de ellos y la justificación de todas las decisiones tomadas.

4. Ficheros necesarios para realizar el despliegue de todos los servicios de la aplicación con Docker Compose. (NOTA: Para que el objetivo se considere alcanzado, el despliegue debe funcionar por completo tras ejecutar el comando docker-compose up)

5. Reorganización de los contenedores y servicios para su despliegue en un clúster Kubernetes. (NOTA: Para que el objetivo se considere alcanzado, el despliegue debe funcionar por completo tras ejecutar el comando kubectl apply -f <fichero>)

6. Se valorará la simulación del comportamiento de los servicios mediante el empleo de herramientas de mocking tales como Stoplight Prism y Postman.

7. Se valorará la implementación de la API del servicio que cada grupo especificó en la primera práctica.

8. Se valorará el despliegue de la aplicación completa en una nube pública (Azure, AWS, Google Cloud, etc.). Incluir capturas de pantalla del despliegue en la memoria del paso 3.

Unión de microservicios:
------
1. Crear un  schema en openapi.yaml llamado AllNombreMicroservicio para reunir los schemas de cada microservicio y que se visualice de forma más clara
2. Dividir cada microservicio en un .yaml distinto para poder diferenciarlos mejor
3. Dentro de nuestro openapi.yaml haremos dentro de path referencia a cada uno de los NombreMicroservicio.yaml para acceder a cada endpoint
4. Con el comando: docker compose up, levantaremos todos los contenedores: swagger, stoplight y caddy (proxy)
  
  
Para crear la imagen de nuestro openapi hemos tenido que:
------
1. Crear un Docker file con las reglas necesarias
2. Meter este Dockerfile en el mismo directorio en el que se encuentra openapi.yaml
3. Una vez hecho esto, ya podemos construir la imagen con: docker build -t img_all:v1 -f Dockerfile .
4. Para guardar la imagen creada tendremos que ejecutar: docker save -o img_all_v1.tar img_all:v1
5. Para cargar la imagen desde.tar y registrarla en el sistema Docker local haremos: docker load -i img_all_v1.tar
  
  
Kubernetes:
------
1. Instalar un cluster con el que poder ejecutar Kubernetes, se ha elegido minikube el cual es una herramienta que permite ejecutar un clúster de Kubernetes de un solo nodo en un entorno local.
2. Necesitaremos también la imagen de nuestro openapi subidda a algun repositorio de la nube.
3. Crearemos un fichero .yaml en el cual especificaremos un deployment y un service.
4. Iniciaremos el cluster con minikube start --driver=docker , esto lo haremos para correr el cluster sobre docker, sino podría coger otra forma de emulación como VirtualMachine.
5. Usaremos el comando minikube config set driver docker para indicar que usaremos docker como forma de emulación por defecto, y podremos iniciar el cluster solo con el comando minikube start.
6. Levantaremos el fichero .yaml previamente creado, este levantará un servicio el cual podrá ser accedido desde dentro del cluster, pero no desde fuera, esto s hará con el comando kubectl apply -f <fichero>
7. Para poder acceder a nuestro servicio será necesario proporcionarle una IP externa, esto será hecho con el comando minikube service <nombre servicio>
8. Este ultimo comando nos proporcionará una url con la que poder acceder al servicio desde el navegador o a través de la terminal. En equipos con sistema operativo Windows se nos abrirá el navegador directamente.


