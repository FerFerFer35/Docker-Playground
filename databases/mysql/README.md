# 📦 MySQL con Docker Compose

Este entorno levanta una instancia de MySQL utilizando la imagen oficial de Docker.

MySQL es un sistema de gestión de bases de datos relacional (RDBMS) ampliamente utilizado en aplicaciones web y backend.

---

# 📖 Imagen utilizada

```yaml
image: mysql:8.0
```

- Se utiliza la versión **8.0**
- Es una imagen oficial mantenida por el equipo de MySQL
- Basada en Linux
- Preparada para configurarse mediante variables de entorno

> ⚠️ En entornos profesionales se recomienda especificar versión y evitar `latest`.

---

# 🧱 Explicación del docker-compose.yml

```yaml
services:
  mysql:
    image: mysql:8.0
    container_name: mysql-demo
    restart: unless-stopped

    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: demo_db
      MYSQL_USER: demo_user
      MYSQL_PASSWORD: demo_password

    ports:
      - "3306:3306"

    volumes:
      - mysql_data:/var/lib/mysql

volumes:
  mysql_data:
```

---

## 🔹 services

Define los contenedores que serán creados por Docker Compose.

---

## 🔹 image

```yaml
image: mysql:8.0
```

Indica la imagen que se descargará desde Docker Hub.

---

## 🔹 container_name

```yaml
container_name: mysql-demo
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

Variables de entorno requeridas por la imagen oficial:

| Variable | Descripción |
|----------|------------|
| `MYSQL_ROOT_PASSWORD` | Contraseña del usuario root |
| `MYSQL_DATABASE` | Base de datos que se crea automáticamente al iniciar |
| `MYSQL_USER` | Usuario adicional con permisos sobre la DB |
| `MYSQL_PASSWORD` | Contraseña del usuario adicional |

---

## 🔹 ports

```yaml
- "3306:3306"
```

Formato:

```
PUERTO_HOST:PUERTO_CONTENEDOR
```

- **Puerto del contenedor:** 3306 (interno de MySQL)
- **Puerto del host:** 3306 (tu máquina)

### 🔎 Diferencia entre puerto interno y externo

- `3306` del lado derecho → es el puerto dentro del contenedor.
- `3306` del lado izquierdo → es el puerto expuesto en tu máquina.

Si cambias a:

```yaml
- "3307:3306"
```

Entonces:

- Te conectas desde tu máquina al puerto **3307**
- Pero internamente MySQL sigue usando **3306**

Esto es útil cuando ya tienes un MySQL instalado localmente.

---

## 🔹 volumes

```yaml
- mysql_data:/var/lib/mysql
```

Permite persistencia de datos.

Sin volumen:
- Si eliminas el contenedor → pierdes los datos.

Con volumen:
- Los datos sobreviven aunque el contenedor sea eliminado.

La ruta `/var/lib/mysql` es donde MySQL almacena sus datos internamente.

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
- Puerto: `3306` (o el que hayas definido en el lado izquierdo)
- Usuario: `demo_user`
- Contraseña: `demo_password`
- Base de datos: `demo_db`

También puedes conectarte como root:

- Usuario: `root`
- Contraseña: `rootpassword`

---

# 🧪 Probar conexión desde terminal

```bash
docker exec -it mysql-demo mysql -u root -p
```

---

# 🎯 Qué demuestra este ejemplo

- Uso de imagen oficial
- Configuración mediante variables de entorno
- Exposición de puertos
- Persistencia con volúmenes
- Gestión básica con Docker Compose
