# Kali Linux - Docker Image

## 📌 Descripción

Este entorno utiliza la imagen oficial de Kali Linux para crear un contenedor interactivo orientado a pruebas de seguridad y análisis.

Kali Linux es una distribución basada en Debian especializada en seguridad informática, pruebas de penetración y auditoría. Es ideal para:

- Simular entornos de pruebas de seguridad
- Explorar herramientas de análisis
- Practicar comandos avanzados de red
- Entender diferencias entre una distro tradicional y una enfocada en seguridad

Este ejemplo forma parte de la sección **operating-systems**, cuyo objetivo es comprender distintos sistemas base dentro de Docker.

---

## 🏷 Imagen utilizada

`kalilinux/kali-rolling:latest`

---

## ⚙️ Configuración del servicio

| Propiedad        | Valor                          | Descripción |
|------------------|--------------------------------|-------------|
| image            | kalilinux/kali-rolling:latest  | Imagen oficial de Kali Linux |
| container_name   | kali-demo                      | Nombre personalizado del contenedor |
| stdin_open       | true                           | Permite mantener STDIN abierto |
| tty              | true                           | Asigna una terminal interactiva |
| command          | bash                           | Inicia la shell Bash |

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
docker exec -it kali-demo bash
```

Ahora estarás dentro del sistema Kali Linux del contenedor.

---

## 📦 Actualizar e instalar herramientas

Kali está basado en Debian y utiliza `apt`.

Actualizar repositorios:

```bash
apt update
```

Actualizar el sistema:

```bash
apt upgrade -y
```

Instalar herramientas específicas:

```bash
apt install nmap -y
apt install net-tools -y
```

---

## 🔍 Ver tamaño de la imagen

Desde tu máquina host:

```bash
docker images
```

Esto te permitirá comparar Kali con Debian, Ubuntu u otras distribuciones.

---

## 🧹 Detener y eliminar el entorno

Para detener el contenedor:

```bash
docker compose down
```

---

## ⚠️ Nota importante

Este contenedor no está configurado para realizar pruebas reales contra redes externas.  
Debe utilizarse únicamente con fines educativos y en entornos controlados.

---

## 🧠 Conceptos importantes

### Kali Linux
Distribución especializada en seguridad informática y pruebas de penetración.

### apt
Gestor de paquetes heredado de Debian.

### stdin_open
Permite interacción directa con el contenedor.

### tty
Asigna una terminal virtual al contenedor.

### command
Define el proceso inicial del contenedor (en este caso `bash`).

---

Este contenedor no expone puertos porque no ejecuta servicios de red por defecto.
Está diseñado como entorno interactivo de laboratorio.
