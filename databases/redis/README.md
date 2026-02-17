# 📦 Redis con Docker Compose

Este entorno levanta una instancia de Redis utilizando la imagen oficial de Docker.

Redis es un sistema de almacenamiento en memoria (in-memory data store) utilizado comúnmente como cache, broker de mensajes o base de datos NoSQL de alto rendimiento.

---

# 📖 Imagen utilizada

```yaml
image: redis:7.2
```

- Se utiliza la versión **7.2**
- Es una imagen oficial mantenida por el equipo de Redis
- Basada en Linux
- Puede ejecutarse con o sin autenticación

> ⚠️ En entornos profesionales se recomienda proteger Redis con contraseña.

---

# 🧱 Explicación del docker-compose.yml

```yaml
services:
  redis:
    image: redis:7.2
    container_name: redis-demo
    restart: unless-stopped

    command: redis-server --requirepass redispassword

    ports:
      - "6379:6379"

    volumes:
      - redis_data:/data

volumes:
  redis_data:
```

---

## 🔹 services

Define los contenedores que serán creados por Docker Compose.

---

## 🔹 image

```yaml
image: redis:7.2
```

Indica la imagen que se descargará desde Docker Hub.

---

## 🔹 container_name

```yaml
container_name: redis-demo
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

## 🔹 command

```yaml
command: redis-server --requirepass redispassword
```

Sobrescribe el comando por defecto para iniciar Redis con autenticación.

`--requirepass` define la contraseña obligatoria para conectarse al servidor.

Sin este parámetro, Redis permitiría conexiones sin contraseña.

---

## 🔹 ports

```yaml
- "6379:6379"
```

Formato:

```
PUERTO_HOST:PUERTO_CONTENEDOR
```

- **Puerto del contenedor:** 6379 (interno de Redis)
- **Puerto del host:** 6379 (tu máquina)

### 🔎 Diferencia entre puerto interno y externo

- `6379` del lado derecho → puerto interno del contenedor.
- `6379` del lado izquierdo → puerto expuesto en tu máquina.

Si cambias a:

```yaml
- "6380:6379"
```

Entonces:

- Te conectas desde tu máquina al puerto **6380**
- Pero internamente Redis sigue usando **6379**

Esto es útil si ya tienes Redis instalado localmente.

---

## 🔹 volumes

```yaml
- redis_data:/data
```

Permite persistencia de datos si Redis está configurado para guardar snapshots (RDB o AOF).

Sin volumen:
- Los datos se pierden al eliminar el contenedor.

Con volumen:
- Los datos pueden sobrevivir reinicios y recreaciones del contenedor.

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

# 🔌 Cómo conectarse a Redis

Desde tu máquina (host):

- Host: `localhost`
- Puerto: `6379` (o el que hayas definido en el lado izquierdo)
- Contraseña: `redispassword`

Ejemplo de conexión con URL:

```
redis://:redispassword@localhost:6379
```

---

# 🧪 Probar conexión desde terminal

Entrar al contenedor:

```bash
docker exec -it redis-demo redis-cli
```

Autenticarse:

```bash
AUTH redispassword
```

Probar un comando:

```bash
SET mensaje "Hola Redis"
GET mensaje
```

---

# 🎯 Qué demuestra este ejemplo

- Uso de imagen oficial
- Configuración personalizada mediante `command`
- Exposición de puertos
- Persistencia con volúmenes
- Uso básico de autenticación
- Gestión básica con Docker Compose
