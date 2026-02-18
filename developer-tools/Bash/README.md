# Bash - Docker Image

## 📌 Descripción

Este entorno utiliza una imagen ligera que incluye Bash para crear un contenedor interactivo enfocado en práctica de scripting y comandos de terminal.

Bash es uno de los intérpretes de comandos más utilizados en sistemas Unix/Linux y es fundamental para:

- Automatización de tareas
- Creación de scripts
- Administración de sistemas
- Manipulación de archivos y procesos
- DevOps y CI/CD

Este ejemplo forma parte de la sección **developer-tools**, cuyo objetivo es incluir herramientas esenciales para desarrolladores.

---

## 🏷 Imagen utilizada

`bash:latest`

---

## ⚙️ Configuración del servicio

| Propiedad        | Valor         | Descripción |
|------------------|--------------|-------------|
| image            | bash:latest  | Imagen ligera con Bash |
| container_name   | bash-demo    | Nombre personalizado del contenedor |
| stdin_open       | true         | Permite mantener STDIN abierto |
| tty              | true         | Asigna una terminal interactiva |
| command          | bash         | Inicia la shell Bash |

---

## 🚀 Cómo ejecutarlo

Desde la carpeta donde se encuentra el `docker-compose.yml`:

```bash
docker compose up -d
```

---

## 🔐 Cómo acceder al contenedor

```bash
docker exec -it bash-demo bash
```

Ahora estarás dentro de un entorno Bash interactivo.

---

## 🧪 Ejemplos básicos

Listar archivos:

```bash
ls -la
```

Crear un archivo:

```bash
touch ejemplo.txt
```

Crear un script:

```bash
nano script.sh
```

Contenido del script:

```bash
#!/bin/bash
echo "Hola desde Docker y Bash"
```

Dar permisos y ejecutar:

```bash
chmod +x script.sh
./script.sh
```

---

## 📁 Persistencia (Opcional)

Si deseas trabajar con archivos de tu máquina host, puedes modificar el `docker-compose.yml` y agregar:

```yaml
volumes:
  - ./workspace:/workspace
```

Y luego trabajar dentro de `/workspace`.

---

## 🧹 Detener el entorno

```bash
docker compose down
```

---

## 🧠 Conceptos importantes

### Bash
Intérprete de comandos ampliamente utilizado en sistemas Unix/Linux.

### stdin_open
Permite interacción directa con el contenedor.

### tty
Asigna una terminal virtual al contenedor.

### command
Define el proceso inicial del contenedor.

---

Este contenedor no expone puertos porque no ejecuta servicios de red.
Está diseñado como entorno interactivo para práctica de terminal y scripting.
