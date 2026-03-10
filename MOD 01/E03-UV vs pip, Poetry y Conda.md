# E03 — UV vs pip, Poetry y Conda

## 🐍 Comandos con pip (entorno virtual clásico)

```powershell
# Crear el entorno virtual
python -m venv entorno-pip

# Activar el entorno
entorno-pip\Scripts\activate

# Limpiar la caché de pip
pip cache purge

# Instalar paquetes (tardó ~32 segundos)
pip install requests fastapi uvicorn sqlalchemy pydantic httpx pytest black

# Desactivar el entorno
deactivate

# Eliminar el entorno
Remove-Item -Recurse -Force entorno-pip
```

---

## ⚡ Comandos con UV

```powershell
# Crear el entorno virtual
uv venv entorno-uv

# Activar el entorno
entorno-uv\Scripts\activate

# Limpiar la caché de uv
uv cache clean

# Instalar paquetes (tardó ~7 segundos)
uv pip install requests fastapi uvicorn sqlalchemy pydantic httpx pytest black
```

> 💡 **Mismos 8 paquetes, pip tardó 32 s — UV tardó 7 s (~4.5× más rápido).**

---

## 📊 Comparativa de comandos

| Acción | pip | Poetry | Conda | UV |
|---|---|---|---|---|
| Crear entorno | `python -m venv .venv` | `poetry env use 3.x` | `conda create -n env` | `uv venv` |
| Activar entorno | `.venv\Scripts\activate` | (automático) | `conda activate env` | (automático con `uv run`) |
| Instalar paquete | `pip install requests` | `poetry add requests` | `conda install requests` | `uv add requests` |
| Instalar dev deps | `pip install pytest` (manual) | `poetry add --dev pytest` | `conda install pytest` | `uv add --dev pytest` |
| Desinstalar paquete | `pip uninstall requests` | `poetry remove requests` | `conda remove requests` | `uv remove requests` |
| Ver dependencias | `pip list` | `poetry show` | `conda list` | `uv pip list` |
| Lock de dependencias | `pip freeze > req.txt` | `poetry.lock` (auto) | `conda env export` | `uv.lock` (auto) |
| Instalar desde lock | `pip install -r req.txt` | `poetry install` | `conda env create -f env.yml` | `uv sync` |
| Ejecutar script | `python script.py` | `poetry run python s.py` | `conda run python s.py` | `uv run script.py` |
| Gestionar Python | no incluido (pyenv aparte) | no incluido | incluido (envs) | `uv python install 3.12` |
| Init proyecto | manual | `poetry new proyecto` | manual | `uv init proyecto` |
| Publicar en PyPI | `twine upload` | `poetry publish` | no aplica | `uv publish` |

---

## 🧭 Tabla de decisión

| Herramienta | ✅ Usalo cuando... | ⚠️ Pensalo dos veces si... |
|---|---|---|
| **UV** | Proyectos nuevos, equipos modernos, CI/CD, cualquier proyecto Python donde querés velocidad y reproducibilidad. Es la opción por defecto hoy. | El equipo tiene procesos muy establecidos con otra herramienta y el costo de migración supera el beneficio inmediato. |
| **pip** | Scripts rápidos y simples, entornos donde solo tenés Python disponible, compatibilidad con sistemas legacy, tutoriales y documentación que no querés reescribir. | Proyectos con múltiples dependencias, trabajo en equipo o CI/CD — ahí pip solo se queda corto. |
| **Poetry** | Equipos que ya lo usan y están conformes, proyectos con configuración muy específica de Poetry, flujos de publicación de librerías ya establecidos con Poetry. | Proyectos nuevos — UV hace lo mismo y más rápido. La curva de migración de Poetry a UV es baja. |
| **Conda** | Data Science, Machine Learning, proyectos con dependencias no-Python (CUDA, MKL, C libs). Conda maneja dependencias de sistema que pip y UV no tocan. | Desarrollo web estándar o proyectos pure-Python — el overhead de Conda no vale la pena fuera del ecosistema científico. |
