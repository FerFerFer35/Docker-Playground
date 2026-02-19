# Odoo - Docker Environment

## 📌 Descripción

Este entorno utiliza la imagen oficial de Odoo junto con PostgreSQL para levantar un ERP completo en Docker.

Odoo es una plataforma empresarial modular que permite gestionar:

- Ventas
- Inventario
- Facturación
- Contabilidad
- CRM
- Recursos humanos
- Comercio electrónico

Este ejemplo demuestra cómo ejecutar aplicaciones empresariales completas con múltiples servicios en Docker.

---

## 🏷 Imágenes utilizadas

- `odoo:17`
- `postgres:16`

---

## ⚙️ Arquitectura del entorno

El entorno está compuesto por dos servicios:

### 1️⃣ PostgreSQL (db)
Base de datos utilizada por Odoo.

### 2️⃣ Odoo (app)
Aplicación principal del ERP que se conecta a PostgreSQL.

---

## 🔌 Puertos

| Tipo                   | Puerto |
|------------------------|--------|
| Puerto interno Odoo   | 8069   |
| Puerto externo Odoo   | 8069   |
| Puerto interno Postgres| 5432  |

Acceso desde navegador:

```
http://localhost:8069
```

---

## 🔐 Variables de entorno

### PostgreSQL

| Variable           | Valor  | Descripción |
|--------------------|--------|-------------|
| POSTGRES_DB        | postgres | Base de datos inicial |
| POSTGRES_USER      | odoo     | Usuario de base de datos |
| POSTGRES_PASSWORD  | odoo     | Contraseña del usuario |

### Odoo

| Variable  | Valor | Descripción |
|-----------|-------|-------------|
| HOST      | db    | Nombre del servicio PostgreSQL |
| USER      | odoo  | Usuario de base de datos |
| PASSWORD  | odoo  | Contraseña de base de datos |

---

## 💾 Persistencia de datos

Se definen dos volúmenes:

```
odoo_db
odoo_data
```

- `odoo_db`: almacena los datos de PostgreSQL
- `odoo_data`: almacena archivos y configuraciones de Odoo

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
http://localhost:8069
```

En la primera ejecución se mostrará el asistente de creación de base de datos.

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
Asegura que el contenedor de base de datos se inicie antes que Odoo.

### Red interna Docker
Odoo se conecta a PostgreSQL usando el nombre del servicio (`db`) como host.

### Puerto externo vs interno

Formato:
```
HOST:CONTENEDOR
```

En este caso:
```
8069:8069
```

---

Este entorno está diseñado para desarrollo y pruebas.
No se recomienda usar credenciales simples en producción.
