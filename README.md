# Docker---Conceptos-b-sicos
Este repositorio almacena los conceptos básicos para empezar en el mundo de docker.

## Tabla de contenidos

  - [Introducción](#introducción)
    - [Objetivo](#objetivo)
    - [¿Qué es Docker?](#¿qué-es-docker?)
    - [¿Por qué usar Docker?](#¿por-qué-usar-docker?)
    - [¿A quién va dirigida esta guía?](#¿a-quién-va-dirigida-esta-guía?)
    - [¿Qué necesitas para comenzar?](#¿qué-necesitas-para-comenzar?)
  - [Instalación](#instalación)
  - [Conceptos Básicos de Docker](#conceptos-básicos-de-docker)
    - [Objetivo](#objetivo)
    - [Conceptos clave](#conceptos-clave)
    - [¿Qué es una imagen?](#¿qué-es-una-imagen?)
    - [¿Qué es un contenedor?](#¿qué-es-un-contenedor?)
      - [Buenas prácticas](#buenas-prácticas)
      - [Errores comunes](#errores-comunes)
    - [¿Qué es un Dockerfile?](#¿qué-es-un-dockerfile?)
    - [¿Qué son las capas?](#¿qué-son-las-capas?)
    - [¿Qué es un volumen?](#¿qué-es-un-volumen?)
      - [Uso del comando “volume create” de Docker](#uso-del-comando-“volume-create”-de-docker)
        - [Paso 1. Crear y nombrar el volumen](#paso-1.-crear-y-nombrar-el-volumen)
        - [Paso 2. Usar el volume en un contenedor de Docker](#paso-2.-usar-el-volume-en-un-contenedor-de-docker)
        - [Paso 3. Listar los volumes](#paso-3.-listar-los-volumes)
        - [Paso 4. Inspeccionar el volume](#paso-4.-inspeccionar-el-volume)
        - [Paso 5. Eliminar el volume](#paso-5.-eliminar-el-volume)
  - [Crear y compartir `Docker Images`](#crear-y-compartir-`docker-images`)
    - [Container Registry](#container-registry)
      - [Ejemplo:](#ejemplo:)
      - [Buenas prácticas](#buenas-prácticas)
      - [Errores comunes](#errores-comunes)
  - [Docker Compose](#docker-compose)
    - [Objetivo](#objetivo)
    - [Conceptos clave](#conceptos-clave)
    - [Explicación detallada](#explicación-detallada)
    - [Estructura básica de un `docker-compose.yml`](#estructura-básica-de-un-`docker-compose.yml`)
    - [Ejemplo completo: app con Flask + PostgreSQL](#ejemplo-completo:-app-con-flask-+-postgresql)
      - [Buenas prácticas](#buenas-prácticas)
  - [Visualización de logs con `docker logs`](#visualización-de-logs-con-`docker-logs`)
    - [Objetivo](#objetivo)
    - [Conceptos clave](#conceptos-clave)
    - [¿Qué hace `docker logs`?](#¿qué-hace-`docker-logs`?)
    - [Sintaxis básica](#sintaxis-básica)
    - [Comandos básicos](#comandos-básicos)
  - [Persistencia de datos y volúmenes en Docker](#persistencia-de-datos-y-volúmenes-en-docker)
    - [Objetivo](#objetivo)
    - [Conceptos clave](#conceptos-clave)
    - [Explicación detallada](#explicación-detallada)
      - [Bind Mounts](#bind-mounts)
        - [Ventajas:](#ventajas:)
        - [Desventajas:](#desventajas:)
      - [Named Volumes](#named-volumes)
        - [Ventajas:](#ventajas:)
        - [Desventajas:](#desventajas:)
    - [Ejemplo práctico](#ejemplo-práctico)
  - [Docker en flujos DevOps y CI/CD](#docker-en-flujos-devops-y-ci/cd)
    - [Objetivo](#objetivo)
    - [Conceptos clave](#conceptos-clave)
    - [Explicación detallada](#explicación-detallada)
    - [Buenas prácticas](#buenas-prácticas)
    - [Errores comunes](#errores-comunes)
  - [Redes en Docker: Conectando contenedores](#redes-en-docker:-conectando-contenedores)
    - [Objetivo](#objetivo)
    - [Conceptos clave](#conceptos-clave)
    - [Explicación detallada](#explicación-detallada)
      - [1. Bridge Network (la más común)](#1.-bridge-network-(la-más-común))
        - [Ejemplo](#ejemplo)
      - [2. Host Network](#2.-host-network)
        - [Limitaciones](#limitaciones)
      - [Ventajas:](#ventajas:)
        - [Desventajas:](#desventajas:)
      - [3. Overlay Network (en Swarm)](#3.-overlay-network-(en-swarm))
        - [Caracteristicas destacadas](#caracteristicas-destacadas)
          - [Gestión de clústeres integrada con Docker Engine](#gestión-de-clústeres-integrada-con-docker-engine)
          - [Diseño descentralizado](#diseño-descentralizado)
          - [Modelo de servicio declarativo](#modelo-de-servicio-declarativo)
          - [Escalada](#escalada)
          - [Conciliación del estado deseado](#conciliación-del-estado-deseado)
          - [Redes multihost](#redes-multihost)
          - [Descubrimiento de servicios](#descubrimiento-de-servicios)
          - [Equilibrio de carga](#equilibrio-de-carga)
          - [Seguro por defecto](#seguro-por-defecto)
      - [Ejemplo práctico](#ejemplo-práctico)
      - [Docker Compose y redes automáticas](#docker-compose-y-redes-automáticas)
      - [Diferencias entre Docker y Docker Swarm](#diferencias-entre-docker-y-docker-swarm)
      - [¿Cuándo usar Docker Swarm?](#¿cuándo-usar-docker-swarm?)

## Introducción

### Objetivo
El objetivo de esta sección es entender ¿Qué es Docker? de donde viene y porque nos puede interesar el utilizarlo.

### ¿Qué es Docker?  
Docker es una plataforma que permite empaquetar aplicaciones y sus dependencias en contenedores, que son entornos ligeros, portables y consistentes. Los contenedores permiten que el software se ejecute de la misma forma en distintos entornos (desarrollo, testing, producción), eliminando problemas como “en mi máquina sí funciona”.

### ¿Por qué usar Docker?
- Facilita la consistencia entre entornos.
- Acelera la configuración y el despliegue de entornos.
- Permite el aislamiento de servicios.
- Facilita el escalado y despliegue continuo.

###  ¿A quién va dirigida esta guía?

- **Desarrolladores** que necesiten ambientes reproducibles y consistentes.
- **QA y testers** que deseen levantar entornos fácilmente para pruebas.
- **Equipos de infraestructura/DevOps** que quieran contenerizar aplicaciones para facilitar despliegues.
- **Nuevos miembros del equipo** que necesiten una referencia clara para integrarse rápidamente.
### ¿Qué necesitas para comenzar?

- Conocimientos básicos de línea de comandos.
- Tener instalado Docker Desktop (Windows/macOS) o Docker Engine (Linux).
- Ganas de aprender una herramienta poderosa para el desarrollo moderno

## Instalación 
La instalación puede seguirse desde la [Documentación Oficial](https://docs.docker.com/engine/installation/).

---

## Conceptos Básicos de Docker

### Objetivo
Entender los componentes esenciales de Docker: imágenes, contenedores, capas, Dockerfile, volúmenes y registros. Esta base conceptual es fundamental para usar Docker de manera efectiva.
### Conceptos clave
- **Imagen (Image):** plantilla de solo lectura que contiene todo lo necesario para ejecutar una aplicación.
- **Contenedor (Container):** instancia ejecutable de una imagen.
- **Dockerfile:** archivo de instrucciones para construir imágenes.
- **Capa (Layer):** cada instrucción del Dockerfile crea una nueva capa que se apila.
- **Volumen (Volume):** mecanismo para guardar datos persistentes fuera del contenedor.
- **Registro (Registry):** repositorio donde se almacenan y comparten imágenes, como Docker Hub.
### ¿Qué es una imagen?
Una **imagen de Docker** es como una receta o plantilla. Incluye:
- El sistema operativo base (generalmente minimalista)
- Archivos de aplicación
- Dependencias (librerías, binarios, etc.)
- Variables de entorno y configuraciones

Ejemplo: una imagen de Python puede traer ya preinstalado Python 3.10 y pip.

> [!NOTE]
> Las imágenes no cambian; son de **solo lectura**.


### ¿Qué es un contenedor?
Un **contenedor** es una **instancia en ejecución de una imagen**.  
Cuando ejecutas una imagen, Docker la convierte en un contenedor que corre de forma aislada del resto del sistema.
Ejemplo:
```bash
docker run python:3.10

---
## Ciclo de vida de un contenedor de Docker

### Objetivo
Comprender cómo funciona el ciclo de vida de un contenedor en Docker, desde su creación hasta su eliminación, y cómo interactuar con él en cada etapa.
### Conceptos clave

- **Imagen:** Archivo inmutable que contiene el sistema de archivos y la configuración necesarios para ejecutar una aplicación.
- **Contenedor:** Instancia ejecutable de una imagen.
- **Estado de un contenedor:** Puede estar *creado*, *en ejecución*, *detenido*, *pausado*, o *eliminado*.

### Explicación detallada

El ciclo de vida de un contenedor se puede entender como una serie de estados por los que pasa desde que es creado hasta que es eliminado. Aquí se describe el flujo más común:

1. **Creación (`Created`)**
   - Se genera una instancia de la imagen, pero aún no se está ejecutando.
   - Comando: `docker create`

2. **Ejecución (`Running`)**
   - El contenedor está activo y ejecutando su proceso principal.
   - Comando: `docker run` o `docker start`

3. **Pausado (`Paused`)**
   - El contenedor se congela temporalmente (no consume CPU, pero sigue en memoria).
   - Comando: `docker pause` y `docker unpause`

4. **Detenido (`Exited`)**
   - El contenedor terminó su ejecución, ya sea por éxito, error o detención manual.
   - Comando: `docker stop`, `docker kill`, o el proceso interno terminó.

5. **Eliminación (`Removed`)**
   - El contenedor y sus recursos asociados se eliminan del sistema.
   - Comando: `docker rm`

### Ejemplo práctico

```bash
$ docker create -P --expose=8001 python:2.7 python -m SimpleHTTPServer 8001
  a842945e2414132011ae704b0c4a4184acc4016d199dfd4e7181c9b89092de13
$ docker ps -a
  CONTAINER ID IMAGE      COMMAND              CREATED       ... NAMES
  a842945e2414 python:2.7 "python -m SimpleHTT 8 seconds ago ... fervent_hodgkin
$ docker start a842945e2414
  a842945e2414
$ docker ps
  CONTAINER ID IMAGE      COMMAND              ... NAMES
  a842945e2414 python:2.7 "python -m SimpleHTT ... fervent_hodgkin
  ```
  
Siguiendo el ejemplo, para detener el contenedor se puede ejecutar cualquiera de los siguientes comandos:

```bash
docker kill a842945e2414 # (envía SIGKILL)
```

```bash
docker stop a842945e2414 # (envía SIGTERM).
```

Así mismo, pueden reiniciarse:
```bash
docker restart a842945e2414
```

o destruirse:
```bash
docker rm a842945e2414
```
####  Buenas prácticas

- Asigna nombres a tus contenedores con `--name` para facilitar su gestión.
- Usa `--rm` si el contenedor es temporal y deseas que se elimine automáticamente al terminar.
- Detén los contenedores antes de eliminarlos (aunque `docker rm -f` también los forzará).

#### Errores comunes
- **No detener contenedores que ya no usas:** puede consumir recursos innecesarios.
- **Confundir contenedor con imagen:** eliminar el contenedor no borra la imagen original.
- **Olvidar eliminar contenedores `Exited`:** pueden acumularse con el tiempo.

### ¿Qué es un Dockerfile?
Un `Dockerfile` es un archivo de texto, que describe los pasos (secuenciales) a seguir para preparar una imagen Docker. Esto incluye instalación de paquetes, creación de directorios, definición de variables de entorno, ETC. Toda imagen que creemos, parte de una _base image_. 

```dockerfile
FROM node:18
COPY . /app
WORKDIR /app
RUN npm install
CMD ["npm", "start"]
```

Esto crea una imagen que corre una app Node.js con base en la imagen oficial de Node.
En donde:

| Instrucción           | Descripción                                                                                                                                                                                                          |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `FROM <image>`        | Define una base para tu imagen<br>                                                                                                                                                                                   |
| `RUN <command>`       | Ejecuta cualquier comando en una nueva capa sobre la imagen actual y confirma el resultado. `RUN`También tiene un formato de shell para ejecutar comandos.                                                           |
| `WORKDIR <direcotry>` | Establece el directorio de trabajo para cualquier instrucción `RUN`, `CMD`, `ENTRYPOINT`, `COPY`y `ADD`que le siga en el Dockerfile                                                                                  |
| `COPY <src> <dest>`   | Copia nuevos archivos o directorios `<src>`y los agrega al sistema de archivos del contenedor en la ruta `<dest>`.                                                                                                   |
| `CMD <command>`       | Permite definir el programa predeterminado que se ejecuta al iniciar el contenedor según esta imagen. Cada Dockerfile solo tiene un archivo , y solo se respeta `CMD`la última instancia cuando existen varios.`CMD` |

### ¿Qué son las capas?
Docker Las capas forman un concepto fundamental en Docker, desempeñando un papel crucial en la gestión eficiente de los contenedores y sus imágenes. A Docker La imagen se compone de una serie de capas, donde cada capa representa modificaciones o adiciones a la anterior.

Cada capa de una imagen contiene un conjunto de cambios en el sistema de archivos: adiciones, eliminaciones o modificaciones. Veamos una imagen teórica:

1. La primera capa agrega comandos básicos y un administrador de paquetes, como apt.
2. La segunda capa instala un entorno de ejecución de Python y pip para la gestión de dependencias.
3. La tercera capa copia el archivo requirements.txt específico de la aplicación.
4. La cuarta capa instala las dependencias específicas de esa aplicación.
5. La quinta capa copia el código fuente real de la aplicación.

Este ejemplo podría verse así:
![[docker_capas.png]]

Esto es beneficioso porque permite reutilizar capas entre imágenes. Por ejemplo, imagina que quieres crear otra aplicación Python. Gracias a la superposición, puedes aprovechar la misma base de Python. Esto agilizará las compilaciones y reducirá la cantidad de almacenamiento y ancho de banda necesarios para distribuir las imágenes. La superposición de imágenes podría ser similar a la siguiente:
![[docker_capas_2.png]]
Las capas le permiten ampliar imágenes de otros reutilizando sus capas base, lo que le permite agregar solo los datos que su aplicación necesita.

**Ventajas**:
- Las capas se **reutilizan** para acelerar la construcción.
- Las capas inferiores no se vuelven a generar si no cambian.

### ¿Qué es un volumen?
Un volumen de contenedor permite conservar los datos, aunque se elimine el Docker container. Los volúmenes también permiten un intercambio práctico de datos entre el host y el container.

Crear un volumen de Docker es una buena solución para poder:

- Transferir datos a un contenedor de Docker
- Guardar los datos de un contenedor de Docker
- Intercambiar datos entre contenedores de Docker

```bash
docker run -v /mis-datos:/app/data myimage
```
Esto monta la carpeta del host `/mis-datos` dentro del contenedor en `/app/data`.

#### Uso del comando “volume create” de Docker

A partir de la versión 1.9.0, que salió el 3 de noviembre de 2015, los Docker volumes se pueden crear y gestionar fácilmente con el comando _docker volume_ integrado.

##### Paso 1. Crear y nombrar el volumen

El comando _docker volume create_ crea un volumen identificado con un nombre. El nombre te permite encontrar fácilmente los Docker volumes y poder asignarlos a los contenedores específicos.

Para crear un volume, utiliza el siguiente comando:

```bash
sudo docker volume create - - name [volume name]
```

##### Paso 2. Usar el volume en un contenedor de Docker

Para crear un container que utilice un volume creado con _docker volume create_, añade el siguiente parámetro al comando _docker run_:

```bash
-v [volume name]:[container directory]
```

Para, por ejemplo, ejecutar un contenedor desde una imagen de CentOS llamada _my-volume-test_ y asignar el **data-volume** al directorio o el _data_ al container, el comando es el siguiente:

```bash
sudo docker run -it --name my-volume-test -v data-volume:/data centos /bin/bash
```

##### Paso 3. Listar los volumes

Para listar los Docker volumes que hay en el sistema, utiliza el siguiente comando:

```bash
sudo docker volume ls
```

Este comando emite una lista de todos los Docker volumes creados en el host.

##### Paso 4. Inspeccionar el volume

Para inspeccionar un volume concreto, utiliza el siguiente comando:

```bash
sudo docker volume inspect [volume name]
```

Este comando te proporciona información sobre el volume que hayas indicado, incluyendo el mount point y el directorio en el sistema host a través del cual se puede acceder al Docker volume.

Para, por ejemplo, obtener más información sobre el volume llamado “data” que hemos creado anteriormente, el comando a utilizar es el siguiente:

```bash
sudo docker volume inspect data-volume
```

##### Paso 5. Eliminar el volume

Para eliminar un volume creado de esta manera, utiliza el siguiente comando:

```bash
sudo docker volume rm [volume name]
```

No se puede eliminar un volume si está siendo utilizado por un contenedor existente. **Antes de poder eliminar el volume**, debes detener y eliminar el contenedor de Docker con los siguientes comandos:

```bash
sudo docker stop [container name or ID]
sudo docker rm [container name or ID]
```

Para, por ejemplo, eliminar el volume llamado “Data”, primero debes detener y eliminar el container que lo utiliza con my-volume-test:

```bash
sudo docker stop my-volume-test
sudo docker rm my-volume-test
```

El data-volume puede ser **borrado** con el siguiente comando:

```bash
sudo docker volume rm data-volume
```

---
## Crear y compartir `Docker Images`

Después de crear varios contenedores, tal vez quisiéramos crear nuestras propias imágenes también. Cuando iniciamos un contenedor, al mismo lo iniciamos desde una imagen base. Una vez con el contenedor en ejecución nosotros podríamos hacer cambios, por ejemplo, instalarle ciertas librerías o dependencias (ejemplo, correr `apt install htop vim git` dentro de un contenedor que tiene de imagen base, `ubuntu`). Luego de haber ejecutado este comando, el contenedor ha modificado su filesystem. Nosotros a futuro tal vez quisiéramos ejecutar contenedores iguales al anterior, por lo que Docker nos provee del comando `commit` para, a partir de un contenedor, crear una imagen. Docker mantiene las diferencias entre la imagen base y la que se quiere crear, creando una nueva _layer_ usando [UnionFS](https://es.wikipedia.org/wiki/UnionFS). Similar a _git_.

Crearemos un contenedor de _ubuntu_, y al mismo le actualizaremos la lista de repositorios. Luego de ello, haremos un `docker commit`, para definir la nueva imagen para mantener una imagen mas actualizada.

```bash
$ docker run -t -i --name=contenedorPrueba ubuntu:14.04 /bin/bash
root@69079aaaaab1:/# apt update
```

Cuando salgamos de este contenedor, el mismo se detendrá, pero seguirá estando disponibles a menos que lo eliminemos explícitamente con `docker rm`. Ahora commitiemos el contenedor, para crear una nueva imagen.

```bash
$ docker commit contenedorPrueba ubuntu:update
13132d42da3cc40e8d8b4601a7e2f4dbf198e9d72e37e19ee1986c280ffcb97c
$ docker images
REPOSITORY    TAG     IMAGE ID      CREATED          VIRTUAL SIZE
ubuntu        update  13132d42da3c  5 days ago  ...  213 MB
```

**NOTA:** Esto `ubuntu:update` especifica `<nombre_imagen>:<tag_del_commit>`.

Luego ya podremos lanzar contenedores basados en la nueva imagen `ubuntu:update`.

**ADICIONAL**

Podemos chequear las diferencias con `docker diff`.

```bash
$ docker diff contenedorPrueba
C /root
A /root/.bash_history
C /tmp
C /var
C /var/cache
C /var/cache/apt
D /var/cache/apt/pkgcache.bin
D /var/cache/apt/srcpkgcache.bin
C /var/lib
C /var/lib/apt
C /var/lib/apt/lists
...
```

### Container Registry

Un registro de contenedores es un repositorio centralizado que almacena y distribuye imágenes de contenedores. Actúa como un catálogo para las imágenes que se utilizan para crear y desplegar aplicaciones basadas en contenedores, como las imágenes de Docker.

- **Almacenamiento de imágenes:** Un registro de contenedores guarda las imágenes de los contenedores, que son archivos inmutables que contienen todo lo necesario para ejecutar una aplicación (código, bibliotecas, dependencias, etc.). 
- **Distribución:** Permite a los desarrolladores "subir" (push) imágenes al registro y "descargar" (pull) las imágenes desde el registro a otros entornos, como servidores de producción o entornos de pruebas. 
- **Gestión de versiones:** Los registros de contenedores suelen admitir el control de versiones de las imágenes, lo que facilita la gestión de diferentes versiones de una aplicación.

Existen una variedad de estos contenedores pero algunos populares son:
- Docker Hub
- Azure Container Registry  (Microsoft)
- Elastic Container Registry (AWS)
- Google Container Registry (Google Cloud)

#### Ejemplo:
```bash
# Descargar imagen oficial de nginx (servidor web)
docker pull nginx

# Ver imágenes descargadas
docker images

# Ejecutar la imagen en un contenedor
docker run -d -p 8080:80 nginx

# Accede a http://localhost:8080 para ver nginx corriendo

```

#### Buenas prácticas

- Aprende la diferencia entre imágenes y contenedores (una es la receta, el otro la comida lista).
- Usa imágenes oficiales siempre que sea posible.
- Evita guardar datos importantes dentro del contenedor: usa volúmenes.
#### Errores comunes

- **Confundir imagen con contenedor:** La imagen no cambia; el contenedor sí.
- **Modificar directamente dentro del contenedor:** esos cambios se pierden al reiniciar.
- **No usar volúmenes para datos persistentes:** esto puede causar pérdida de información.

---
## Docker Compose

### Objetivo
Aprender qué es Docker Compose, para qué sirve y cómo usarlo para definir, configurar y ejecutar aplicaciones multi-contenedor con un solo comando.

### Conceptos clave

- **Docker Compose:** herramienta que permite definir y correr múltiples contenedores usando un archivo YAML (`docker-compose.yml`).
- **Servicio:** definición de un contenedor en Compose.
- **Redes y volúmenes:** recursos que Compose puede crear automáticamente para conectar y persistir datos entre servicios.

### Explicación detallada

Cuando desarrollamos una aplicación, muchas veces necesitamos varios servicios corriendo al mismo tiempo, por ejemplo:

- Un backend en Python o Node.js
- Una base de datos como PostgreSQL
- Un frontend en Vue o React

Configurar y ejecutar cada contenedor manualmente puede ser tedioso. Aquí es donde entra **Docker Compose**.

Con Docker Compose puedes:

- Declarar todos los servicios en un solo archivo (`docker-compose.yml`)
- Ejecutarlos juntos con un solo comando
- Gestionar redes, volúmenes y variables de entorno fácilmente

### Estructura básica de un `docker-compose.yml`

```yaml
version: "3.9"

services:
  app:
    build: .
    ports:
      - "8000:8000"
    volumes:
      - .:/code
    depends_on:
      - db

  db:
    image: postgres:13
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
      POSTGRES_DB: mydb

```

Este ejemplo define dos servicios:
- `app`: construye la imagen desde el Dockerfile local y expone el puerto 8000
- `db`: usa una imagen oficial de PostgreSQL y define variables de entorno

Comandos esenciales de Docker Compose
```bash
# Levanta los servicios definidos en segundo plano
docker-compose up -d

# Muestra los logs de los servicios
docker-compose logs

# Detiene todos los servicios
docker-compose down

# Reconstruye imágenes si hay cambios
docker-compose up --build

```

### Ejemplo completo: app con Flask + PostgreSQL

**1. Dockerfile para la app**

```
Dockerfile

`FROM python:3.10 WORKDIR /app COPY . . RUN pip install flask psycopg2-binary CMD ["python", "app.py"]`
```

**2. app.py**

```python
from flask 
import Flask
import psycopg2 


app = Flask(__name__) 
@app.route('/')


def index():
	return "¡Hola desde Flask + Docker Compose!"  if __name__ == '__main__':           app.run(host='0.0.0.0', port=8000)

```

**3. docker-compose.yml**

```yaml
version: "3.9"

services:
  web:
    build: .
    ports:
      - "8000:8000"
    depends_on:
      - db

  db:
    image: postgres:13
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
      POSTGRES_DB: mydb

```

**4. Ejecutar**

```bash
docker-compose up --build
```
Abre `http://localhost:8000` y verás el mensaje.

#### Buenas prácticas
- Usa variables de entorno en un archivo `.env` para manejar secretos y configuraciones:
```yml
environment:
  - DB_USER=${POSTGRES_USER}
```

- Usa `depends_on` para manejar el orden de arranque, pero considera también healthchecks si necesitas control más estricto.
- No almacenes datos importantes dentro del contenedor: usa volúmenes declarados.

--- 
## Visualización de logs con `docker logs`

### Objetivo
Aprender cómo inspeccionar, filtrar y entender los registros (logs) generados por los contenedores Docker, una herramienta esencial para depurar errores y monitorear servicios.

### Conceptos clave

- **Logs en Docker:** salida estándar (`stdout` y `stderr`) del proceso principal dentro del contenedor.
- **docker logs:** comando para ver los logs generados por un contenedor.
- **Drivers de logging:** sistemas que definen cómo y dónde se almacenan los logs (por defecto: `json-file`).
### ¿Qué hace `docker logs`?

Docker redirige la salida del proceso principal del contenedor (`stdout` y `stderr`) a un archivo de log interno.  
`docker logs` te permite acceder a esa información.

### Sintaxis básica
```bash
docker logs [opciones] <container_id o nombre>
```

### Comandos básicos
| Opcion            | Descripción                                                                   |
| ----------------- | ----------------------------------------------------------------------------- |
| `-f` / `--follow` | Muestra logs en tiempo real (como `tail -f`)                                  |
| `--tail N`        | Muestra solo las últimas `N` líneas <br>                                      |
| `-t`              | Incluye timestamps en la salida\|                                             |
| `--since TIME`    | Muestra logs a partir de un momento específico (`30m`, `2024-12-01T10:00:00`) |
| `--until TIME`    | Muestra logs hasta cierto punto en el tiempo                                  |


---
## Persistencia de datos y volúmenes en Docker

### Objetivo
Comprender cómo Docker maneja la persistencia de datos usando volúmenes, conocer las diferencias entre *bind mounts* y *named volumes*, y aprender cómo respaldar y migrar los datos almacenados.

### Conceptos clave

- **Volumen (volume):** mecanismo que Docker usa para guardar datos fuera del sistema de archivos del contenedor.
- **Bind mount:** conexión directa entre una carpeta del host y el contenedor.
- **Named volume:** volumen gestionado por Docker que se almacena en una ruta controlada.
- **Persistencia:** habilidad de mantener datos aunque el contenedor sea eliminado.

### Explicación detallada

Por defecto, cuando un contenedor termina o es eliminado, **todos sus datos se pierden**. Para evitar esto, Docker permite conectar el contenedor a una ubicación persistente: un volumen.

Existen dos formas principales:
#### Bind Mounts

Los **bind mounts** enlazan un directorio del host al contenedor. Son útiles para desarrollo porque los cambios en tiempo real se reflejan dentro del contenedor.

```bash
docker run -v $(pwd)/data:/app/data myimage
```
- La carpeta `./data` en tu máquina se monta dentro del contenedor en `/app/data`.
- Muy útil para editar archivos desde tu IDE sin reconstruir la imagen.

##### Ventajas:
- Control total del contenido
-  Ideal para entornos locales

##### Desventajas:
- Menos portables
- Menos seguros (acceso directo al sistema del host)
#### Named Volumes

Los **named volumes** son volúmenes gestionados por Docker. Se almacenan en una ruta interna como `/var/lib/docker/volumes`.

```bash
docker volume create mis_datos
docker run -v mis_datos:/app/data myimage
```

- Se puede usar en múltiples contenedores
- No depende del sistema operativo del host

##### Ventajas:

- Más portables y fáciles de respaldar
- Separación clara entre datos y código
#####  Desventajas:
- Menos transparente que bind mounts

### Ejemplo práctico

1. Crear un named volume:
```bash
docker volume create app_data
```

2. Usarlo en un contenedor:
```bash
docker run -v app_data:/var/lib/data myimage
```

3. Ver los volúmenes
```bash
docker volume ls
```

4. Inspeccionar un volumen:
```bash
docker volume inspect app_data
```

---
## Docker en flujos DevOps y CI/CD

### Objetivo
Aprender cómo usar Docker en pipelines de integración y entrega continua (CI/CD), para automatizar la construcción, prueba y despliegue de imágenes de forma segura y repetible.

###  Conceptos clave

- **CI/CD:** Práctica de automatizar pruebas (CI) y despliegues (CD) en cada cambio del código.
- **Pipeline:** Secuencia de pasos automatizados (build, test, deploy).
- **Registro de contenedores (registry):** Repositorio para almacenar y compartir imágenes Docker (Docker Hub, GHCR, GitLab, etc).
- **Docker build/push:** Comandos para construir y subir una imagen.

###  Explicación detallada

En un entorno moderno de DevOps, lo ideal es que cada vez que haces un `push` de código, se ejecute una pipeline que:

1. **Construye la imagen Docker**
2. **Ejecuta pruebas automáticas**
3. **Publica la imagen en un registro (si pasa todo)**
4. **Despliega a staging o producción**

Docker es perfecto para esto porque permite empaquetar la aplicación con todo su entorno, haciendo que las builds sean 100% reproducibles y portables.

Ejemplo práctico con GitHub Actions

** Estructura básica de workflow**
```yaml
# .github/workflows/docker.yml
name: Docker CI

on:
  push:
    branches:
      - main

jobs:
  build-and-push:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout código
        uses: actions/checkout@v3

      - name: Login a Docker Hub
        uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}

      - name: Construir la imagen
        uses: docker/build-push-action@v5
        with:
          context: .
          push: true
          tags: carlostorres/miapp:latest
```

**Dockerfile básico** 

```dockerfile
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
CMD ["npm", "start"]
```

###  Buenas prácticas

- Usa etiquetas (tags) semánticas (`1.0.0`, `main`, `latest`) para las imágenes.
- No guardes tus credenciales directamente en los archivos: usa `secrets`.
- Realiza `docker scan` o `trivy` para detectar vulnerabilidades antes de hacer push.
- Divide los pasos en etapas (`build`, `test`, `push`, `deploy`) para mayor claridad.

### Errores comunes
- **No loguearte al registry antes del push:** el build funciona, pero el push falla.
- **Usar `latest` en todos lados:** puede generar builds inconsistentes.
- **No testear la imagen antes de publicarla:** asegúrate de correr al menos una prueba mínima.

---
## Redes en Docker: Conectando contenedores

### Objetivo
Comprender cómo Docker maneja la comunicación entre contenedores mediante redes. Aprender los distintos tipos de red disponibles y cómo conectarlos manual o automáticamente usando Docker Compose.

### Conceptos clave

- **Red (network):** canal virtual que permite que los contenedores se comuniquen entre sí.
- **Bridge network:** red privada creada por Docker por defecto (modo aislado).
- **Host network:** el contenedor usa directamente la red del host (sin aislamiento).
- **Overlay network:** red distribuida usada en clústeres Docker Swarm o Kubernetes.
- **Alias:** nombre DNS interno por el cual un contenedor puede ser alcanzado en la red.

### Explicación detallada

Por defecto, Docker aísla cada contenedor, pero permite que se comuniquen **a través de redes virtuales**.

#### 1. Bridge Network (la más común)

La red por defecto (`bridge`) permite que varios contenedores se comuniquen si están conectados a la misma red.

En términos de redes, un puente es un dispositivo de capa de enlace que reenvía tráfico entre segmentos de red. Un puente puede ser un dispositivo de hardware o de software que se ejecuta dentro del núcleo de un host.

En Docker, una red de puentes utiliza un puente de software que permite la comunicación entre los contenedores conectados a la misma red, a la vez que proporciona aislamiento de los contenedores que no están conectados a ella. El controlador de puente de Docker instala automáticamente reglas en el equipo host para que los contenedores de diferentes redes de puentes no puedan comunicarse directamente entre sí.

Las redes puente se aplican a los contenedores que se ejecutan en el mismo host de demonio de Docker. Para la comunicación entre contenedores que se ejecutan en diferentes hosts de demonio de Docker, se puede gestionar el enrutamiento a nivel del sistema operativo o usar una [red superpuesta](https://docs.docker.com/engine/network/drivers/overlay/) .

Al iniciar Docker, se crea automáticamente una [red de puente predeterminada](https://docs.docker.com/engine/network/drivers/bridge/#use-the-default-bridge-network) (también llamada `bridge`) y los contenedores recién iniciados se conectan a ella, a menos que se especifique lo contrario. También se pueden crear redes de puente personalizadas, definidas por el usuario. **Las redes de puente definidas por el usuario son superiores a la red predeterminada `bridge` .**

##### Ejemplo

```bash
docker network create mi_red
docker run -d --name app --network mi_red myimage
docker run -d --name db --network mi_red postgres
```

Dentro del contenedor `app`, puedes acceder a `db` por su nombre de contenedor:
```python
# Ejemplo Python
connection = psycopg2.connect(host="db", ...)
```

#### 2. Host Network

El contenedor comparte el stack de red del host (no hay NAT, ni puertos).
Si usa el `host`modo de red para un contenedor, su pila de red no está aislada del host Docker (el contenedor comparte el espacio de nombres de red del host) y no se le asigna su propia dirección IP. Por ejemplo, si ejecuta un contenedor enlazado al puerto 80 y usa `host` la red, la aplicación del contenedor está disponible en el puerto 80 de la dirección IP del host.

##### Limitaciones
- Los procesos dentro del contenedor no pueden vincularse a las direcciones IP del host porque el contenedor no tiene acceso directo a las interfaces del host.
- La función de red de host de Docker Desktop funciona en la capa 4. Esto significa que, a diferencia de Docker en Linux, los protocolos de red que operan por debajo de TCP o UDP no son compatibles.
- Esta función no funciona con el Aislamiento de contenedor mejorado habilitado, ya que aislar los contenedores del host y permitirles acceder a la red del host se contradicen entre sí.
- Solo se admiten contenedores Linux. La red de host no funciona con contenedores Windows.
#### Ventajas:
- Acceso más rápido a la red
- Útil para servicios que requieren puertos específicos

##### Desventajas:
- No hay aislamiento
- No disponible en Windows

#### 3. Overlay Network (en Swarm)

Permite comunicación entre contenedores distribuidos en diferentes hosts físicos o virtuales. Se usa con Docker Swarm o Kubernetes.

Las versiones actuales de Docker incluyen el modo Swarm para gestionar de forma nativa un clúster de motores Docker llamado swarm. Utilice la CLI de Docker para crear un enjambre, implementar servicios de aplicación en él y gestionar su comportamiento.

**Ejecutar Docker en modo Swarm permite gestionar varios clusters de manera descentralizada.** Esto es una orquestación de contenedores los cuales no tienen por qué estar situados en la misma máquina física ni virtual. Crea así una independencia del sistema que aloja los contenedores, aumentando la seguridad ante pérdida del servicio si se distribuye los nodos en distintas máquinas. 

**Docker Swarm se basa en una arquitectura maestro-esclavo (manager-worker).** Cada enjambre está formado al menos por un nodo maestro (también llamado administrador o manager) y tantos nodos esclavos (llamados trabajadores o workers) como se desee. El maestro de Swarm es responsable de la gestión del clúster y la delegación de tareas, el esclavo se encarga de ejecutar dichas tareas. 

Existen **tres conceptos que se deben diferenciar: servicio, aplicación y tarea.** 

- Los servicios definidos para Docker Swarm pueden contener varias tareas o una única. 

- Las tareas hacen referencia a las réplicas de un mismo servicio y puede existir varias tareas de un mismo servicio. El encargado de esta distribución de tareas entre los nodos como ya se ha mencionado es el manager del enjambre.

- Las aplicaciones hacen referencia a los distintos softwares que puede contener un mismo contenedor que ejecuta una imagen específica de Docker.

Se distinguen **dos maneras de trabajar con Docker Swarm** en cuanto a cómo es la disponibilidad de las réplicas de los servicios definidos: 

- **Servicios globales:** Swarm ejecutará una tarea en todos y cada uno de los nodos del clúster que cumpla con las restricciones establecidas como la ubicación del servicio o recursos.  

- **Servicios replicados:** se especifica el número de tareas idénticas que se desea ejecutar. Swarm creará tantas réplicas de la tarea especificada como se ha determinado. Por ejemplo, si creamos un servicio con dos réplicas, Swarm creará dos tareas que alojará en los nodos del enjambre.
![[swarm.png]]
La imagen anterior muestra cómo existe un servicio replicado con dos réplicas, alojado en dos nodos distintos. Existe también un servicio global, de este segundo se encuentra una réplica en cada nodo disponible. 

La manera de trabajar con un servicio global o un servicio replicado se establece mediante el número de réplicas a ejecutar de un servicio o indicando que se desea ejecutar el servicio en el modo global. Se puede indicar mediante las sentencias del Docker CLI o mediante el `docker-compose.yml`
##### Caracteristicas destacadas
###### Gestión de clústeres integrada con Docker Engine

Usa la CLI de Docker Engine para crear un enjambre de Docker Engines donde puedas implementar servicios de aplicación. No necesitas software de orquestación adicional para crear o administrar un enjambre.

###### Diseño descentralizado

En lugar de gestionar la diferenciación entre los roles de los nodos durante la implementación, Docker Engine gestiona cualquier especialización en tiempo de ejecución. Puedes implementar ambos tipos de nodos (managers y workers) con Docker Engine. Esto significa que puedes crear un enjambre completo a partir de una sola imagen de disco.

###### Modelo de servicio declarativo

Docker Engine utiliza un enfoque declarativo que permite definir el estado deseado de los distintos servicios en la pila de aplicaciones. Por ejemplo, se podría describir una aplicación compuesta por un servicio front-end web con servicios de cola de mensajes y un back-end de base de datos.

###### Escalada

Para cada servicio, puede indicar el número de tareas que desea ejecutar. Al escalar, el administrador de enjambre se adapta automáticamente añadiendo o eliminando tareas para mantener el estado deseado.

###### Conciliación del estado deseado

El nodo administrador de enjambre supervisa constantemente el estado del clúster y concilia cualquier diferencia entre el estado real y el deseado. Por ejemplo, si configura un servicio para ejecutar 10 réplicas de un contenedor, y un equipo de trabajo que aloja dos de esas réplicas falla, el administrador crea dos nuevas réplicas para reemplazar las que fallaron. El administrador de enjambre asigna las nuevas réplicas a los equipos de trabajo que se están ejecutando y están disponibles.

###### Redes multihost

Puede especificar una red superpuesta para sus servicios. El administrador de enjambre asigna automáticamente direcciones a los contenedores en la red superpuesta al inicializar o actualizar la aplicación.

###### Descubrimiento de servicios

Los nodos del administrador de enjambre asignan a cada servicio un nombre DNS único y equilibran la carga de los contenedores en ejecución. Se pueden consultar todos los contenedores que se ejecutan en el enjambre a través de un servidor DNS integrado en él.

###### Equilibrio de carga

Puedes exponer los puertos de los servicios a un balanceador de carga externo. Internamente, el enjambre te permite especificar cómo distribuir los contenedores de servicios entre los nodos.

###### Seguro por defecto

Cada nodo del enjambre aplica autenticación mutua y cifrado TLS para proteger las comunicaciones entre sí y con los demás nodos. Puede usar certificados raíz autofirmados o certificados de una CA raíz personalizada.

#### Ejemplo práctico

```bash
# Crear una red personalizada
docker network create red_mis_servicios

# Correr dos contenedores en esa red
docker run -d --name redis --network red_mis_servicios redis
docker run -it --rm --network red_mis_servicios busybox sh
```

Desde `busybox` puedes hacer ping a `redis`:
```bash
ping redis
```

#### Docker Compose y redes automáticas

Cuando usas **Docker Compose**, se crea una red automática con el nombre del proyecto, y todos los servicios definidos pueden comunicarse entre sí por su nombre de servicio.

```yaml
version: "3.9"
services:
  web:
    image: nginx
  app:
    build: "."
  db:
    image: postgres

```

En este ejemplo:
- `web`, `app` y `db` pueden hablar entre sí usando sus nombres como hostname.
- No es necesario declarar una red explícita (Docker lo hace por ti).

Puedes también definir redes personalizadas si lo deseas:

```yaml
networks:
  red_interna:
    driver: bridge

services:
  app:
    build: .
    networks:
      - red_interna
```

#### Diferencias entre Docker y Docker Swarm
| Característica            | Docker (modo standalone) | Docker Swarm               |
| ------------------------- | ------------------------ | -------------------------- |
| Corre en una sola máquina | ✅                        | ❌ (corre en múltiples)     |
| Orquestación automática   | ❌ (manual con scripts)   | ✅                          |
| Balanceo de carga interno | ❌                        | ✅                          |
| Alta disponibilidad       | ❌                        | ✅                          |
| Escalado automático       | ❌                        | ✅ (`docker service scale`) |
#### ¿Cuándo usar Docker Swarm?

Usa Swarm si:

- Tienes múltiples servidores y necesitas **alta disponibilidad**.
- Quieres **balancear carga** entre instancias de tu app.
- Necesitas **recuperación automática** de fallos.
- Quieres una solución más simple que Kubernetes (aunque Kubernetes es más potente, también más complejo).
