# PrestaShop - Docker Environment

## 📌 Descripción

Este entorno utiliza la imagen oficial de PrestaShop junto con MySQL para levantar una plataforma completa de comercio electrónico en Docker.

PrestaShop es una solución open source para crear tiendas en línea que permite:

- Gestión de productos y categorías
- Administración de pedidos
- Control de inventario
- Configuración de pagos y envíos
- Gestión de clientes

Este ejemplo forma parte de la sección **enterprise-apps / full-environments**, demostrando cómo ejecutar aplicaciones empresariales completas con múltiples servicios en Docker.

---

## 🏷 Imágenes utilizadas

- `prestashop/prestashop:latest`
- `mysql:8.0`

---

## ⚙️ Arquitectura del entorno

El entorno está compuesto por dos servicios:

### 1️⃣ MySQL (db)
Base de datos utilizada por PrestaShop.

### 2️⃣ PrestaShop (app)
Aplicación principal que se conecta a la base de datos MySQL.

---

## 🔌 Puertos

| Tipo                       | Puerto |
|----------------------------|--------|
| Puerto interno PrestaShop  | 80     |
| Puerto externo PrestaShop  | 8082   |
| Puerto interno MySQL       | 3306   |

Acceso desde navegador:

```
http://localhost:8082
```

---

## 🔐 Variables de entorno

### MySQL

| Variable             | Valor       | Descripción |
|----------------------|------------|-------------|
| MYSQL_ROOT_PASSWORD  | root       | Contraseña del usuario root |
| MYSQL_DATABASE       | prestashop | Base de datos inicial |
| MYSQL_USER           | psuser     | Usuario de la base de datos |
| MYSQL_PASSWORD       | pspass     | Contraseña del usuario |

### PrestaShop

| Variable   | Valor       | Descripción |
|------------|------------|-------------|
| DB_SERVER  | db         | Nombre del servicio MySQL |
| DB_NAME    | prestashop | Base de datos |
| DB_USER    | psuser     | Usuario de la base de datos |
| DB_PASSWD  | pspass     | Contraseña |

---

## 💾 Persistencia de datos

Se definen dos volúmenes:

```
prestashop_db
prestashop_data
```

- `prestashop_db`: almacena los datos de MySQL
- `prestashop_data`: almacena archivos y configuraciones de la tienda

Esto permite conservar la información aunque los contenedores se detengan.

---

## 🚀 Cómo ejecutarlo

Desde la carpeta donde se encuentra el `docker-compose.yml`:

```bash
docker compose up -d
```

---

## 🌐 Instalación inicial

Abrir en navegador:

```
http://localhost:8082
```

Seguir el asistente de instalación de PrestaShop.

---

## 🧹 Detener el entorno

```bash
docker compose down
```

Si deseas eliminar también los datos:

```bash
docker compose down -v
```

---

## 🧠 Conceptos importantes

### depends_on
Asegura que MySQL inicie antes que la aplicación.

### Red interna Docker
PrestaShop se conecta a MySQL usando el nombre del servicio (`db`) como host.

### Puerto externo vs interno

Formato:
```
HOST:CONTENEDOR
```

En este caso:
```
8082:80
```

- 8082 → puerto del host
- 80 → puerto interno del contenedor

---

Este entorno está diseñado para desarrollo local.
No se recomienda usar credenciales simples en producción.
