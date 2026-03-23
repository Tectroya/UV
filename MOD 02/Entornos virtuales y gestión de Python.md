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
