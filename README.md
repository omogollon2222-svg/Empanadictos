# Empanadictos 🥟

App de caja, comandas de cocina, inventario, cierre de caja y análisis de ventas.
Funciona en celular, tablet o computadora, directamente en el navegador.

## Archivos

| Archivo | Para qué sirve |
|---|---|
| `index.html` | La app completa |
| `firebase-config.js` | Conexión en la nube (opcional, para sincronizar caja y cocina) |
| `manifest.json`, `icon*.png`, `icon.svg` | Permiten instalarla como app en el celular |
| `firestore.rules` | Reglas de seguridad para Firebase (paso 3) |
| `.nojekyll` | Le dice a GitHub Pages que publique los archivos tal cual |

## 1. Subir a GitHub

1. Entra a github.com → **New repository** → nombre: `empanadictos` → **Public** → *Create repository*.
2. Haz clic en **uploading an existing file** y arrastra **todos** los archivos de esta carpeta
   (en Windows, el archivo `.nojekyll` puede estar oculto; si no aparece, no pasa nada grave).
3. Clic en **Commit changes**.

## 2. Publicar la web (GitHub Pages)

1. En el repositorio: **Settings → Pages**.
2. En *Source* elige **Deploy from a branch**, rama **main**, carpeta **/ (root)** → **Save**.
3. En 1–2 minutos tu app estará en: `https://TU-USUARIO.github.io/empanadictos/`

**Instalar en el celular:** abre el enlace → menú del navegador → *Agregar a pantalla de inicio*.

> ⚠️ Sin el paso 3, cada dispositivo guarda sus propios datos. La caja y la cocina
> **no** se verán entre sí si están en dispositivos distintos.

## 3. Sincronizar caja y cocina (Firebase, gratis)

1. Entra a https://console.firebase.google.com → **Agregar proyecto** → nombre `empanadictos` (puedes desactivar Analytics).
2. Menú **Compilación → Firestore Database → Crear base de datos** → ubicación cercana (ej. `southamerica-east1`) → modo **producción**.
3. Pestaña **Reglas**: pega el contenido de `firestore.rules` → **Publicar**.
4. Ve a ⚙️ **Configuración del proyecto → Tus apps → Web (`</>`)** → registra la app → copia el bloque `firebaseConfig`.
5. En GitHub abre `firebase-config.js` → ✏️ editar → pega los valores (apiKey, projectId, etc.) → **Commit changes**.
6. Recarga la app: arriba a la derecha dirá **"Guardado en la nube"**.

El plan gratuito de Firebase (Spark) alcanza de sobra para un local: 50.000 lecturas y 20.000 escrituras por día.

## Seguridad

- Las claves de Ventas y Cocina se guardan cifradas (SHA-256).
- Las reglas de `firestore.rules` limitan el acceso a las colecciones de la app, pero quien tenga
  la dirección de la web y conocimientos técnicos podría leer los datos. Para un local pequeño
  suele ser suficiente; si quieres más protección, se puede agregar inicio de sesión con Firebase Auth.
