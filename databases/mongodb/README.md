# 📦 MongoDB con Docker Compose

Este entorno levanta una instancia de MongoDB utilizando la imagen oficial de Docker.

MongoDB es un sistema de gestión de bases de datos NoSQL orientado a documentos, ampliamente utilizado en aplicaciones modernas, APIs y arquitecturas basadas en microservicios.

---

# 📖 Imagen utilizada

```yaml
image: mongo:7.0
```

- Se utiliza la versión **7.0**
- Es una imagen oficial mantenida por el equipo de MongoDB
- Basada en Linux
- Permite inicialización mediante variables de entorno

> ⚠️ En entornos profesionales se recomienda especificar versión y evitar `latest`.

---

# 🧱 Explicación del docker-compose.yml

```yaml
services:
  mongo:
    image: mongo:7.0
    container_name: mongo-demo
    restart: unless-stopped

    environment:
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: rootpassword
      MONGO_INITDB_DATABASE: demo_db

    ports:
      - "27017:27017"

    volumes:
      - mongo_data:/data/db

volumes:
  mongo_data:
```

---

## 🔹 services

Define los contenedores que serán creados por Docker Compose.

---

## 🔹 image

```yaml
image: mongo:7.0
```

Indica la imagen que se descargará desde Docker Hub.

---

## 🔹 container_name

```yaml
container_name: mongo-demo
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
| `MONGO_INITDB_ROOT_USERNAME` | Usuario administrador inicial |
| `MONGO_INITDB_ROOT_PASSWORD` | Contraseña del usuario administrador |
| `MONGO_INITDB_DATABASE` | Base de datos que se crea al iniciar |

Estas variables se ejecutan únicamente cuando el contenedor se inicia por primera vez (si no existe volumen previo).

---

## 🔹 ports

```yaml
- "27017:27017"
```

Formato:

```
PUERTO_HOST:PUERTO_CONTENEDOR
```

- **Puerto del contenedor:** 27017 (interno de MongoDB)
- **Puerto del host:** 27017 (tu máquina)

### 🔎 Diferencia entre puerto interno y externo

- `27017` del lado derecho → puerto interno del contenedor.
- `27017` del lado izquierdo → puerto expuesto en tu máquina.

Si cambias a:

```yaml
- "27018:27017"
```

Entonces:

- Te conectas desde tu máquina al puerto **27018**
- Pero internamente MongoDB sigue usando **27017**

---

## 🔹 volumes

```yaml
- mongo_data:/data/db
```

Permite persistencia de datos.

Sin volumen:
- Si eliminas el contenedor → pierdes los datos.

Con volumen:
- Los datos sobreviven aunque el contenedor sea eliminado.

La ruta `/data/db` es donde MongoDB almacena sus datos internamente.

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
- Puerto: `27017` (o el que hayas definido en el lado izquierdo)
- Usuario: `root`
- Contraseña: `rootpassword`
- Base de datos inicial: `demo_db`

Cadena de conexión ejemplo:

```
mongodb://root:rootpassword@localhost:27017
```

---

# 🧪 Probar conexión desde terminal

```bash
docker exec -it mongo-demo mongosh -u root -p
```

---

# 🎯 Qué demuestra este ejemplo

- Uso de imagen oficial
- Inicialización mediante variables de entorno
- Exposición de puertos
- Persistencia con volúmenes
- Gestión básica con Docker Compose
