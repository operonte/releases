# 🖥️ Guía de Instalación de Cursor IDE en BlackArch

## 🎯 Introducción
Cursor IDE es un editor de código basado en VS Code con capacidades avanzadas de IA integradas. Es una alternativa popular a Windsurf con características similares pero con su propio enfoque.

## 🔍 Requisitos Previos

### Sistema Operativo
- ✅ BlackArch Linux (basado en Arch)
- ✅ Acceso a terminal con permisos sudo
- ✅ Conexión a internet
- ✅ Cuenta de Cursor (para funcionalidades premium)

### Dependencias Comunes
```bash
# Actualizar sistema
sudo pacman -Syu

# Instalar dependencias esenciales
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
    libgconf-2-4
```

## 📦 Métodos de Instalación

### 🥇 Método 1: Descarga Directa (Recomendado)
**Ventajas**: Estable, independiente, fácil de actualizar

```bash
# 1. Crear directorio de trabajo
mkdir -p ~/Downloads/cursor
cd ~/Downloads/cursor

# 2. Descargar Cursor IDE (última versión)
wget https://download.todesktop.com/230313mzl4w4u92/linux/x64/Cursor-0.42.4-build-241040xq3a6wqz.AppImage

# 3. Hacer ejecutable
chmod +x Cursor-*.AppImage

# 4. Mover a directorio global
sudo mkdir -p /opt/appimages
sudo mv Cursor-*.AppImage /opt/appimages/cursor.AppImage

# 5. Crear enlace simbólico para acceso global
sudo ln -sf /opt/appimages/cursor.AppImage /usr/local/bin/cursor

# 6. Verificar instalación
cursor --version
```

### 🥈 Método 2: AppImage (Portátil)
**Ventajas**: Sin instalación, portable, aislado

```bash
# 1. Descargar AppImage
cd ~/Downloads
wget https://download.todesktop.com/230313mzl4w4u92/linux/x64/Cursor-0.42.4-build-241040xq3a6wqz.AppImage

# 2. Hacer ejecutable
chmod +x Cursor-*.AppImage

# 3. Ejecutar directamente
./Cursor-*.AppImage

# 4. Opcional: Mover a directorio de aplicaciones
sudo mkdir -p /opt/appimages
sudo mv Cursor-*.AppImage /opt/appimages/cursor.AppImage
sudo ln -sf /opt/appimages/cursor.AppImage /usr/local/bin/cursor
```

### 🥉 Método 3: AUR (Arch User Repository)
**Ventajas**: Integrado con pacman, actualizaciones automáticas

```bash
# Opción A: Con yay (helper de AUR)
if ! command -v yay &> /dev/null; then
    # Instalar yay si no existe
    sudo pacman -S --needed git base-devel
    git clone https://aur.archlinux.org/yay.git
    cd yay
    makepkg -si
    cd ..
fi

# Instalar Cursor desde AUR
yay -S cursor-bin

# Opción B: Con paru (alternativa a yay)
if ! command -v paru &> /dev/null; then
    # Instalar paru si no existe
    sudo pacman -S --needed git base-devel
    git clone https://aur.archlinux.org/paru.git
    cd paru
    makepkg -si
    cd ..
fi

# Instalar Cursor
paru -S cursor-bin

# Opción C: Instalación manual desde AUR
git clone https://aur.archlinux.org/cursor-bin.git
cd cursor-bin
makepkg -si
```

### 🔧 Método 4: Repositorio Oficial
**Ventajas**: Actualizaciones automáticas, versión estable

```bash
# 1. Añadir clave GPG
curl -fsSL https://download.todesktop.com/keys/linux/signature.gpg | sudo gpg --dearmor -o /usr/share/keyrings/cursor.gpg

# 2. Añadir repositorio
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/cursor.gpg] https://download.todesktop.com/230313mzl4w4u92/linux/ stable main" | sudo tee /etc/apt/sources.list.d/cursor.list

# 3. Actualizar lista de paquetes
sudo pacman -Syu

# 4. Instalar Cursor
sudo pacman -S cursor
```

## 🚀 Post-Instalación

### Verificación
```bash
# Verificar versión
cursor --version

# Verificar ayuda
cursor --help

# Listar comandos disponibles
cursor --list-commands
```

### Configuración Inicial
```bash
# Abrir Cursor
cursor

# O ejecutar con directorio específico
cursor /ruta/a/tu/proyecto

# Ejecutar con configuración específica
cursor --config ~/.config/cursor/
```

### Crear Acceso Directo (Desktop Entry)
```bash
# Crear archivo .desktop
sudo nano /usr/share/applications/cursor.desktop
```

**Contenido del archivo:**
```ini
[Desktop Entry]
Name=Cursor
Comment=AI-powered IDE
Exec=/usr/local/bin/cursor %U
Icon=/opt/appimages/cursor.png
Type=Application
StartupNotify=true
Categories=Development;IDE;
MimeType=text/plain;inode/directory;
Keywords=ide;code;editor;cursor;
```

## 🔑 Configuración de Cuenta y API

### 1. Crear Cuenta de Cursor
```bash
# Abrir Cursor y registrarse
cursor

# O registrarse en la web
# https://cursor.com/signup
```

### 2. Configurar API Keys
```bash
# Editar configuración
nano ~/.config/cursor/User/settings.json
```

**Configuración de API Keys:**
```json
{
    "cursor.ai.apiKey": "tu-api-key-aqui",
    "cursor.ai.model": "gpt-4",
    "cursor.ai.provider": "openai",
    "cursor.ai.temperature": 0.7,
    "cursor.ai.maxTokens": 2048,
    "telemetry.enableTelemetry": false,
    "extensions.autoUpdate": false,
    "files.autoSave": "afterDelay",
    "workbench.startupEditor": "none",
    "update.mode": "manual"
}
```

### 3. Configurar Modelos de IA
```bash
# Configurar diferentes modelos
{
    "cursor.ai.models": {
        "coding": "gpt-4",
        "chat": "gpt-3.5-turbo",
        "debug": "gpt-4",
        "refactor": "gpt-4"
    },
    "cursor.ai.providers": {
        "openai": {
            "apiKey": "tu-openai-key",
            "baseURL": "https://api.openai.com/v1"
        },
        "anthropic": {
            "apiKey": "tu-anthropic-key",
            "baseURL": "https://api.anthropic.com/v1"
        }
    }
}
```

## 🔧 Solución de Problemas

### Problemas Comunes

#### 1. Error de Dependencias
```bash
# Error: libgtk-3-0: cannot open shared object file
sudo pacman -S gtk3

# Error: libnotify: cannot open shared object file
sudo pacman -S libnotify

# Error: nss: cannot open shared object file
sudo pacman -S nss
```

#### 2. Error de Permisos
```bash
# Error: Permission denied
sudo chmod +x /opt/appimages/cursor.AppImage
sudo chmod -R 755 /opt/appimages/

# Error: Cannot write to log directory
sudo mkdir -p /var/log/cursor
sudo chown $USER:$USER /var/log/cursor
```

#### 3. Error de Librerías Faltantes
```bash
# Verificar dependencias faltantes
ldd /opt/appimages/cursor.AppImage | grep "not found"

# Instalar librerías faltantes comunes
sudo pacman -S --needed \
    libxss1 \
    libgconf-2-4 \
    libasound2 \
    libxtst6 \
    libnss3 \
    libxrandr2 \
    libxcomposite1 \
    libxcursor1 \
    libxdamage1 \
    libxi6 \
    libgbm1 \
    libgtk-3-0
```

#### 4. Error de API Key
```bash
# Verificar configuración de API
cat ~/.config/cursor/User/settings.json | grep apiKey

# Resetear configuración
rm ~/.config/cursor/User/settings.json
cursor --reset-config
```

#### 5. Problemas con Wayland
```bash
# Forzar X11 si hay problemas con Wayland
export GDK_BACKEND=x11
cursor

# O usar variables de entorno específicas
export ELECTRON_OZONE_PLATFORM_HINT=x11
cursor
```

### Depuración
```bash
# Verbose mode
cursor --verbose

# Debug mode
cursor --debug

# Ver logs del sistema
journalctl -f | grep cursor

# Verificar proceso
ps aux | grep cursor
```

## 🎯 Optimización y Configuración

### Configuración de Rendimiento
```bash
# Editar configuración
nano ~/.config/cursor/settings.json
```

**Configuración recomendada:**
```json
{
    "telemetry.enableTelemetry": false,
    "extensions.autoUpdate": false,
    "files.autoSave": "afterDelay",
    "workbench.startupEditor": "none",
    "update.mode": "manual",
    "security.workspace.trust.enabled": true,
    "cursor.ai.enableAutoComplete": true,
    "cursor.ai.enableChat": true,
    "cursor.ai.enableDebug": true,
    "workbench.rendererSettings": {
        "experimentalWebRenderer": true
    }
}
```

### Atajos de Teclado Útiles
```bash
# Abrir Cursor rápidamente
alias cs='cursor'

# Abrir en directorio actual
alias cs-here='cursor .'

# Abrir con configuración específica
alias cs-config='cursor --config ~/.config/cursor/'
```

Añadir a `~/.bashrc` o `~/.zshrc`:
```bash
# Cursor aliases
alias cs='cursor'
alias cs-here='cursor .'
alias cs-config='cursor --config ~/.config/cursor/'

# Cursor functions
cs-projeto() {
    cursor /home/$USER/projects/$1
}
```

## 🔄 Actualización

### Método 1: Descarga Manual
```bash
# Descargar nueva versión
cd ~/Downloads/cursor
wget https://download.todesktop.com/230313mzl4w4u92/linux/x64/Cursor-0.42.4-build-241040xq3a6wqz.AppImage

# Respaldar configuración
cp -r ~/.config/cursor ~/.config/cursor.backup

# Desinstalar versión anterior
sudo rm /opt/appimages/cursor.AppImage

# Instalar nueva versión
sudo mv Cursor-*.AppImage /opt/appimages/cursor.AppImage
sudo chmod +x /opt/appimages/cursor.AppImage
```

### Método 2: AUR
```bash
# Actualizar con yay
yay -Syu cursor-bin

# O con paru
paru -Syu cursor-bin
```

### Método 3: Repositorio
```bash
# Actualizar sistema
sudo pacman -Syu

# Actualizar Cursor específicamente
sudo pacman -S cursor
```

## 🗑️ Desinstalación

### Método 1: Instalación Manual
```bash
# Eliminar archivos
sudo rm /opt/appimages/cursor.AppImage
sudo rm /usr/local/bin/cursor
sudo rm /usr/share/applications/cursor.desktop

# Opcional: Eliminar configuración
rm -rf ~/.config/cursor
rm -rf ~/.local/share/cursor
```

### Método 2: AUR
```bash
# Con yay
yay -R cursor-bin

# Con paru
paru -R cursor-bin
```

### Método 3: Repositorio
```bash
# Eliminar paquete
sudo pacman -R cursor

# Eliminar repositorio
sudo rm /etc/apt/sources.list.d/cursor.list
```

## 📚 Recursos Útiles

### Enlaces Oficiales
- **Página Web**: https://cursor.com
- **GitHub**: https://github.com/getcursor/cursor
- **Documentación**: https://cursor.com/docs
- **Descargas**: https://cursor.com/download

### Comunidad
- **Discord**: https://discord.gg/cursor
- **Twitter**: https://twitter.com/getcursor
- **Issues**: https://github.com/getcursor/cursor/issues

### Archivos de Configuración
- **Configuración principal**: `~/.config/cursor/`
- **Logs**: `~/.config/cursor/logs/`
- **Extensions**: `~/.config/cursor/extensions/`
- **User settings**: `~/.config/cursor/User/settings.json`

## 🎯 Tips Adicionales

### Integración con Terminal
```bash
# Abrir archivo específico
cursor archivo.txt

# Abrir con línea específica
cursor --goto archivo.txt:10

# Abrir en modo diff
cursor --diff archivo1.txt archivo2.txt
```

### Configuración para BlackArch Específico
```bash
# Variables de entorno para BlackArch
export ELECTRON_IS_DEV=0
export ELECTRON_ENABLE_LOGGING=1
export ELECTRON_ENABLE_STACK_DUMPING=1

# Añadir a ~/.bashrc o ~/.zshrc
echo 'export ELECTRON_IS_DEV=0' >> ~/.bashrc
echo 'export ELECTRON_ENABLE_LOGGING=1' >> ~/.bashrc
echo 'export ELECTRON_ENABLE_STACK_DUMPING=1' >> ~/.bashrc
```

### Optimización para Hardware Limitado
```json
{
    "workbench.rendererSettings": {
        "experimentalWebRenderer": true
    },
    "extensions.ignoreRecommendations": true,
    "telemetry.enableTelemetry": false,
    "workbench.enableExperiments": false,
    "files.watcherExclude": {
        "**/.git/objects/**": true,
        "**/.git/subtree-cache/**": true,
        "**/node_modules/**": true
    },
    "cursor.ai.enableAutoComplete": false,
    "cursor.ai.enableChat": true
}
```

### Configuración de API Keys para Diferentes Servicios
```json
{
    "cursor.ai.openai": {
        "apiKey": "sk-...",
        "model": "gpt-4",
        "baseURL": "https://api.openai.com/v1"
    },
    "cursor.ai.anthropic": {
        "apiKey": "sk-ant-...",
        "model": "claude-3-opus-20240229",
        "baseURL": "https://api.anthropic.com/v1"
    },
    "cursor.ai.google": {
        "apiKey": "AIza...",
        "model": "gemini-pro",
        "baseURL": "https://generativelanguage.googleapis.com/v1beta"
    }
}
```

---

## 🎉 ¡Listo!

Con esta guía completa deberías poder instalar Cursor IDE en BlackArch sin problemas. Recuerda que el **Método 1 (descarga directa)** es el más recomendado por su estabilidad y simplicidad.

**¿Necesitas ayuda con algún paso específico o has encontrado algún error?** 🚀
