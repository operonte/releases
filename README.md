# 📦 Releases y Políticas de Privacidad

Repositorio centralizado para releases de aplicaciones y políticas de privacidad.

---

## 📁 Estructura del Repositorio

```
/
├── imcapp/
│   ├── releases/
│   │   ├── android/ (APK/AAB files)
│   │   └── ios/ (IPA files)
│   └── policies/ (Políticas de privacidad)
├── misionapp/
│   ├── releases/
│   │   ├── android/ (APK/AAB files)
│   │   └── ios/ (IPA files)
│   └── policies/ (Políticas de privacidad)
├── fast/
│   ├── releases/
│   │   ├── android/ (APK/AAB files)
│   │   └── ios/ (IPA files)
│   └── policies/ (Políticas de privacidad)
├── horasmedicas/
│   ├── releases/
│   │   ├── android/ (APK/AAB files)
│   │   └── ios/ (IPA files)
│   └── policies/ (Políticas de privacidad)
├── categoriaaldia/
│   ├── releases/ (Información sobre releases)
│   └── policies/ (Políticas de privacidad)
└── README.md (este archivo)
```

---

## 🚀 Proyectos Disponibles

### 📱 IMC App
**Descripción:** Calculadora de IMC - Aplicación Flutter para calcular y gestionar tu Índice de Masa Corporal

**Package:** `com.example.imcapp`

**Repositorio:** https://github.com/operonte/imcapp

**Releases:**
- **Android:** [Ver releases](./imcapp/releases/android/)
- **iOS:** [Ver releases](./imcapp/releases/ios/)

**Políticas:**
- **Política de Privacidad:** [Ver política](./imcapp/policies/)
- **URL pública (GitHub Pages):** `https://operonte.github.io/releases/imcapp/policies/privacy_policy.html`

---

### 📱 Misión App
**Descripción:** Aplicación Flutter para gestión de visitas y seguimiento de personas en trabajos misioneros

**Package:** `com.example.misionapp`

**Repositorio:** https://github.com/operonte/misionapp

**Releases:**
- **Android:** [Ver releases](./misionapp/releases/android/)
- **iOS:** [Ver releases](./misionapp/releases/ios/)

**Políticas:**
- **Política de Privacidad:** [Ver política](./misionapp/policies/privacy-policy.md)
- **URL pública (GitHub Pages):** `https://operonte.github.io/releases/misionapp/policies/privacy-policy.html`

---

### 📱 Fast
**Descripción:** Aplicación Flutter para enviar mensajes a WhatsApp de forma rápida con historial y mensajes predefinidos

**Package:** `com.example.fast`

**Repositorio:** https://github.com/operonte/fast

**Releases:**
- **Android:** [Ver releases](./fast/releases/android/)
- **iOS:** [Ver releases](./fast/releases/ios/)

**Políticas:**
- **Política de Privacidad:** [Ver política](./fast/policies/)
- **URL pública (GitHub Pages):** `https://operonte.github.io/releases/fast/policies/privacy_policy.html`

---

### 📱 Horas Médicas
**Descripción:** App con acceso directo a clínicas médicas en Rancagua para reservar horas

**Package:** `com.example.horasmedicas`

**Repositorio:** https://github.com/operonte/horasmedicas

**Releases:**
- **Android:** [Ver releases](./horasmedicas/releases/android/)
- **iOS:** [Ver releases](./horasmedicas/releases/ios/)

**Políticas:**
- **Política de Privacidad:** [Ver política](./horasmedicas/policies/)
- **URL pública (GitHub Pages):** `https://operonte.github.io/releases/horasmedicas/policies/privacy_policy.html`

---

### 📊 Categoria al Día
**Descripción:** Macro Excel para gestión de inventario Walmart Smart (no es aplicación móvil)

**Repositorio:** https://github.com/operonte/categoriaaldia

**Releases:**
- **Información:** [Ver información](./categoriaaldia/releases/)

**Políticas:**
- **Política de Privacidad:** [Ver política](./categoriaaldia/policies/)

---

## 📝 Cómo Usar Este Repositorio

### Para Agregar una Nueva Release:

1. **Crear release de la app:**
   ```bash
   # Android
   flutter build apk --release
   # o
   flutter build appbundle --release
   
   # iOS
   flutter build ipa
   ```

2. **Copiar archivo al repositorio:**
   ```bash
   # Android APK
   cp build/app/outputs/flutter-apk/app-release.apk misionapp/releases/android/app-release-v1.0.0.apk
   
   # Android AAB
   cp build/app/outputs/bundle/release/app-release.aab misionapp/releases/android/app-release-v1.0.0.aab
   
   # iOS IPA
   cp build/ios/ipa/*.ipa misionapp/releases/ios/misionapp-v1.0.0.ipa
   ```

3. **Hacer commit y push:**
   ```bash
   git add misionapp/releases/android/app-release-v1.0.0.apk
   git commit -m "Release: Misión App v1.0.0 (Android)"
   git push origin main
   ```

### Para Actualizar Política de Privacidad:

1. **Editar política:**
   ```bash
   nano misionapp/policies/privacy-policy.md
   ```

2. **Hacer commit:**
   ```bash
   git add misionapp/policies/privacy-policy.md
   git commit -m "Actualizar Política de Privacidad - Misión App"
   git push origin main
   ```

---

## 🔗 URLs Públicas para Políticas

### GitHub Pages (Recomendado):

1. **Habilitar GitHub Pages:**
   - Ir a Settings > Pages
   - Source: Deploy from a branch
   - Branch: `main` / `/ (root)`

2. **URL resultante:**
   ```
   https://operonte.github.io/releases/{proyecto}/policies/privacy_policy.html
   ```

   Ejemplos:
   - IMC App: `https://operonte.github.io/releases/imcapp/policies/privacy_policy.html`
   - Misión App: `https://operonte.github.io/releases/misionapp/policies/privacy-policy.html`
   - Fast: `https://operonte.github.io/releases/fast/policies/privacy_policy.html`
   - Horas Médicas: `https://operonte.github.io/releases/horasmedicas/policies/privacy_policy.html`

### GitHub Raw (Alternativa):

```
https://raw.githubusercontent.com/operonte/releases/main/{proyecto}/policies/privacy-policy.md
```

⚠️ **Nota:** GitHub Raw muestra Markdown como texto plano. Para mejor presentación, usa GitHub Pages.

---

## 📋 Checklist para Cada Release

- [ ] Compilar app en modo release
- [ ] Copiar APK/AAB/IPA a la carpeta correspondiente
- [ ] Actualizar README.md de la carpeta de releases
- [ ] Crear tag de Git (opcional): `git tag v1.0.0`
- [ ] Hacer commit y push
- [ ] Crear Release en GitHub (opcional, con notas de versión)

---

## 🔐 Seguridad

- ⚠️ **NO subir keystores** (`*.jks`, `key.properties`)
- ⚠️ **NO subir archivos sensibles** (credenciales, tokens, etc.)
- ✅ **Usar .gitignore** para ignorar archivos temporales
- ✅ **Firmar releases** antes de subirlas

---

## 📚 Recursos

- [Guía de Releases en GitHub](https://docs.github.com/en/repositories/releasing-projects-on-github)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [Flutter Build Documentation](https://docs.flutter.dev/deployment)

---

## 🆘 Soporte

Para consultas sobre releases o políticas, contactar al administrador del repositorio.

---

**Última actualización:** Enero 2025
