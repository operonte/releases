# 📱 Misión App - Releases Android

Releases de la aplicación **Misión App** para la plataforma Android.

**Package:** `com.example.misionapp`

---

## 📦 Última Release

**Versión:** v1.0.0  
**Fecha:** Enero 2025  
**Archivo:** `app-release.apk` o `app-release.aab`

---

## 📥 Descargar

### APK (Instalación Directa)
- **Archivo:** `app-release.apk`
- **Uso:** Para instalación directa en dispositivos Android
- **Requisito:** Habilitar "Fuentes desconocidas" en Android Settings

### AAB (Google Play Store)
- **Archivo:** `app-release.aab`
- **Uso:** Para publicación en Google Play Store
- **Formato:** Android App Bundle (formato recomendado por Google)

---

## 🔒 Verificación de Integridad

Antes de instalar, verifica el SHA-256 del APK:

```bash
# Linux/Mac
sha256sum app-release.apk

# Windows
certutil -hashfile app-release.apk SHA256
```

Compara el hash con el proporcionado en esta documentación.

---

## 📋 Historial de Versiones

### v1.0.0 (Enero 2025)
- ✅ Primera release pública
- ✅ Sistema de grupos implementado
- ✅ Gestión de miembros
- ✅ Autenticación con Google Sign-In
- ✅ Política de Privacidad disponible

**Cambios principales:**
- Implementación completa del sistema de grupos
- CRUD de personas con filtrado por grupo
- Interfaz de usuario mejorada
- Manejo de errores robusto

---

## 📲 Instalación

### Desde APK:

1. **Habilitar fuentes desconocidas:**
   - Android Settings > Security > Unknown Sources (activar)
   - O Android Settings > Apps > Special access > Install unknown apps

2. **Descargar APK:**
   - Click en el archivo `app-release.apk` o `app-release-vX.X.X.apk`
   - Descargar el archivo

3. **Instalar:**
   - Abrir el archivo descargado desde la carpeta Downloads
   - Seguir las instrucciones de instalación

### Desde Google Play Store:

La app estará disponible próximamente en Google Play Store.

---

## ⚠️ Notas Importantes

- Solo instala APKs desde fuentes confiables
- Verifica el SHA-256 antes de instalar
- Esta app requiere **Android 5.0 (API 21)** o superior
- Requiere **conexión a internet** para Firebase (autenticación y almacenamiento)
- Requiere **cuenta de Google** para iniciar sesión

---

## 📱 Requisitos del Sistema

- **Android:** 5.0 (Lollipop) o superior
- **RAM:** Mínimo 2GB recomendado
- **Almacenamiento:** ~50MB para la app
- **Permisos:**
  - Internet (requerido)
  - Cuenta de Google (requerido para login)

---

## 🔄 Actualizaciones

Las nuevas versiones se publicarán en esta carpeta con el formato:
- `app-release-vX.X.X.apk` para APKs
- `app-release-vX.X.X.aab` para AABs

---

**Desarrollador:** Cristian Bravo D.  
**Contacto:** (Pendiente)  
**Package:** `com.example.misionapp`
