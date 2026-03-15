# 🤖 Herramientas de IA para Desarrollo en BlackArch

## 📋 Introducción
Esta sección contiene guías completas para instalar y configurar diversas herramientas de Inteligencia Artificial asistida para desarrollo de software en BlackArch Linux.

## 🛠️ Herramientas Disponibles

### 1. **Windsurf** - IDE con IA Integrada
- **Descripción**: IDE moderno basado en VS Code con capacidades de IA
- **Características**: Autocompletado, generación de código, debugging asistido
- **Guía**: [windsurf_blackarch.md](./windsurf_blackarch.md)
- **Requisitos**: Cuenta de Windsurf, conexión a internet

### 2. **Cursor IDE** - Alternativa con IA Avanzada
- **Descripción**: Editor de código basado en VS Code con IA integrada
- **Características**: Chat con IA, generación de código, refactorización automática
- **Guía**: [cursor_ide.md](./cursor_ide.md)
- **Requisitos**: Cuenta de Cursor, API keys opcionales

### 3. **Grok AI** - Modelo de xAI
- **Descripción**: Modelo de lenguaje de Elon Musk/xAI para desarrollo
- **Características**: CLI, scripts personalizados, integración con IDEs
- **Guía**: [grok_ai_setup.md](./grok_ai_setup.md)
- **Requisitos**: API Key de xAI, Python 3.8+

## 🚀 Instalación Rápida

### Windsurf (Recomendado)
```bash
# Descargar e instalar
wget https://windsurf-cdn.s3.us-east-1.amazonaws.com/Windsurf-linux-x64.tar.gz
tar -xzf Windsurf-linux-x64.tar.gz
sudo mv Windsurf /opt/
sudo ln -sf /opt/Windsurf/windsurf /usr/local/bin/windsurf
windsurf
```

### Cursor IDE
```bash
# Descargar AppImage
wget https://download.todesktop.com/230313mzl4w4u92/linux/x64/Cursor-0.42.4-build-241040xq3a6wqz.AppImage
chmod +x Cursor-*.AppImage
sudo mv Cursor-*.AppImage /opt/appimages/cursor.AppImage
sudo ln -sf /opt/appimages/cursor.AppImage /usr/local/bin/cursor
cursor
```

### Grok AI
```bash
# Instalar SDK
pip install xai-sdk
export GROK_API_KEY="tu-api-key-aqui"
python3 -c "import xai; print('Grok listo')"
```

## 🔧 Configuración Común

### Variables de Entorno
```bash
# Añadir a ~/.bashrc
export WINDSURF_CONFIG="$HOME/.config/windsurf"
export CURSOR_CONFIG="$HOME/.config/cursor"
export GROK_API_KEY="tu-api-key-aqui"

# Aliases útiles
alias ws='windsurf'
alias cs='cursor'
alias grok-chat='python3 ~/grok-ai/chat.py'
```

### Dependencias del Sistema
```bash
# Instalar dependencias comunes para todas las herramientas
sudo pacman -S --needed \
    gtk3 \
    libnotify \
    nss \
    xdg-utils \
    libxtst \
    libxss \
    libasound2 \
    libgbm \
    libdrm \
    libxcomposite \
    libxdamage \
    libxrandr \
    libxkbfile \
    libxfixes \
    libgtk-3-0 \
    libgconf-2-4 \
    curl \
    wget \
    jq \
    python3 \
    python-pip \
    git
```

## 📊 Comparación de Herramientas

| Característica | Windsurf | Cursor IDE | Grok AI |
|---------------|----------|------------|----------|
| **Tipo** | IDE completo | IDE completo | CLI + SDK |
| **Base** | VS Code | VS Code | Python |
| **IA Integrada** | ✅ Sí | ✅ Sí | 🔧 Manual |
| **Autocompletado** | ✅ Sí | ✅ Sí | 🔧 Scripts |
| **Chat con IA** | ✅ Sí | ✅ Sí | ✅ Sí |
| **Debug Asistido** | ✅ Sí | ✅ Sí | ✅ Sí |
| **Costo** | Freemium | Freemium | API Key |
| **Curva de Aprendizaje** | Media | Media | Alta |
| **Personalización** | Alta | Alta | Máxima |

## 🎯 Casos de Uso Recomendados

### Para Principiantes
- **Windsurf**: Más fácil de usar, buena documentación
- **Cursor IDE**: Interfaz familiar, características básicas sólidas

### Para Desarrolladores Intermedios
- **Windsurf**: Buen balance de características y rendimiento
- **Cursor IDE**: Más opciones de personalización

### Para Usuarios Avanzados
- **Cursor IDE**: Máxima personalización y control
- **Grok AI**: Integración personalizada, scripts propios

### Para Uso Específico
- **Windsurf**: Proyectos web y generales
- **Cursor IDE**: Desarrollo de software profesional
- **Grok AI**: Automatización y scripts personalizados

## 🔑 API Keys y Cuentas

### Obtener Cuentas
```bash
# Windsurf
# https://windsurf.ai/signup

# Cursor IDE
# https://cursor.com/signup

# Grok AI (xAI)
# https://console.x.ai/
```

### Configurar API Keys
```bash
# Windsurf
cat > ~/.config/windsurf/User/settings.json << 'EOF'
{
    "windsurf.apiKey": "tu-api-key-windsurf"
}
EOF

# Cursor IDE
cat > ~/.config/cursor/User/settings.json << 'EOF'
{
    "cursor.apiKey": "tu-api-key-cursor"
}
EOF

# Grok AI
export GROK_API_KEY="tu-api-key-grok"
```

## 🛠️ Scripts Útiles

### Script de Verificación
```bash
# Crear script para verificar todas las instalaciones
cat > ~/check_ai_tools.sh << 'EOF'
#!/bin/bash

echo "🔍 Verificando herramientas de IA..."

# Verificar Windsurf
if command -v windsurf &> /dev/null; then
    echo "✅ Windsurf instalado"
    windsurf --version
else
    echo "❌ Windsurf no encontrado"
fi

# Verificar Cursor
if command -v cursor &> /dev/null; then
    echo "✅ Cursor IDE instalado"
    cursor --version
else
    echo "❌ Cursor IDE no encontrado"
fi

# Verificar Grok AI
if python3 -c "import xai" 2>/dev/null; then
    echo "✅ Grok AI SDK instalado"
else
    echo "❌ Grok AI SDK no encontrado"
fi

# Verificar API Keys
if [ -n "$GROK_API_KEY" ]; then
    echo "✅ GROK_API_KEY configurada"
else
    echo "❌ GROK_API_KEY no configurada"
fi

echo "🏁 Verificación completada"
EOF

chmod +x ~/check_ai_tools.sh
~/check_ai_tools.sh
```

### Script de Limpieza
```bash
# Script para limpiar configuraciones
cat > ~/cleanup_ai_tools.sh << 'EOF'
#!/bin/bash

echo "🧹 Limpiando herramientas de IA..."

# Limpiar Windsurf
rm -rf ~/.config/windsurf
rm -rf ~/.local/share/windsurf

# Limpiar Cursor
rm -rf ~/.config/cursor
rm -rf ~/.local/share/cursor

# Limpiar Grok AI
rm -rf ~/grok-ai

echo "✅ Limpieza completada"
EOF

chmod +x ~/cleanup_ai_tools.sh
```

## 🔧 Solución de Problemas Comunes

### Problemas de Dependencias
```bash
# Error: libgtk-3-0: cannot open shared object file
sudo pacman -S gtk3

# Error: libnotify: cannot open shared object file
sudo pacman -S libnotify

# Error: nss: cannot open shared object file
sudo pacman -S nss
```

### Problemas de Permisos
```bash
# Error: Permission denied
sudo chmod +x /opt/appimages/*.AppImage
sudo chmod -R 755 /opt/

# Error: Cannot write to log directory
sudo mkdir -p /var/log/{windsurf,cursor,grok}
sudo chown $USER:$USER /var/log/{windsurf,cursor,grok}
```

### Problemas de Conexión
```bash
# Verificar conexión
ping api.x.ai
ping windsurf.ai
ping cursor.com

# Usar proxy si es necesario
export https_proxy=http://proxy.ejemplo.com:8080
```

## 📚 Recursos Adicionales

### Documentación Oficial
- **Windsurf**: https://windsurf.ai/docs
- **Cursor IDE**: https://cursor.com/docs
- **Grok AI**: https://docs.x.ai/

### Comunidades
- **Windsurf**: https://discord.gg/windsurf
- **Cursor IDE**: https://discord.gg/cursor
- **Grok AI**: https://discord.gg/xai

### Tutoriales y Guías
- **VS Code con IA**: https://code.visualstudio.com/docs/ai
- **Python con IA**: https://docs.python.org/3/
- **BlackArch**: https://blackarch.org/

## 🎯 Recomendaciones Finales

### Para Empezar
1. **Instala Windsurf** primero (es el más fácil)
2. **Configura tu cuenta** y prueba las funciones básicas
3. **Experimenta con Cursor IDE** si necesitas más opciones
4. **Añade Grok AI** para automatización avanzada

### Para Producción
1. **Usa Cursor IDE** para proyectos serios
2. **Configura API keys** para todas las herramientas
3. **Crea scripts personalizados** con Grok AI
4. **Mantén todo actualizado** regularmente

### Para Aprendizaje
1. **Prueba todas las herramientas** para comparar
2. **Experimenta con diferentes modelos** de IA
3. **Crea tus propios scripts** y flujos de trabajo
4. **Únete a las comunidades** para aprender de otros

---

## 🎉 ¡Listo!

Con estas guías tienes todo lo necesario para instalar y configurar las mejores herramientas de IA para desarrollo en BlackArch Linux.

**¿Necesitas ayuda con alguna herramienta específica?** 🚀
