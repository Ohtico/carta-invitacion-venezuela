# 🇻🇪 Generador de Carta de Invitación para Venezuela

Aplicación web para generar cartas de invitación oficiales para visitar la República Bolivariana de Venezuela.

## 🚀 Características

- ✅ Formulario completo con validación
- 📄 Generación de PDF profesional
- 👁️ Vista previa antes de generar
- 📊 Métricas con Firebase (opcional)
- 📱 Diseño responsive
- ⚡ Sin backend necesario

## 🔧 Configuración de Firebase (Opcional)

### 1. Crear proyecto en Firebase

1. Ve a [Firebase Console](https://console.firebase.google.com/)
2. Crea un nuevo proyecto
3. Habilita Firestore Database
4. Copia las credenciales de configuración

### 2. Configurar GitHub Secrets

En tu repositorio de GitHub, ve a **Settings > Secrets and variables > Actions** y agrega los siguientes secrets:

- `FIREBASE_API_KEY`
- `FIREBASE_AUTH_DOMAIN`
- `FIREBASE_PROJECT_ID`
- `FIREBASE_STORAGE_BUCKET`
- `FIREBASE_MESSAGING_SENDER_ID`
- `FIREBASE_APP_ID`

### 3. Reglas de Seguridad de Firestore

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Colección de estadísticas (solo escritura)
    match /stats/{document=**} {
      allow read: if false;
      allow write: if true;
    }

    // Colección de generaciones (solo escritura)
    match /generaciones/{document=**} {
      allow read: if false;
      allow write: if true;
    }
  }
}
```

## 📦 Deployment

### GitHub Pages (Automático)

1. Sube el código a GitHub
2. Configura los secrets de Firebase
3. GitHub Actions se encargará del deployment automático

### Local (Sin Firebase)

Simplemente abre `index.html` en tu navegador. La aplicación funcionará sin el sistema de métricas.

## 🛠️ Desarrollo Local con Firebase

1. Crea un archivo `firebase-config.js` (no se subirá a git):

```javascript
const firebaseConfig = {
  apiKey: "tu-api-key",
  authDomain: "tu-auth-domain",
  projectId: "tu-project-id",
  storageBucket: "tu-storage-bucket",
  messagingSenderId: "tu-messaging-sender-id",
  appId: "tu-app-id"
};
```

2. Modifica `index.html` para cargar este archivo en desarrollo

## 📄 Licencia

MIT License - Libre para uso personal y comercial

## 👨‍💻 Autor

Victor Gelvis
