# Jupyter Notebook - Docker Environment

## 📌 Descripción

Este entorno levanta una instancia de Jupyter Notebook utilizando la imagen oficial base.

Jupyter permite crear y ejecutar notebooks interactivos que combinan:

- Código
- Visualizaciones
- Markdown
- Resultados en tiempo real

Es ampliamente utilizado en:

- Ciencia de datos
- Machine Learning
- Análisis estadístico
- Investigación académica
- Automatización de scripts Python

Este ejemplo forma parte de la sección **developer-tools**, mostrando cómo levantar herramientas de productividad y análisis en Docker con un solo comando.

---

## 🏷 Imagen utilizada

- `jupyter/base-notebook:latest`

---

## ⚙️ Arquitectura

El entorno consta de un único servicio:

### Jupyter Notebook

Expone el puerto 8888 y monta un volumen local para persistir notebooks.

---

## 🔌 Puertos

| Tipo                     | Puerto |
|--------------------------|--------|
| Puerto interno Jupyter  | 8888   |
| Puerto externo          | 8888   |

Acceso:

```
http://localhost:8888
```

---

## 💾 Persistencia

Se monta el directorio local:

```
./notebooks
```

Dentro del contenedor en:

```
/home/jovyan/work
```

Todo archivo creado dentro del entorno Jupyter quedará guardado en tu máquina local.

---

## 🚀 Cómo ejecutarlo

Desde la carpeta donde está el `docker-compose.yml`:

```bash
docker compose up -d
```

Luego abrir en navegador:

```
http://localhost:8888
```

El token de acceso se mostrará en los logs del contenedor:

```bash
docker logs jupyter-notebook
```

---

## 🧠 Conceptos importantes

### Volúmenes
Permiten persistir notebooks incluso si el contenedor se elimina.

### Imagen base-notebook
Incluye:

- Python
- pip
- Conda
- Jupyter Notebook
- JupyterLab (habilitado con variable de entorno)

---

## 🧹 Detener el entorno

```bash
docker compose down
```

---

Este entorno está pensado para desarrollo local y experimentación.
No se recomienda exponerlo directamente a internet sin autenticación adicional.
