# Amazon Linux - Docker Image

## 📌 Descripción

Este entorno utiliza la imagen oficial de Amazon Linux para crear un contenedor interactivo que simula el sistema operativo utilizado comúnmente en entornos de AWS.

Amazon Linux está optimizado para servicios en la nube y es ampliamente utilizado en instancias EC2. Es ideal para:

- Simular entornos cloud locales
- Probar compatibilidad con servidores en AWS
- Entender diferencias entre distribuciones empresariales
- Crear imágenes base orientadas a producción

Este ejemplo forma parte de la sección **operating-systems**, cuyo propósito es comprender distintos sistemas base antes de construir entornos más complejos.

---

## 🏷 Imagen utilizada

`amazonlinux:2023`

---

## ⚙️ Configuración del servicio

| Propiedad        | Valor                | Descripción |
|------------------|----------------------|-------------|
| image            | amazonlinux:2023     | Imagen oficial de Amazon Linux |
| container_name   | amazonlinux-demo     | Nombre personalizado del contenedor |
| stdin_open       | true                 | Permite mantener STDIN abierto |
| tty              | true                 | Asigna una terminal interactiva |
| command          | bash                 | Inicia la shell Bash |

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
docker exec -it amazonlinux-demo bash
```

Ahora estarás dentro del sistema Amazon Linux del contenedor.

---

## 📦 Instalar paquetes dentro del contenedor

Amazon Linux 2023 utiliza `dnf` como gestor de paquetes.

Actualizar repositorios:

```bash
dnf update -y
```

Instalar paquetes:

```bash
dnf install curl -y
dnf install nano -y
```

---

## 🔍 Ver tamaño de la imagen

Desde tu máquina host:

```bash
docker images
```

Esto te permitirá comparar Amazon Linux con otras imágenes como Ubuntu, Fedora o Alpine.

---

## 🧹 Detener y eliminar el entorno

Para detener el contenedor:

```bash
docker compose down
```

---

## 🧠 Conceptos importantes

### Amazon Linux
Distribución mantenida por AWS y optimizada para rendimiento y seguridad en la nube.

### dnf
Gestor de paquetes moderno utilizado en Amazon Linux 2023.

### stdin_open
Permite interacción directa con el contenedor.

### tty
Asigna una terminal virtual al contenedor.

### command
Define el proceso inicial del contenedor (en este caso `bash`).

---

Este contenedor no expone puertos porque no ejecuta servicios de red.
Está diseñado como entorno interactivo de laboratorio.
