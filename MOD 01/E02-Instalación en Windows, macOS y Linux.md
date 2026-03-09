# 🚀 E02 — Instalación de UV en Windows, macOS y Linux

> **UV** es el gestor de paquetes ultrarrápido para Python. A continuación verás cómo instalarlo en los tres sistemas operativos más usados y los primeros comandos esenciales.

---

## 🪟 Instalación en Windows

### 1. Verificar que UV no está instalado

```powershell
uv --version
```

> Si el comando no se reconoce, UV no está instalado. ¡Perfecto, sigamos!

### 2. Instalar UV (comando oficial de Astral)

Abre **PowerShell** y ejecuta:

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

### 3. Verificar la instalación

Abre una **nueva terminal** y ejecuta:

```powershell
uv --version
```

✅ Si ves el número de versión, ¡UV está listo!

---

## 🍎 Instalación en macOS

### 1. Verificar que UV no está instalado

```bash
uv --version
```

### 2. Instalar UV mediante Homebrew

```bash
brew install uv
```

> 💡 ¿No tienes Homebrew? Instálalo primero desde [https://brew.sh](https://brew.sh)

### 3. Verificar la instalación

```bash
uv --version
```

### 4. Ver dónde quedó instalado

```bash
which uv
```

✅ El comando te mostrará la ruta exacta donde se instaló el binario de UV.

---

## 🐧 Instalación en Linux (vía Docker Desktop)

> En este ejemplo usamos un **contenedor Ubuntu** para simular un entorno Linux limpio.

### 1. Levantar un contenedor Ubuntu interactivo

```bash
docker run -it ubuntu:latest bash
```

### 2. Actualizar paquetes e instalar `curl`

```bash
apt-get update && apt-get install -y curl
```

### 3. Instalar UV (instalador oficial de Astral)

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### 4. Aplicar el PATH en la sesión actual

```bash
source $HOME/.local/bin/env
```

### 5. Verificar la instalación

```bash
uv --version
```

✅ ¡UV instalado correctamente en Linux!

---

## ⚡ Primeros Comandos Esenciales

Una vez instalado UV, estos son los comandos que debes conocer desde el primer día:

| Comando | Descripción |
|---|---|
| `uv --version` | Muestra la versión de UV instalada |
| `uv --help` | Muestra la ayuda general de UV |
| `uv pip --help` | Muestra la ayuda del subcomando `pip` |
| `uv python list` | Lista las versiones de Python disponibles para instalar |
| `uv self update` | Actualiza UV a la última versión (funciona en cualquier SO) |