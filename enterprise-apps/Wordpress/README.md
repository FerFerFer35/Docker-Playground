# WordPress - Docker Environment

## 📌 Descripción

Este entorno utiliza la imagen oficial de WordPress junto con MySQL para levantar un sistema completo de gestión de contenido (CMS) en Docker.

WordPress es uno de los CMS más utilizados del mundo y permite:

- Crear sitios web y blogs
- Gestionar contenido dinámico
- Instalar temas y plugins
- Administrar usuarios y permisos
- Construir entornos de desarrollo locales rápidamente

Este ejemplo forma parte de la sección **developer-tools / full-environments**, demostrando cómo levantar aplicaciones completas con múltiples servicios en Docker.

---

## 🏷 Imágenes utilizadas

- `wordpress`
- `mysql:8.0`

---

## ⚙️ Arquitectura del entorno

Este entorno contiene dos servicios:

### 1️⃣ WordPress
- Expone el puerto 8080 (externo)
- Se conecta a la base de datos MySQL
- Almacena archivos del sitio en un volumen persistente

### 2️⃣ MySQL
- Base de datos para WordPress
- Credenciales definidas mediante variables de entorno
- Datos persistentes mediante volumen Docker

---

## 🔌 Puertos

| Tipo                     | Puerto |
|--------------------------|--------|
| Puerto interno WordPress | 80     |
| Puerto externo WordPress | 8080   |
| Puerto interno MySQL     | 3306   |

El acceso al navegador se realiza mediante:

```
http://localhost:8080
```

---

## 🔐 Variables de entorno

### WordPress

| Variable                  | Valor         | Descripción |
|---------------------------|--------------|-------------|
| WORDPRESS_DB_HOST         | db           | Nombre del servicio MySQL |
| WORDPRESS_DB_USER         | exampleuser  | Usuario de la base de datos |
| WORDPRESS_DB_PASSWORD     | examplepass  | Contraseña de la base de datos |
| WORDPRESS_DB_NAME         | exampledb    | Nombre de la base de datos |

### MySQL

| Variable                   | Valor         | Descripción |
|----------------------------|--------------|-------------|
| MYSQL_DATABASE             | exampledb    | Base de datos inicial |
| MYSQL_USER                 | exampleuser  | Usuario de base de datos |
| MYSQL_PASSWORD             | examplepass  | Contraseña del usuario |
| MYSQL_RANDOM_ROOT_PASSWORD | '1'          | Genera contraseña root aleatoria |

---

## 💾 Persistencia de datos

Este entorno define dos volúmenes:

```
wordpress
db
```

- `wordpress`: almacena los archivos del sitio
- `db`: almacena los datos de la base de datos

Esto permite mantener la información incluso si los contenedores se detienen.

---

## 🚀 Cómo ejecutarlo

Desde la carpeta donde se encuentra el `docker-compose.yml`:

```bash
docker compose up -d
```

---

## 🌐 Acceso inicial

Abrir en navegador:

```
http://localhost:8080
```

Luego seguir el asistente de instalación de WordPress.

---

## 🧹 Detener el entorno

```bash
docker compose down
```

Si deseas eliminar también los volúmenes (borrando datos):

```bash
docker compose down -v
```

---

## 🧠 Conceptos importantes

### depends_on implícito
WordPress se conecta al servicio `db` usando el nombre del servicio como host dentro de la red Docker.

### Volúmenes
Permiten persistir datos fuera del ciclo de vida del contenedor.

### Puerto externo vs interno

Formato:
```
HOST:CONTENEDOR
```

En este caso:
```
8080:80
```

- 8080 → puerto del host
- 80 → puerto interno del contenedor

---

Este entorno está diseñado para desarrollo local.
No se recomienda usar credenciales de ejemplo en producción.
