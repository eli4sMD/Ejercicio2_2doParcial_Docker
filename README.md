**Despliegue de Servicios en Docker Swarm con Enfoque Práctico**

**Descripción del Proyecto:**

Este proyecto se centra en implementar el despliegue de cuatro servicios como parte de un conjunto (**stack**) ejecutándose en un entorno de **Docker Swarm**, que se encarga del balanceo de carga.

1. El primer servicio consiste en una base de datos **MySQL** con una tabla llamada **perfiles**. Dos servicios web, uno utilizando **SOAP** y otro con una **REST API**, se conectan a esta base de datos.

2. El segundo servicio es una **REST API** básica que se conecta a la base de datos y permite la **inserción de nuevos registros** en la tabla **perfiles**.

3. El tercer servicio es un sencillo **Web Service SOAP** que consulta todos los registros almacenados en la tabla **perfiles** de la base de datos.

4. El cuarto servicio consume los dos servicios web mencionados anteriormente. Devuelve una tabla HTML con los datos obtenidos y un formulario para insertar nuevos registros en la tabla.

Cada uno de estos servicios se crea a partir de **imágenes Docker personalizadas**, las cuales se construyen utilizando archivos **Dockerfile** específicos para cada servicio.

**Requerimientos:**

- Docker Desktop
- Entorno Node.js
- Clonar este repositorio

**Pasos para el Despliegue(los siguientes comandos se pueden ejecutar desde la carpeta raiz del proyecto):**

1. **Inicializar Docker Swarm:**
   ```bash
   docker swarm init
   ```

2. **Construir Imágenes:**
   - MySQL:
     ```bash
     docker build -t mysql:img ./imagenMysql/
     ```
   - Servicio Web SOAP:
     ```bash
     docker build -t soap:ws ./soap-service/
     ```
   - REST API:
     ```bash
     docker build -t rest:ws ./rest-service/
     ```
   - Aplicación Cliente:
     ```bash
     docker build -t cliente:web ./app-cliente/
     ```

3. **Desplegar Stack en Docker Swarm:**
   ```bash
   docker stack deploy -c docker-stack-compose.yml app
   ```

4. **Verificar Servicios:**
   ```bash
   docker service ls
   ```

5. **Realizar Pruebas:**
   Abrir un navegador y acceder a: "http://localhost:3000"

**Desmontar y Limpiar:**

6. **Eliminar Stack y Servicios:**
   ```bash
   docker stack rm app
   ```

7. **Eliminar Imágenes (Opcional):**
   ```bash
   docker rmi cliente:web rest:ws soap:ws mysql:img
   ```

**Nota:**
- Puedes ejecutar los comandos desde el paso 2 tantas veces como desees sin problemas.
- Este enfoque práctico facilita la creación, despliegue y limpieza de servicios en un entorno Docker Swarm.
