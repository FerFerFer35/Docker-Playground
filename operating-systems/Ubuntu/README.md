# Ubuntu - Docker Image

## 📌 Descripción

Este entorno utiliza la imagen oficial de Ubuntu para crear un contenedor interactivo que simula un sistema Linux base dentro de Docker.

Ubuntu es una de las distribuciones Linux más utilizadas en servidores y entornos de desarrollo. En este contexto, nos permite:

- Explorar cómo funciona una imagen base
- Instalar paquetes manualmente
- Probar comandos Linux
- Entender el comportamiento de contenedores interactivos
- Servir como punto de partida para futuros Dockerfiles

Este ejemplo forma parte de la sección **operating-systems**, cuyo objetivo es comprender los fundamentos antes de construir entornos más complejos.

---

## 🏷 Imagen utilizada

`ubuntu:24.04`

---

## ⚙️ Configuración del servicio

| Propiedad        | Valor            | Descripción |
|------------------|------------------|-------------|
| image            | ubuntu:24.04     | Imagen oficial de Ubuntu |
| container_name   | ubuntu-demo      | Nombre personalizado del contenedor |
| stdin_open       | true             | Permite mantener STDIN abierto (modo interactivo) |
| tty              | true             | Asigna una terminal TTY |
| command          | bash             | Inicia la shell Bash al arrancar |

---

## 🚀 Cómo ejecutarlo

Desde la carpeta donde se encuentra el `docker-compose.yml`:

```bash
docker compose up -d
```

Esto levantará el contenedor en segundo plano.

---

## 🔐 Cómo acceder al contenedor

```bash
docker exec -it ubuntu-demo bash
```

Ahora estarás dentro del sistema Ubuntu del contenedor.

---

## 📦 Instalar paquetes dentro del contenedor

Una vez dentro puedes usar APT normalmente:

```bash
apt update
apt install curl -y
```

Ejemplos adicionales:

```bash
apt install nano -y
apt install iputils-ping -y
```

---

## 🔍 Ver tamaño de la imagen

Desde tu máquina host:

```bash
docker images
```

Esto te permitirá comparar el tamaño de Ubuntu con otras imágenes como Alpine.

---

## 🧹 Detener y eliminar el entorno

Para detener el contenedor:

```bash
docker compose down
```

---

## 🧠 Conceptos importantes

### stdin_open
Permite que el contenedor acepte entrada interactiva.

### tty
Asigna una terminal al contenedor para poder interactuar como si fuera una máquina real.

### command
Define qué proceso se ejecuta al iniciar el contenedor. En este caso, `bash`.

---

Este entorno no expone puertos porque no ejecuta servicios de red.  
Está pensado únicamente como laboratorio interactivo.
