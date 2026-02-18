# phpMyAdmin - Docker Image

## 📌 Descripción

Este entorno utiliza la imagen oficial de phpMyAdmin junto con MySQL para proporcionar una interfaz web que permite administrar bases de datos de manera visual.

phpMyAdmin es ampliamente utilizado en entornos de desarrollo para:

- Crear y modificar bases de datos
- Gestionar tablas
- Ejecutar consultas SQL
- Administrar usuarios y permisos
- Importar y exportar datos

Este ejemplo forma parte de la sección **developer-tools**, permitiendo integrar herramientas visuales con bases de datos en Docker.

---

## 🏷 Imágenes utilizadas

- `mysql:8.0`
- `phpmyadmin:latest`

---

## ⚙️ Configuración del entorno

### Servicio MySQL

| Variable              | Valor   | Descripción |
|-----------------------|---------|-------------|
| MYSQL_ROOT_PASSWORD   | root    | Contraseña del usuario root |
| MYSQL_DATABASE        | app_db  | Base de datos inicial |

### Servicio phpMyAdmin

| Variable    | Valor  | Descripción |
|------------|--------|-------------|
| PMA_HOST   | mysql  | Nombre del servicio MySQL |
| PMA_PORT   | 3306   | Puerto interno de MySQL |

---

## 🚀 Cómo ejecutarlo

Desde la carpeta donde se encuentra el `docker-compose.yml`:

```bash
docker compose up -d
```

---

## 🌐 Acceso desde el navegador

```
http://localhost:8081
```

### Credenciales

Usuario:
```
root
```

Password:
```
root
```

---

## 🔌 Puerto de conexión

| Tipo              | Puerto |
|-------------------|--------|
| Interno MySQL     | 3306   |
| Externo phpMyAdmin| 8081   |

El puerto 8081 es el puerto externo expuesto para acceder desde el navegador.

---

## 💾 Persistencia de datos

El volumen:

```
mysql_data
```

permite que los datos de la base de datos no se pierdan al detener el contenedor.

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

### phpMyAdmin
Herramienta web para administración de MySQL y MariaDB.

### depends_on
Asegura que MySQL inicie antes que phpMyAdmin.

### ports
Define el puerto externo (host) y el puerto interno (contenedor).

Formato:
```
"HOST:CONTENEDOR"
```

---

Este entorno está diseñado para desarrollo local.
No se recomienda usar configuraciones básicas de contraseña en producción.
