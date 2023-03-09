# Proyecto Microservicios en Docker Compose
Proyecto Final Microservicios
Eduard Hernandez

Despliegue de Kanban App con Docker Compose
Este es un archivo README.md que describe cómo desplegar la aplicación Kanban utilizando Docker Compose.

## Prerrequisitos
Antes de comenzar, asegúrese de tener instalado Docker y Docker Compose en su sistema. Puede seguir los siguientes enlaces para obtener más información sobre cómo instalarlos:

### Instrucciones
Clone el repositorio de la aplicación Kanban en su sistema:

```git clone https://github.com/tu-usuario/kanban-app.git```

Asegúrese de reemplazar tu-usuario con su nombre de usuario de GitHub y kanban-app con el nombre de su repositorio.

Navegue al directorio de la aplicación Kanban en su sistema:

```
cd kanban-app
```
Cree un archivo docker-compose.yml en el directorio raíz del proyecto y copie el siguiente contenido en él:
```
version: '3'
services:

  kanban-postgres:
    image: "postgres:9.6-alpine"
    container_name: kanban-postgres
    volumes:
      - kanban-data:/var/lib/postgresql/data
    ports:
      - 5432:5432
    environment:
      - POSTGRES_DB=kanban
      - POSTGRES_USER=kanban
      - POSTGRES_PASSWORD=kanban

  kanban-app:
    build: ./kanban-app
    container_name: kanban-app
    environment:
      - DB_SERVER=kanban-postgres
      - POSTGRES_DB=kanban
      - POSTGRES_USER=kanban
      - POSTGRES_PASSWORD=kanban
    ports:
      - 8080:8080
    links:
      - kanban-postgres

  kanban-ui:
    build: ./kanban-ui
    container_name: kanban-ui
    ports:
      - 4200:80
    links:
      - kanban-app
volumes:
  kanban-data:
```
Ejecute el comando ```docker-compose up``` en el directorio raíz del proyecto para iniciar la aplicación:

```
docker-compose up
```
Acceda a la aplicación Kanban en su navegador web en la siguiente dirección:

```
http://localhost:4200
```
Eso es todo. Ahora ha desplegado la aplicación Kanban utilizando Docker Compose.
