# Módulo 2 — Entornos virtuales y gestión de Python

## E04 - Crear y activar entornos virtuales

```bash
uv venv                  # entorno con Python del sistema
uv venv .venv            # nombre explícito
uv venv --python 3.12    # Python específico
```

### Activar el entorno virtual

```bash
# Windows
.venv\Scripts\activate

# macOS/Linux
source .venv/bin/activate
```

### Desactivar el entorno virtual

```bash
deactivate
```

### Tabla comparativa: `python -m venv` vs `uv venv`

| | `python -m venv` | `uv venv` |
|---|---|---|
| Velocidad de creación | ~2-4 segundos | < 0.5 segundos |
| Nombre por defecto | Ninguno (obligatorio darlo) | `.venv` (automático) |
| Gestiona Python | No — usa el Python del sistema | Sí — descarga si no existe |
| Requiere Python previo | Sí — siempre | No — UV lo gestiona |
| Integración proyecto | Manual | Automática con `pyproject.toml` |
| Detección en IDEs | Depende del nombre | `.venv` detectado automáticamente |

### Activar y desactivar por sistema operativo

| Sistema / Shell | Activar | Desactivar |
|---|---|---|
| Windows (PowerShell) | `.venv\Scripts\activate` | `deactivate` |
| Windows (CMD) | `.venv\Scripts\activate.bat` | `deactivate` |
| macOS / Linux (bash/zsh) | `source .venv/bin/activate` | `deactivate` |
| macOS / Linux (fish) | `source .venv/bin/activate.fish` | `deactivate` |

### Buenas prácticas

- ✅ Siempre llamar al entorno `.venv` — es la convención moderna y todos los IDEs lo detectan automáticamente.
- ✅ Agregar `.venv/` al `.gitignore` — NUNCA subir el entorno a GitHub. Solo sube `pyproject.toml` y `uv.lock`.
- ✅ Un entorno por proyecto — no compartir entornos entre proyectos distintos.
- ✅ Usar `uv run` en lugar de activar/desactivar constantemente — más limpio y menos propenso a errores.
- ❌ No crear el entorno con `python -m venv` si ya tienes UV — usa siempre `uv venv` para aprovechar la velocidad y la integración.
- ❌ No instalar paquetes en el Python del sistema — siempre dentro de un entorno virtual.

---

## E05 - Gestión de versiones de Python con UV

```bash
uv python list
```

```
cpython-3.14.0a4   <download available>
cpython-3.13.2     C:\Users\...\AppData\Local\Programs\Python\Python313\python.exe
cpython-3.12.9     <download available>
cpython-3.11.11    <download available>
cpython-3.10.16    <download available>
cpython-3.9.21     <download available>
...
```

```bash
uv python list --only-installed    # solo las versiones ya instaladas
uv python list --only-downloads    # solo las disponibles para descargar
```

### Instalar versiones de Python

```bash
uv python install 3.11               # instala una versión específica
uv python install 3.10 3.11 3.12     # instala varias a la vez
```

### Fijar la versión del proyecto

```bash
uv python pin 3.11    # crea o actualiza el archivo .python-version
```

En `pyproject.toml`:

```toml
[project]
requires-python = ">=3.11"
```

### Tabla comparativa: `pyenv` vs UV

| Característica | pyenv | UV |
|---|---|---|
| Instalación | Proceso separado y complejo en Windows | Incluido con UV — ya lo tienes |
| Listar versiones | `pyenv install --list` | `uv python list` |
| Instalar versión | `pyenv install 3.11` | `uv python install 3.11` |
| Fijar versión global | `pyenv global 3.11` | `uv python pin 3.11` (global) |
| Fijar versión por proyecto | `pyenv local 3.11` → `.python-version` | `uv python pin 3.11` → `.python-version` |
| Ver versión activa | `pyenv version` | `uv python list --only-installed` |
| Desinstalar versión | `pyenv uninstall 3.11` | `uv python uninstall 3.11` |
| Soporte Windows | pyenv-win (proyecto separado, limitado) | Nativo — funciona igual en todos los OS |
| Integración con entornos | Manual con virtualenv | Automática con `uv venv` y `uv run` |
