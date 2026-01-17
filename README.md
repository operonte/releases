# 📦 Releases y Políticas de Privacidad

Repositorio centralizado para releases de aplicaciones y políticas de privacidad.

---

## 📁 Estructura del Repositorio

```
/
├── misionapp/
│   ├── releases/
│   │   ├── android/
│   │   │   ├── README.md
│   │   │   └── (APK/AAB files aquí)
│   │   └── ios/
│   │       ├── README.md
│   │       └── (IPA files aquí)
│   └── policies/
│       ├── privacy-policy.md
│       └── README.md
├── README.md (este archivo)
└── .gitignore
```

---

## 🚀 Proyectos Disponibles

### 📱 Misión App
**Descripción:** Aplicación para seguimiento de miembros de iglesias

**Package:** `com.example.misionapp`

**Releases:**
- **Android:** [Ver releases](./misionapp/releases/android/)
- **iOS:** [Ver releases](./misionapp/releases/ios/) (próximamente)

**Políticas:**
- **Política de Privacidad:** [Ver política](./misionapp/policies/privacy-policy.md)
- **URL pública (GitHub Pages):** `https://TU-USUARIO.github.io/releases/misionapp/policies/privacy-policy.html`

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
   https://TU-USUARIO.github.io/releases/misionapp/policies/privacy-policy.html
   ```

### GitHub Raw (Alternativa):

```
https://raw.githubusercontent.com/TU-USUARIO/releases/main/misionapp/policies/privacy-policy.md
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
