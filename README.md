# Go Application with Air for Hot Reload

Este proyecto es una aplicación Go que utiliza [Air](https://github.com/cosmtrek/air) para el hot reload durante el desarrollo. A continuación se muestra cómo configurar y ejecutar el proyecto usando Docker y Docker Compose.

## Requisitos Previos

- **Docker**: Asegúrate de tener Docker instalado. Puedes descargar Docker desde [aquí](https://www.docker.com/get-started).
- **Docker Compose**: Asegúrate de tener Docker Compose instalado. Esto generalmente se instala junto con Docker. Verifica la instalación con `docker-compose --version`.

## Estructura del Proyecto

- **Dockerfile**: Define la imagen Docker para la aplicación Go.
- **docker-compose.yml**: Define cómo construir y ejecutar el contenedor de la aplicación Go.

## Configuración

### 1. Dockerfile

El Dockerfile proporciona los pasos para construir la imagen de Docker para la aplicación Go. Incluye la instalación de Air para hot reload.

```Dockerfile
FROM golang:1.22-alpine

WORKDIR /app

RUN go install github.com/air-verse/air@latest

COPY go.mod ./
COPY .air.toml ./
COPY . .

RUN go mod download

# Crea el directorio tmp para Air
RUN mkdir -p /app/tmp

CMD ["air", "-c", ".air.toml"]

### Explicación de los Comandos Agregados:

- **docker build -t go-app .**: Construye la imagen del proyecto con el nombre `go-app`.
- **docker-compose up**: Ejecuta la aplicación, construyendo la imagen si no existe y levantando el contenedor.
- **docker-compose down**: Detiene y elimina el contenedor.
- **docker-compose up -d**: Ejecuta la aplicación en segundo plano.
- **docker start <nombre_contenedor>**: Inicia un contenedor previamente detenido.
- **docker-compose logs**: Muestra los logs del contenedor en ejecución.
- **docker-compose logs -f**: Sigue los logs en tiempo real.
