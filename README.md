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

## 3. Sincronizar caja y cocina con seguridad (Firebase, gratis)

1. Entra a https://console.firebase.google.com → **Agregar proyecto** → `empanadictos` (puedes desactivar Analytics).
2. **Compilación → Authentication → Comenzar → Correo electrónico/contraseña → Habilitar → Guardar.**
3. En **Authentication → Usuarios → Agregar usuario**: crea la cuenta del negocio (correo + contraseña larga).
4. **Compilación → Firestore Database → Crear base de datos** → ubicación cercana → modo **producción**.
5. Pestaña **Reglas**: pega `firestore.rules` (ya trae el correo autorizado; para otra cuenta agrégala a la lista) → **Publicar**.
6. ⚙️ **Configuración del proyecto → Tus apps → Web (`</>`)** → registra la app → copia los valores de `firebaseConfig` en `firebase-config.js`.
7. En **Authentication → Configuración → Dominios autorizados** confirma que esté `TU-USUARIO.github.io`.

Cuando abras la app pedirá **correo y contraseña** (una sola vez por dispositivo). Después, cada persona entra con la clave de Ventas o de Cocina como siempre.

## Uso diario

- **Vender**: toca los productos y **Cobrar** (venta rápida) o **Abrir cuenta** para mesas que pagan al final. Los pedidos con empanadas llegan solos a Cocina.
- **Modo comanda** (interruptor arriba en Vender): encendido, los pedidos con empanadas van a la pantalla de Cocina; apagado, las ventas se registran como entregadas al instante (útil si una sola persona atiende y cocina).
- **Cocina**: entra con la clave de Cocina; cada comanda pasa por *Empezar → Marcar listo → Entregado*, en orden de llegada.
- **Inventario**: se descuenta con cada venta. *Sumar* agrega lo que se hornea o compra; *Ajustar* pone el conteo exacto. **Sin inventario no se pueden tomar pedidos** de ese producto (se registra como venta perdida).
- **⚙️ Mínimos y alertas** (administrador, en Inventario): define el mínimo de cada producto, el WhatsApp del administrador y la hora de revisión diaria. Al llegar al mínimo: aviso en caja, botón para enviar WhatsApp y notificación en los dispositivos del administrador que la activen.
- **Caja**: al final del día cuenta el efectivo y toca **Cerrar caja**; puedes ver y compartir el reporte ejecutivo.
- **Análisis**: ventas, horas fuertes, rendimiento de cocina y recomendaciones.
- **Ajustes → 📁 Google Drive**: crea un solo archivo Excel con 3 hojas (Ventas, Resumen por día, Inventario). En el celular se abre el menú de compartir: elige **Drive**. En computadora se descarga y se sube a drive.google.com. Hazlo al cerrar cada día o cada semana.
- **Ajustes → 💾 Respaldo**: descarga una copia completa o las ventas para Excel. Hazlo cada semana.

> Primer uso: en Inventario, ajusta el conteo real de cada empanada y bebida.

## Seguridad

- Sin iniciar sesión con una cuenta autorizada nadie puede leer ni cambiar datos, aunque tenga el enlace.
- Las claves de Ventas y Cocina se guardan cifradas (SHA-256) y bloquean tras 5 intentos.
- Los datos de `firebase-config.js` no son secretos: la protección la dan las reglas y el inicio de sesión.
- Si pierdes un dispositivo: cambia la contraseña en Firebase → Authentication.
- Ajustes → Seguridad → **Cerrar sesión de este dispositivo**.
