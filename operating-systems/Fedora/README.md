# Fedora - Docker Image

## 📌 Descripción

Este entorno utiliza la imagen oficial de Fedora para crear un contenedor interactivo que simula un sistema Linux moderno dentro de Docker.

Fedora es una distribución enfocada en incorporar tecnologías recientes y suele estar más actualizada que otras distribuciones tradicionales. Es ideal para:

- Probar herramientas modernas
- Experimentar con versiones recientes de paquetes
- Entender diferencias entre gestores de paquetes
- Usarlo como base para imágenes personalizadas

Este ejemplo forma parte de la sección **operating-systems**, cuyo propósito es comprender las imágenes base antes de construir entornos más complejos.

---

## 🏷 Imagen utilizada

`fedora:40`

---

## ⚙️ Configuración del servicio

| Propiedad        | Valor         | Descripción |
|------------------|--------------|-------------|
| image            | fedora:40    | Imagen oficial de Fedora |
| container_name   | fedora-demo  | Nombre personalizado del contenedor |
| stdin_open       | true         | Permite mantener STDIN abierto |
| tty              | true         | Asigna una terminal interactiva |
| command          | bash         | Inicia la shell Bash |

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
docker exec -it fedora-demo bash
```

Ahora estarás dentro del sistema Fedora del contenedor.

---

## 📦 Instalar paquetes dentro del contenedor

Fedora utiliza `dnf` como gestor de paquetes.

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

Esto te permitirá comparar Fedora con otras imágenes como Ubuntu o Alpine.

---

## 🧹 Detener y eliminar el entorno

Para detener el contenedor:

```bash
docker compose down
```

---

## 🧠 Conceptos importantes

### dnf
Es el gestor de paquetes de Fedora (reemplazo moderno de yum).

### stdin_open
Permite interacción directa con el contenedor.

### tty
Asigna una terminal virtual al contenedor.

### command
Define el proceso inicial del contenedor (en este caso `bash`).

---

Este contenedor no expone puertos porque no ejecuta servicios de red.
Está diseñado como entorno interactivo de laboratorio.
