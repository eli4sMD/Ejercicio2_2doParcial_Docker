## SWARM CON SERVICIOS SOAP Y REST

**Despliegue de Servicios en Docker Swarm con Enfoque Práctico**

**Descripción del Proyecto:**

Este proyecto se centra en implementar el despliegue de cuatro servicios como parte de un conjunto (**stack**) ejecutándose en un entorno de **Docker Swarm**, que se encarga del balanceo de carga.

1. El primer servicio consiste en una base de datos **MySQL** con una tabla llamada **perfiles**. Dos servicios web, uno utilizando **SOAP** y otro con una **REST API**, se conectan a esta base de datos.

2. El segundo servicio es una **REST API** básica que se conecta a la base de datos y permite la **inserción de nuevos registros** en la tabla **perfiles**.

3. El tercer servicio es un sencillo **Web Service SOAP** que consulta todos los registros almacenados en la tabla **perfiles** de la base de datos.

4. El cuarto servicio consume los dos servicios web mencionados anteriormente. Devuelve una tabla HTML con los datos obtenidos y un formulario para insertar nuevos registros en la tabla.

Cada uno de estos servicios se crea a partir de **imágenes Docker personalizadas**, las cuales se construyen utilizando archivos **Dockerfile** específicos para cada servicio.

## PASO 1 Crear las imagenes (debera ingresar en las respectivas carpetas)

## en apiRest
`docker build . -t restapi`
## en apiSoap
`docker build . -t soapapi`
## en client
`docker build . -t client`
## en mysql
`docker build . -t mysql-image`

## PASO 2 Desplegar los servicios con swarm(en carpeta raiz)

`docker swarm init`

`docker stack deploy -c docker-compose.yml app`

## Aclaraciones

Se creo el servidor SOAP en el puerto 4000

El servidor web se encuentra alojado en localhost:8080

**Desmontar y Limpiar:**

6. **Eliminar Stack y Servicios:**
   ```bash
   docker stack rm app
   ```

7. **Eliminar Imágenes (Opcional):**
   ```bash
   docker rmi cliente:web rest:ws soap:ws mysql:img
   ```