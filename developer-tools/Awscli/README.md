# AWS CLI - Docker Image

## 📌 Descripción

Este entorno utiliza la imagen oficial de AWS CLI para ejecutar comandos de Amazon Web Services desde un contenedor Docker.

AWS CLI es una herramienta fundamental para desarrolladores y DevOps que trabajan con servicios en la nube, permitiendo:

- Gestionar recursos de AWS
- Crear y administrar buckets S3
- Controlar instancias EC2
- Automatizar despliegues
- Integrarse en pipelines CI/CD

Este ejemplo forma parte de la sección **developer-tools**, enfocada en herramientas esenciales para el desarrollo moderno.

---

## 🏷 Imagen utilizada

`amazon/aws-cli:latest`

---

## ⚙️ Configuración del servicio

| Propiedad        | Valor                   | Descripción |
|------------------|------------------------|-------------|
| image            | amazon/aws-cli:latest  | Imagen oficial de AWS CLI |
| container_name   | awscli-demo            | Nombre del contenedor |
| stdin_open       | true                   | Permite interacción |
| tty              | true                   | Asigna terminal interactiva |
| volumes          | ~/.aws:/root/.aws      | Monta credenciales locales |

---

## 🔐 Requisitos previos

Debes tener configuradas tus credenciales en tu máquina host:

```bash
aws configure
```

Esto crea la carpeta:

```
~/.aws
```

Que será montada dentro del contenedor.

---

## 🚀 Cómo ejecutarlo

Desde la carpeta donde se encuentra el `docker-compose.yml`:

```bash
docker compose run --rm awscli --version
```

Para abrir una sesión interactiva:

```bash
docker compose run --rm awscli bash
```

---

## 🧪 Ejemplos de uso

Listar buckets S3:

```bash
aws s3 ls
```

Listar instancias EC2:

```bash
aws ec2 describe-instances
```

---

## 📂 Persistencia de credenciales

El volumen:

```
~/.aws:/root/.aws
```

permite reutilizar tus credenciales locales sin configurarlas dentro del contenedor.

---

## 🧹 Limpieza

Este servicio se ejecuta bajo demanda con:

```bash
docker compose run --rm awscli
```

La opción `--rm` elimina automáticamente el contenedor al finalizar.

---

## 🧠 Conceptos importantes

### AWS CLI
Herramienta oficial para interactuar con servicios de Amazon Web Services desde la terminal.

### volumes
Permite compartir archivos entre el host y el contenedor.

### run vs up
`docker compose run` ejecuta un comando puntual.
`docker compose up` levanta servicios persistentes.

---

Este entorno está pensado para desarrollo y pruebas.
No expone puertos porque no ejecuta servicios web.
