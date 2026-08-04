# Mi Club Aletas

App de gestión interna para la Mesa Directiva del Club Aletas Copacabana.
Un solo archivo (`index.html`), sin build, con datos compartidos en tiempo real vía Firebase.

## 1. Antes de desplegar: pega tu configuración de Firebase

Abre `index.html`, busca cerca de la línea 7 esto:

```js
const FIREBASE_CONFIG = {
  apiKey: 'PENDIENTE',
  authDomain: 'PENDIENTE',
  projectId: 'PENDIENTE',
  storageBucket: 'PENDIENTE',
  messagingSenderId: 'PENDIENTE',
  appId: 'PENDIENTE',
};
```

Reemplaza los 6 valores por los de tu proyecto de Firebase (Configuración del
proyecto → Tus apps → objeto `firebaseConfig`). Guarda el archivo.

Recuerda tener listo en tu proyecto de Firebase:
- Firestore Database creado (modo producción).
- Reglas de Firestore (pestaña "Reglas"):

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /mi-club-aletas/{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```
- Authentication → Sign-in method → proveedor **Anónimo** habilitado.

## 2. Subir a GitHub

1. Crea un repositorio nuevo en github.com (puede ser privado).
2. Sube `index.html` a la raíz del repositorio (botón "Add file" → "Upload files", o con git).

## 3. Desplegar en Vercel

1. Entra a vercel.com e inicia sesión con tu cuenta de GitHub.
2. "Add New..." → "Project" → elige el repositorio que acabas de crear.
3. Vercel detecta que es un sitio estático — no necesitas tocar ninguna
   configuración de build. Clic en "Deploy".
4. En un minuto te da un link tipo `https://mi-club-aletas.vercel.app`.

## 4. Compartir con la mesa directiva

Envíales solo el link de Vercel. Lo abren en el navegador de su celular
("Agregar a pantalla de inicio" para que quede como app) y ya están
conectados a los mismos datos — no necesitan pegar ninguna configuración.

## Actualizaciones futuras

Cualquier cambio que subas a la rama principal del repositorio de GitHub
se despliega automáticamente en el mismo link de Vercel.
