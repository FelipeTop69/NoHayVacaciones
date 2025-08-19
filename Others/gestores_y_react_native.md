# 🚀 Guía de Gestores de Paquetes y Creación de Proyectos React Native

## 📦 Gestores de Paquetes en JavaScript/Node.js

### 🔹 1. npm (Node Package Manager)
- **Qué es**: Administrador de paquetes oficial que viene con Node.js.
- **Cómo funciona**:
  - Instala dependencias en `node_modules`.
  - Usa `package-lock.json` para versiones fijas.
- ✅ **Ventajas**:
  - Oficial y siempre disponible.
  - Gran comunidad.
  - Desde v7 soporta **workspaces**.
- ❌ **Desventajas**:
  - `node_modules` ocupa mucho espacio.
  - Más lento comparado con pnpm/yarn (aunque mejoró).

---

### 🔹 2. Yarn (Facebook/Meta)
- **Qué es**: Gestor creado para mejorar a npm (2016).
- **Cómo funciona**:
  - Usa caché local para no descargar lo mismo varias veces.
  - Usa `yarn.lock`.
- ✅ **Ventajas**:
  - Más rápido que npm en sus inicios.
  - Soporte nativo para workspaces.
  - Instalaciones determinísticas.
- ❌ **Desventajas**:
  - npm ya se puso al día.
  - Dos versiones: Yarn Classic (v1) y Yarn Berry (v2+), que cambia mucho.

---

### 🔹 3. pnpm (Performant npm)
- **Qué es**: Gestor moderno y eficiente.
- **Cómo funciona**:
  - Usa un **almacén global** de paquetes.
  - Crea **symlinks** en cada proyecto.
- ✅ **Ventajas**:
  - Muy rápido.
  - Ahorra espacio en disco.
  - Estricto en resolución de dependencias.
- ❌ **Desventajas**:
  - Menos popular (pero creciendo).
  - Algunos paquetes antiguos fallan con su estructura.

---

## 🚀 Comparativa rápida

| Gestor  | Velocidad 🚀 | Uso de espacio 💾 | Popularidad 🌍 | Workspaces 🧩 | Comentario |
|---------|--------------|------------------|----------------|---------------|-------------|
| **npm** | Medio        | Alto             | Muy alto       | Sí (v7+)      | Oficial, estable |
| **yarn**| Medio-Alto   | Medio            | Alto           | Sí            | Fue más rápido, ahora menos necesario |
| **pnpm**| Muy alto     | Muy bajo         | En crecimiento | Sí            | Ideal para proyectos grandes |

---

## 📱 Creación de proyectos React Native

### 🔹 A. Usando React Native CLI (control total)
```bash
npm install -g react-native-cli
npx react-native init MiApp
cd MiApp
npm install
npx react-native start        # Iniciar Metro bundler
npx react-native run-android  # Ejecutar en Android
npx react-native run-ios      # Ejecutar en iOS (Mac)
```

---

### 🔹 B. Usando Expo CLI (más fácil para empezar)
```bash
npm install -g expo-cli
npx create-expo-app MiAppExpo
cd MiAppExpo
npm install
npx expo start
```
- Abre un servidor con un **QR** para probar en Expo Go.

---

## 📑 Resumen de comandos npm

| Comando | Uso |
|---------|-----|
| `npx create-react-app mi-app` | Crear proyecto React web |
| `npx react-native init MiApp` | Crear proyecto React Native |
| `cd mi-app` | Entrar al proyecto |
| `npm install` | Instalar dependencias |
| `npm start` | Iniciar servidor |
| `npm run build` | Compilar para producción (web) |
| `npx react-native run-android` | Ejecutar en Android |
| `npx react-native run-ios` | Ejecutar en iOS |

---

✨ **Conclusión**:  
- Usa **npm** si quieres lo oficial y estable.  
- Usa **yarn** si tu equipo ya lo maneja.  
- Usa **pnpm** si quieres rapidez y eficiencia en proyectos grandes.  
