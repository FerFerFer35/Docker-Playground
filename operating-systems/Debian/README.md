# Debian - Docker Image

## 📌 Descripción

Este entorno utiliza la imagen oficial de Debian para crear un contenedor interactivo que simula un sistema Linux estable y ampliamente utilizado en servidores.

Debian es reconocido por su estabilidad y solidez. Muchas distribuciones, incluyendo Ubuntu, están basadas en Debian. Es ideal para:

- Simular entornos de servidor estables
- Construir imágenes base confiables
- Comparar diferencias con Ubuntu
- Practicar instalación de paquetes con APT
- Servir como base para entornos backend

Este ejemplo forma parte de la sección **operating-systems**, cuyo propósito es comprender distintos sistemas base antes de construir entornos más complejos.

---

## 🏷 Imagen utilizada

`debian:12`

---

## ⚙️ Configuración del servicio

| Propiedad        | Valor          | Descripción |
|------------------|---------------|-------------|
| image            | debian:12     | Imagen oficial de Debian |
| container_name   | debian-demo   | Nombre personalizado del contenedor |
| stdin_open       | true          | Permite mantener STDIN abierto |
| tty              | true          | Asigna una terminal interactiva |
| command          | bash          | Inicia la shell Bash |

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
docker exec -it debian-demo bash
```

Ahora estarás dentro del sistema Debian del contenedor.

---

## 📦 Instalar paquetes dentro del contenedor

Debian utiliza `apt` como gestor de paquetes.

Actualizar repositorios:

```bash
apt update
```

Instalar paquetes:

```bash
apt install curl -y
apt install nano -y
```

---

## 🔍 Ver tamaño de la imagen

Desde tu máquina host:

```bash
docker images
```

Esto te permitirá comparar Debian con Ubuntu, Fedora, Amazon Linux o Alpine.

---

## 🧹 Detener y eliminar el entorno

Para detener el contenedor:

```bash
docker compose down
```

---

## 🧠 Conceptos importantes

### Debian
Distribución enfocada en estabilidad y seguridad, ampliamente utilizada en servidores.

### apt
Gestor de paquetes utilizado en Debian y distribuciones basadas en él.

### stdin_open
Permite interacción directa con el contenedor.

### tty
Asigna una terminal virtual al contenedor.

### command
Define el proceso inicial del contenedor (en este caso `bash`).

---

Este contenedor no expone puertos porque no ejecuta servicios de red.
Está diseñado como entorno interactivo de laboratorio.
