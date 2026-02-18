# Azure CLI - Docker Image

## 📌 Descripción

Este entorno utiliza la imagen oficial de Azure CLI para ejecutar comandos de Microsoft Azure desde un contenedor Docker.

Azure CLI es una herramienta esencial para desarrolladores y profesionales DevOps que trabajan con servicios en la nube de Microsoft, permitiendo:

- Administrar recursos en Azure
- Crear y gestionar máquinas virtuales
- Configurar redes y almacenamiento
- Automatizar despliegues
- Integrarse en pipelines CI/CD

Este ejemplo forma parte de la sección **developer-tools**, enfocada en herramientas modernas de infraestructura y nube.

---

## 🏷 Imagen utilizada

`mcr.microsoft.com/azure-cli:latest`

---

## ⚙️ Configuración del servicio

| Propiedad        | Valor                               | Descripción |
|------------------|--------------------------------------|-------------|
| image            | mcr.microsoft.com/azure-cli:latest   | Imagen oficial de Azure CLI |
| container_name   | azurecli-demo                        | Nombre del contenedor |
| stdin_open       | true                                 | Permite interacción |
| tty              | true                                 | Asigna terminal interactiva |
| volumes          | ~/.azure:/root/.azure                | Monta credenciales locales |

---

## 🔐 Requisitos previos

Debes iniciar sesión en Azure al menos una vez:

```bash
az login
```

Esto generará la carpeta:

```
~/.azure
```

Que será utilizada dentro del contenedor.

---

## 🚀 Cómo ejecutarlo

Verificar versión:

```bash
docker compose run --rm azurecli az version
```

Abrir sesión interactiva:

```bash
docker compose run --rm azurecli bash
```

---

## 🧪 Ejemplos de uso

Iniciar sesión:

```bash
az login
```

Listar grupos de recursos:

```bash
az group list
```

Listar máquinas virtuales:

```bash
az vm list
```

---

## 📂 Persistencia de credenciales

El volumen:

```
~/.azure:/root/.azure
```

Permite reutilizar tus credenciales sin configurarlas cada vez dentro del contenedor.

---

## 🧹 Limpieza

El servicio se ejecuta bajo demanda usando:

```bash
docker compose run --rm azurecli
```

La opción `--rm` elimina el contenedor automáticamente al finalizar.

---

## 🧠 Conceptos importantes

### Azure CLI
Herramienta oficial para interactuar con servicios de Microsoft Azure desde la terminal.

### volumes
Permite compartir credenciales y archivos entre el host y el contenedor.

### run vs up
`docker compose run` ejecuta un comando puntual.
`docker compose up` levanta servicios persistentes.

---

Este entorno está diseñado para desarrollo y automatización.
No expone puertos porque no ejecuta servicios web.
