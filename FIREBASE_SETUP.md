# 🔥 Configuración de Firebase para Métricas

## 📋 Paso 1: Crear Proyecto en Firebase

1. Ve a [Firebase Console](https://console.firebase.google.com/)
2. Clic en "Agregar proyecto"
3. Nombre del proyecto: `carta-invitacion-venezuela` (o el que prefieras)
4. Desactiva Google Analytics (opcional)
5. Clic en "Crear proyecto"

## 📊 Paso 2: Configurar Firestore Database

1. En el menú lateral, ve a **Firestore Database**
2. Clic en "Crear base de datos"
3. Selecciona **Modo de producción**
4. Elige una ubicación (recomendado: `us-central1`)
5. Clic en "Habilitar"

## 🔐 Paso 3: Configurar Reglas de Seguridad

En la pestaña **Reglas** de Firestore, pega estas reglas:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Estadísticas globales (solo escritura)
    match /stats/{document=**} {
      allow read: if false;
      allow write: if true;
    }

    // Generaciones individuales (solo escritura)
    match /generaciones/{document=**} {
      allow read: if false;
      allow write: if true;
    }
  }
}
```

Clic en **Publicar**

## 🔑 Paso 4: Obtener Credenciales

1. Ve a **Configuración del proyecto** (ícono de engranaje)
2. Scroll down hasta "Tus apps"
3. Clic en el ícono web `</>`
4. Registra tu app con un nombre
5. **Copia las credenciales** que aparecen:

```javascript
const firebaseConfig = {
  apiKey: "AIza...",
  authDomain: "tu-proyecto.firebaseapp.com",
  projectId: "tu-proyecto",
  storageBucket: "tu-proyecto.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123..."
};
```

## 🔒 Paso 5: Configurar GitHub Secrets

1. Ve a tu repositorio en GitHub
2. **Settings** > **Secrets and variables** > **Actions**
3. Clic en **New repository secret**
4. Agrega estos 6 secrets (uno por uno):

| Secret Name | Valor |
|-------------|-------|
| `FIREBASE_API_KEY` | El valor de `apiKey` |
| `FIREBASE_AUTH_DOMAIN` | El valor de `authDomain` |
| `FIREBASE_PROJECT_ID` | El valor de `projectId` |
| `FIREBASE_STORAGE_BUCKET` | El valor de `storageBucket` |
| `FIREBASE_MESSAGING_SENDER_ID` | El valor de `messagingSenderId` |
| `FIREBASE_APP_ID` | El valor de `appId` |

## 🚀 Paso 6: Deploy

1. Sube tu código a GitHub:
```bash
git add .
git commit -m "Add Firebase metrics"
git push origin main
```

2. Ve a **Settings** > **Pages** en tu repo
3. Source: **GitHub Actions**
4. Espera a que termine el workflow en la pestaña **Actions**

## ✅ Verificación

1. Abre tu sitio en GitHub Pages
2. Abre la consola del navegador (F12)
3. Deberías ver: `✅ Firebase conectado - Métricas habilitadas`
4. Genera un PDF
5. Ve a Firebase Console > Firestore Database
6. Deberías ver las colecciones `stats` y `generaciones` con datos

## 📈 Ver Métricas

Para ver las estadísticas, puedes crear queries en Firebase Console:

### Total de generaciones:
```
Colección: stats
Documento: global
Campo: total
```

### Últimas generaciones:
```
Colección: generaciones
Ordenar por: timestamp (descendente)
Límite: 10
```

## 🛠️ Desarrollo Local (Opcional)

Si quieres probar Firebase localmente:

1. Crea un archivo `firebase-config-local.js`:
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

2. Reemplaza los placeholders en `index.html` temporalmente
3. **NUNCA** hagas commit de este archivo

## ⚠️ Importante

- Las credenciales de Firebase NO están expuestas en tu código fuente
- GitHub Actions las inyecta durante el deployment
- Solo funcionarán las métricas en GitHub Pages, no en local
- Si abres `index.html` localmente, verás: `ℹ️ Firebase no configurado`
