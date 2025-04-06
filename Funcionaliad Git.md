¡Genial! Te dejo aquí un script listo para guardar como `descargar_parte_repo.sh` (o el nombre que prefieras). Solo necesitás darle permisos de ejecución y correrlo pasando la **URL del repo**, la **rama**, y la **ruta que quieres bajar**.

---

### 📜 **Script: `descargar_parte_repo.sh`**

```bash
#!/bin/bash

# ✅ Script para clonar solo una carpeta o archivo específico de un repo de GitHub
# 👉 Uso:
# ./descargar_parte_repo.sh <repo_url> <rama> <ruta/que/quieres>

# 📌 Ejemplo:
# ./descargar_parte_repo.sh https://github.com/IsabelTovar08/ADSO-2900177.git main "tecnico/2025/Marzo/c#/ModelSecurityProyecto/Diagram"

REPO_URL="$1"
BRANCH="$2"
TARGET_PATH="$3"

# Validación
if [ -z "$REPO_URL" ] || [ -z "$BRANCH" ] || [ -z "$TARGET_PATH" ]; then
  echo "❌ Uso incorrecto."
  echo "👉 Uso: $0 <repo_url> <rama> <ruta/a/descargar>"
  exit 1
fi

# Extraer nombre del directorio del repo
REPO_DIR=$(basename "$REPO_URL" .git)

# 1. Clonar sin checkout
git clone --filter=blob:none --no-checkout "$REPO_URL"
cd "$REPO_DIR" || exit

# 2. Activar sparse-checkout
git sparse-checkout init --cone

# 3. Elegir ruta a descargar
git sparse-checkout set "$TARGET_PATH"

# 4. Hacer checkout de la rama
git checkout "$BRANCH"

echo "✅ Descarga completada: $TARGET_PATH"
```

---

### ✅ Cómo usarlo:

1. Guarda el script:

```bash
nano descargar_parte_repo.sh
```

(Pega el contenido, guarda con `Ctrl+O` y sal con `Ctrl+X`)

2. Dale permisos:

```bash
chmod +x descargar_parte_repo.sh
```

3. Ejecútalo, por ejemplo:

```bash
./descargar_parte_repo.sh https://github.com/IsabelTovar08/ADSO-2900177.git main "tecnico/2025/Marzo/c#/ModelSecurityProyecto/Diagram"
```

---
