# 📦 PostgreSQL con Docker Compose

Este entorno levanta una instancia de PostgreSQL utilizando la imagen oficial de Docker.

PostgreSQL es un sistema de gestión de bases de datos relacional (RDBMS) avanzado, conocido por su robustez, cumplimiento de estándares SQL y soporte para tipos de datos complejos.

---

# 📖 Imagen utilizada

```yaml
image: postgres:16
```

- Se utiliza la versión **16**
- Es una imagen oficial mantenida por el equipo de PostgreSQL
- Basada en Linux
- Permite inicialización mediante variables de entorno

> ⚠️ En entornos profesionales se recomienda especificar versión y evitar `latest`.

---

# 🧱 Explicación del docker-compose.yml

```yaml
services:
  postgres:
    image: postgres:16
    container_name: postgres-demo
    restart: unless-stopped

    environment:
      POSTGRES_USER: demo_user
      POSTGRES_PASSWORD: demo_password
      POSTGRES_DB: demo_db

    ports:
      - "5432:5432"

    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

---

## 🔹 services

Define los contenedores que serán creados por Docker Compose.

---

## 🔹 image

```yaml
image: postgres:16
```

Indica la imagen que se descargará desde Docker Hub.

---

## 🔹 container_name

```yaml
container_name: postgres-demo
```

Nombre personalizado del contenedor para facilitar su identificación.

---

## 🔹 restart

```yaml
restart: unless-stopped
```

- Reinicia el contenedor automáticamente si falla.
- Solo se detiene si se detiene manualmente.

---

## 🔹 environment

Variables de entorno soportadas por la imagen oficial:

| Variable | Descripción |
|----------|------------|
| `POSTGRES_USER` | Usuario administrador inicial |
| `POSTGRES_PASSWORD` | Contraseña del usuario |
| `POSTGRES_DB` | Base de datos que se crea automáticamente |

Estas variables se ejecutan únicamente cuando el contenedor se inicia por primera vez (si no existe volumen previo).

---

## 🔹 ports

```yaml
- "5432:5432"
```

Formato:

```
PUERTO_HOST:PUERTO_CONTENEDOR
```

- **Puerto del contenedor:** 5432 (interno de PostgreSQL)
- **Puerto del host:** 5432 (tu máquina)

### 🔎 Diferencia entre puerto interno y externo

- `5432` del lado derecho → puerto interno del contenedor.
- `5432` del lado izquierdo → puerto expuesto en tu máquina.

Si cambias a:

```yaml
- "5433:5432"
```

Entonces:

- Te conectas desde tu máquina al puerto **5433**
- Pero internamente PostgreSQL sigue usando **5432**

Esto es útil si ya tienes PostgreSQL instalado localmente.

---

## 🔹 volumes

```yaml
- postgres_data:/var/lib/postgresql/data
```

Permite persistencia de datos.

Sin volumen:
- Si eliminas el contenedor → pierdes los datos.

Con volumen:
- Los datos sobreviven aunque el contenedor sea eliminado.

La ruta `/var/lib/postgresql/data` es donde PostgreSQL almacena sus datos internamente.

---

# 🚀 Cómo ejecutar el entorno

Desde la carpeta donde se encuentra el `docker-compose.yml`:

```bash
docker compose up -d
```

Ver contenedores activos:

```bash
docker ps
```

Detener:

```bash
docker compose down
```

Eliminar también el volumen (borra los datos):

```bash
docker compose down -v
```

---

# 🔌 Cómo conectarse a la base de datos

Desde tu máquina (host):

- Host: `localhost`
- Puerto: `5432` (o el que hayas definido en el lado izquierdo)
- Usuario: `demo_user`
- Contraseña: `demo_password`
- Base de datos: `demo_db`

Cadena de conexión ejemplo:

```
postgresql://demo_user:demo_password@localhost:5432/demo_db
```

---

# 🧪 Probar conexión desde terminal

```bash
docker exec -it postgres-demo psql -U demo_user -d demo_db
```

---

# 🎯 Qué demuestra este ejemplo

- Uso de imagen oficial
- Inicialización mediante variables de entorno
- Exposición de puertos
- Persistencia con volúmenes
- Gestión básica con Docker Compose
