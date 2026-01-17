# 🚀 Guía para Configurar el Repositorio en GitHub

**Objetivo:** Crear un repositorio en GitHub para releases de APK y políticas de privacidad.

**Package:** `com.example.misionapp`

---

## 📋 PASOS PARA CREAR EL REPOSITORIO

### Paso 1: Crear Repositorio en GitHub

1. **Ir a GitHub:**
   - Abre [github.com](https://github.com)
   - Inicia sesión

2. **Crear nuevo repositorio:**
   - Click en **"New"** o **"+"** > **"New repository"**

3. **Configurar repositorio:**
   - **Repository name:** `releases` o `app-releases` o `releases-policies`
   - **Description:** "Releases de APK y políticas de privacidad"
   - **Visibility:** 
     - ✅ **Public** (recomendado para URLs públicas de políticas)
     - O **Private** si prefieres controlar el acceso
   - **NO marcar** "Add a README file" (ya lo tenemos)
   - **NO agregar** .gitignore ni licencia (ya los tenemos)

4. **Crear repositorio:**
   - Click en **"Create repository"**

---

### Paso 2: Inicializar Repositorio Local

1. **Navegar a la carpeta del proyecto:**
   ```bash
   cd /home/corban/LAB/proyectos/releases-repo
   ```

2. **Inicializar Git (si no está inicializado):**
   ```bash
   git init
   ```

3. **Agregar archivos:**
   ```bash
   git add .
   ```

4. **Commit inicial:**
   ```bash
   git commit -m "Initial commit: Estructura de releases y políticas de privacidad"
   ```

5. **Agregar remote de GitHub:**
   ```bash
   git remote add origin https://github.com/TU-USUARIO/REPO-NAME.git
   ```
   ⚠️ **Reemplaza:** `TU-USUARIO` con tu usuario de GitHub y `REPO-NAME` con el nombre del repositorio

6. **Subir a GitHub:**
   ```bash
   git branch -M main
   git push -u origin main
   ```

---

### Paso 3: Configurar GitHub Pages (para URLs públicas)

1. **Ir a Settings del repositorio:**
   - En GitHub, ve a tu repositorio
   - Click en **"Settings"**

2. **Configurar Pages:**
   - En el menú lateral, click en **"Pages"**
   - **Source:** Seleccionar **"Deploy from a branch"**
   - **Branch:**
     - Seleccionar `main` o `master`
     - Folder: `/ (root)`
   - Click en **"Save"**

3. **Esperar a que se active:**
   - GitHub tomará unos minutos en configurar Pages
   - Verás un mensaje: "Your site is published at https://TU-USUARIO.github.io/REPO-NAME/"

4. **URL resultante para Política de Privacidad:**
   ```
   https://TU-USUARIO.github.io/REPO-NAME/misionapp/policies/privacy-policy.html
   ```

---

### Paso 4: Verificar Estructura

La estructura final en GitHub debe verse así:

```
releases-repo-name/
├── .gitignore
├── README.md
├── SETUP_GITHUB.md (este archivo)
├── misionapp/
│   ├── releases/
│   │   ├── android/
│   │   │   ├── README.md
│   │   │   └── (APK/AAB files aquí cuando los subas)
│   │   └── ios/
│   │       └── README.md
│   └── policies/
│       ├── privacy-policy.md
│       └── README.md
```

---

### Paso 5: Verificar URLs Públicas

1. **Verificar GitHub Pages:**
   - Esperar 5-10 minutos después de activar Pages
   - Visitar: `https://TU-USUARIO.github.io/REPO-NAME/`
   - Deberías ver el README.md renderizado

2. **Verificar política de privacidad:**
   - Visitar: `https://TU-USUARIO.github.io/REPO-NAME/misionapp/policies/privacy-policy.html`
   - O: `https://raw.githubusercontent.com/TU-USUARIO/REPO-NAME/main/misionapp/policies/privacy-policy.md`

---

### Paso 6: Actualizar URL en la App

1. **Editar `profile_screen.dart` en el proyecto principal:**
   ```bash
   nano /home/corban/LAB/proyectos/misionapp/lib/screens/profile_screen.dart
   ```

2. **Cambiar la URL (línea ~14):**
   ```dart
   const privacyPolicyUrl = 'https://TU-USUARIO.github.io/REPO-NAME/misionapp/policies/privacy-policy.html';
   ```

3. **Verificar que funciona:**
   - Compilar y probar la app
   - Ir a Perfil > Política de Privacidad
   - Debe abrirse en el navegador

---

## 🔄 Workflow para Agregar Nuevas Releases

### Agregar Release de Android:

1. **Compilar APK/AAB:**
   ```bash
   cd /home/corban/LAB/proyectos/misionapp
   flutter build apk --release
   # o
   flutter build appbundle --release
   ```

2. **Copiar al repositorio:**
   ```bash
   cp build/app/outputs/flutter-apk/app-release.apk \
      /home/corban/LAB/proyectos/releases-repo/misionapp/releases/android/app-release-v1.0.0.apk
   ```

3. **Actualizar README (opcional):**
   - Editar `misionapp/releases/android/README.md`
   - Actualizar versión y fecha

4. **Commit y push:**
   ```bash
   cd /home/corban/LAB/proyectos/releases-repo
   git add misionapp/releases/android/app-release-v1.0.0.apk
   git commit -m "Release: Misión App v1.0.0 (Android APK)"
   git push origin main
   ```

5. **Opcional - Crear Release en GitHub:**
   - Ir a tu repositorio en GitHub
   - Click en **"Releases"** > **"Create a new release"**
   - Tag: `v1.0.0`
   - Title: "Misión App v1.0.0"
   - Description: Notas de la versión
   - Attach files: Subir el APK/AAB
   - Click en **"Publish release"**

---

## ✅ Checklist Final

- [ ] Repositorio creado en GitHub
- [ ] Archivos subidos a GitHub (estructura completa)
- [ ] GitHub Pages activado y funcionando
- [ ] Política de Privacidad personalizada y publicada
- [ ] URLs verificadas y accesibles públicamente
- [ ] URL actualizada en `profile_screen.dart`
- [ ] README.md actualizado con información correcta

---

## 🆘 Solución de Problemas

### Error: "Repository not found"
- Verifica que el URL del remote sea correcto
- Verifica que tengas permisos para el repositorio

### GitHub Pages no funciona:
- Verifica que la rama sea `main` o `master`
- Espera 10-15 minutos después de activar
- Verifica que hay al menos un archivo Markdown en la raíz

### URL de política no se muestra correctamente:
- GitHub Pages renderiza Markdown automáticamente si el archivo es `.md`
- Para mejor formato, GitHub convierte `.md` a `.html` automáticamente
- Verifica que el archivo esté en la ruta correcta: `misionapp/policies/privacy-policy.md`

---

## 📝 Notas Importantes

- **Package Name:** `com.example.misionapp`
- **URLs deben ser públicas** para que funcionen en Google Play Console
- **No subir keystores** o archivos sensibles (están en .gitignore)
- **Cada release debe tener nombre único** (ej: `app-release-v1.0.0.apk`)

---

**¡Listo! Ahora tienes un repositorio centralizado para releases y políticas de privacidad.**
