# 📄 Políticas - Misión App

Documentos legales y políticas de privacidad para **Misión App**.

**Package:** `com.example.misionapp`

---

## 📋 Documentos Disponibles

### [Política de Privacidad](./privacy-policy.md)

**Última actualización:** Enero 2025  
**Versión:** 1.0

**Descripción:**  
Este documento describe cómo recolectamos, usamos, compartimos y protegemos su información personal cuando utiliza Misión App.

**Contenido:**
- Información recolectada
- Cómo se usan los datos
- Compartir con terceros
- Seguridad de datos
- Derechos del usuario
- Contacto

---

## 🔗 URLs Públicas

### GitHub Pages (Recomendado para Stores):

```
https://TU-USUARIO.github.io/releases/misionapp/policies/privacy-policy.html
```

### GitHub Raw (Alternativa):

```
https://raw.githubusercontent.com/TU-USUARIO/releases/main/misionapp/policies/privacy-policy.md
```

⚠️ **Nota:** 
- **GitHub Pages** muestra Markdown renderizado como HTML (mejor para stores)
- **GitHub Raw** muestra Markdown como texto plano

---

## 📝 Cómo Usar Estas URLs

### Para Google Play Console:

1. Ir a **Google Play Console** > **App content** > **Privacy Policy**
2. Agregar URL: 
   ```
   https://TU-USUARIO.github.io/releases/misionapp/policies/privacy-policy.html
   ```
3. Verificar que la URL es accesible públicamente
4. Guardar cambios

### Para App Store Connect:

1. Ir a **App Store Connect** > **App Privacy**
2. Agregar URL de Política de Privacidad
3. Usar la URL de GitHub Pages

### En la App:

La app ya está configurada para abrir la Política de Privacidad desde la pantalla de Perfil.

**Archivo:** `lib/screens/profile_screen.dart`

**⚠️ Acción requerida:**
Actualizar la URL en `profile_screen.dart` después de publicar en GitHub Pages:

```dart
const privacyPolicyUrl = 'https://TU-USUARIO.github.io/releases/misionapp/policies/privacy-policy.html';
```

---

## 📝 Actualizar Políticas

Para actualizar una política:

1. **Editar el archivo `.md` correspondiente:**
   ```bash
   nano privacy-policy.md
   ```

2. **Revisar cambios:**
   - Verificar que la información sigue siendo precisa
   - Actualizar fecha de "Última actualización" si corresponde

3. **Commit y push:**
   ```bash
   git add privacy-policy.md
   git commit -m "Actualizar Política de Privacidad - Misión App v1.1"
   git push origin main
   ```

4. **Si usas GitHub Pages:**
   - Los cambios se publicarán automáticamente en 1-5 minutos
   - Verificar que la URL funciona después de publicar

---

## ✅ Checklist de Publicación

Antes de publicar la app en las stores:

- [ ] Política de Privacidad personalizada con información real
  - [ ] Reemplazar `[TU EMAIL]`, `[TU NOMBRE]`, etc.
- [ ] Política de Privacidad publicada en GitHub Pages
- [ ] URL de GitHub Pages verificada y accesible públicamente
- [ ] URL agregada en Google Play Console > App content > Privacy Policy
- [ ] URL agregada en App Store Connect > App Privacy (si aplica)
- [ ] URL actualizada en `profile_screen.dart` de la app
- [ ] Verificar que el link funciona desde la app

---

## 📚 Información Adicional

- **Package Name:** `com.example.misionapp`
- **Última actualización:** Enero 2025
- **Versión de política:** 1.0

---

**Para consultas sobre la política de privacidad, contactar al administrador del repositorio.**
