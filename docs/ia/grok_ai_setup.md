# 🤖 Guía de Configuración de Grok AI en BlackArch

## 🎯 Introducción
Grok AI es el modelo de lenguaje de xAI (empresa de Elon Musk) que puede ser integrado en varios IDEs y herramientas de desarrollo. Esta guía te ayudará a configurar Grok AI en BlackArch Linux.

## 🔍 Requisitos Previos

### Sistema Operativo
- ✅ BlackArch Linux (basado en Arch)
- ✅ Acceso a terminal con permisos sudo
- ✅ Conexión a internet
- ✅ Cuenta de xAI con acceso a Grok

### Dependencias Comunes
```bash
# Actualizar sistema
sudo pacman -Syu

# Instalar dependencias esenciales
sudo pacman -S --needed \
    curl \
    wget \
    jq \
    python3 \
    python-pip \
    git \
    nano \
    htop
```

## 🔑 Obtener API Key de Grok AI

### 1. Crear Cuenta en xAI
```bash
# Abrir navegador y registrarse
# https://console.x.ai/

# O usar curl para verificar disponibilidad
curl -X GET "https://api.x.ai/v1/models" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

### 2. Generar API Key
```bash
# 1. Iniciar sesión en https://console.x.ai/
# 2. Ir a "API Keys"
# 3. Crear nueva API Key
# 4. Copiar la clave generada

# Ejemplo de API Key (reemplazar con la tuya)
export GROK_API_KEY="xai-..."
```

### 3. Verificar API Key
```bash
# Verificar que la API Key funciona
curl -X GET "https://api.x.ai/v1/models" \
  -H "Authorization: Bearer $GROK_API_KEY" \
  -H "Content-Type: application/json"
```

## 📦 Instalación de Herramientas

### Método 1: CLI de Grok AI
```bash
# 1. Instalar CLI de xAI
pip install xai-sdk

# 2. Configurar variables de entorno
echo 'export GROK_API_KEY="tu-api-key-aqui"' >> ~/.bashrc
source ~/.bashrc

# 3. Verificar instalación
python3 -c "import xai; print('Grok SDK instalado correctamente')"
```

### Método 2: Cliente Python
```bash
# 1. Crear directorio de trabajo
mkdir -p ~/grok-ai
cd ~/grok-ai

# 2. Crear entorno virtual
python3 -m venv venv
source venv/bin/activate

# 3. Instalar dependencias
pip install openai xai-sdk requests

# 4. Crear script de prueba
cat > test_grok.py << 'EOF'
import os
from xai import Grok

# Configurar API Key
api_key = os.getenv('GROK_API_KEY')
if not api_key:
    api_key = "tu-api-key-aqui"

# Inicializar cliente
client = Grok(api_key=api_key)

# Probar conexión
try:
    response = client.chat.completions.create(
        model="grok-beta",
        messages=[
            {"role": "user", "content": "Hola, ¿cómo estás?"}
        ]
    )
    print("✅ Conexión exitosa con Grok AI")
    print(f"Respuesta: {response.choices[0].message.content}")
except Exception as e:
    print(f"❌ Error: {e}")
EOF

# 5. Ejecutar prueba
python3 test_grok.py
```

### Método 3: Integración con VS Code/Cursor
```bash
# 1. Instalar extensión de Grok AI
# Buscar "Grok AI" en el marketplace de VS Code/Cursor

# 2. Configurar settings.json
cat > ~/.config/cursor/User/settings.json << 'EOF'
{
    "grok.apiKey": "tu-api-key-aqui",
    "grok.model": "grok-beta",
    "grok.temperature": 0.7,
    "grok.maxTokens": 2048,
    "grok.enableAutoComplete": true,
    "grok.enableChat": true
}
EOF

# 3. Reiniciar el IDE
```

## 🛠️ Scripts y Herramientas Útiles

### Script de Chat Interactivo
```bash
# Crear script de chat
cat > ~/grok-ai/chat.py << 'EOF'
#!/usr/bin/env python3
import os
import sys
from xai import Grok

def main():
    api_key = os.getenv('GROK_API_KEY')
    if not api_key:
        print("❌ Error: GROK_API_KEY no está configurada")
        sys.exit(1)
    
    client = Grok(api_key=api_key)
    
    print("🤖 Grok AI Chat - Escribe 'salir' para terminar")
    print("=" * 50)
    
    while True:
        user_input = input("\nTú: ")
        if user_input.lower() in ['salir', 'exit', 'quit']:
            print("👋 ¡Hasta luego!")
            break
        
        try:
            response = client.chat.completions.create(
                model="grok-beta",
                messages=[
                    {"role": "user", "content": user_input}
                ],
                temperature=0.7,
                max_tokens=1024
            )
            
            print(f"\nGrok: {response.choices[0].message.content}")
            
        except Exception as e:
            print(f"❌ Error: {e}")

if __name__ == "__main__":
    main()
EOF

# Hacer ejecutable
chmod +x ~/grok-ai/chat.py
```

### Script de Generación de Código
```bash
# Crear script de generación de código
cat > ~/grok-ai/codegen.py << 'EOF'
#!/usr/bin/env python3
import os
import sys
import argparse
from xai import Grok

def generate_code(prompt, language="python"):
    api_key = os.getenv('GROK_API_KEY')
    if not api_key:
        print("❌ Error: GROK_API_KEY no está configurada")
        return None
    
    client = Grok(api_key=api_key)
    
    enhanced_prompt = f"""
Genera código {language} para la siguiente tarea:
{prompt}

Requisitos:
- Código limpio y bien comentado
- Manejo de errores básico
- Seguir buenas prácticas
- Sin explicaciones adicionales, solo código
"""
    
    try:
        response = client.chat.completions.create(
            model="grok-beta",
            messages=[
                {"role": "user", "content": enhanced_prompt}
            ],
            temperature=0.3,
            max_tokens=2048
        )
        
        return response.choices[0].message.content
    
    except Exception as e:
        print(f"❌ Error: {e}")
        return None

def main():
    parser = argparse.ArgumentParser(description='Generador de código con Grok AI')
    parser.add_argument('prompt', help='Descripción del código a generar')
    parser.add_argument('--lang', default='python', help='Lenguaje de programación')
    parser.add_argument('--output', help='Archivo de salida')
    
    args = parser.parse_args()
    
    print(f"🤖 Generando código {args.lang}...")
    code = generate_code(args.prompt, args.lang)
    
    if code:
        if args.output:
            with open(args.output, 'w') as f:
                f.write(code)
            print(f"✅ Código guardado en {args.output}")
        else:
            print("\n📝 Código generado:")
            print("=" * 50)
            print(code)

if __name__ == "__main__":
    main()
EOF

# Hacer ejecutable
chmod +x ~/grok-ai/codegen.py
```

### Script de Debugging
```bash
# Crear script de debugging
cat > ~/grok-ai/debug.py << 'EOF'
#!/usr/bin/env python3
import os
import sys
import argparse
from xai import Grok

def debug_code(code, error_message=None):
    api_key = os.getenv('GROK_API_KEY')
    if not api_key:
        print("❌ Error: GROK_API_KEY no está configurada")
        return None
    
    client = Grok(api_key=api_key)
    
    prompt = f"""
Analiza y depura el siguiente código:
{code}

{'Error reportado: ' + error_message if error_message else ''}

Proporciona:
1. Identificación del problema
2. Explicación clara del error
3. Código corregido
4. Prevención de futuros errores
"""
    
    try:
        response = client.chat.completions.create(
            model="grok-beta",
            messages=[
                {"role": "user", "content": prompt}
            ],
            temperature=0.2,
            max_tokens=2048
        )
        
        return response.choices[0].message.content
    
    except Exception as e:
        print(f"❌ Error: {e}")
        return None

def main():
    parser = argparse.ArgumentParser(description='Debugger con Grok AI')
    parser.add_argument('--file', help='Archivo a depurar')
    parser.add_argument('--code', help='Código a depurar')
    parser.add_argument('--error', help='Mensaje de error')
    
    args = parser.parse_args()
    
    code = ""
    if args.file:
        try:
            with open(args.file, 'r') as f:
                code = f.read()
        except Exception as e:
            print(f"❌ Error al leer archivo: {e}")
            return
    elif args.code:
        code = args.code
    else:
        print("❌ Proporciona --file o --code")
        return
    
    print("🔍 Analizando código...")
    result = debug_code(code, args.error)
    
    if result:
        print("\n📋 Análisis de debugging:")
        print("=" * 50)
        print(result)

if __name__ == "__main__":
    main()
EOF

# Hacer ejecutable
chmod +x ~/grok-ai/debug.py
```

## 🔧 Configuración de Entorno

### Variables de Entorno
```bash
# Añadir a ~/.bashrc o ~/.zshrc
cat >> ~/.bashrc << 'EOF'

# Grok AI Configuration
export GROK_API_KEY="tu-api-key-aqui"
export GROK_MODEL="grok-beta"
export GROK_TEMPERATURE="0.7"
export GROK_MAX_TOKENS="2048"

# Grok AI Aliases
alias grok-chat="python3 ~/grok-ai/chat.py"
alias grok-code="python3 ~/grok-ai/codegen.py"
alias grok-debug="python3 ~/grok-ai/debug.py"
EOF

# Recargar configuración
source ~/.bashrc
```

### Configuración de IDEs

#### Cursor IDE
```bash
# Configurar settings.json
cat > ~/.config/cursor/User/settings.json << 'EOF'
{
    "grok.apiKey": "tu-api-key-aqui",
    "grok.model": "grok-beta",
    "grok.temperature": 0.7,
    "grok.maxTokens": 2048,
    "grok.enableAutoComplete": true,
    "grok.enableChat": true,
    "grok.enableDebug": true,
    "grok.contextWindow": 128000,
    "grok.systemPrompt": "Eres un asistente de programación experto que ayuda a escribir código limpio, eficiente y bien documentado."
}
EOF
```

#### Windsurf
```bash
# Configurar settings.json
cat > ~/.config/windsurf/User/settings.json << 'EOF'
{
    "grok.apiKey": "tu-api-key-aqui",
    "grok.model": "grok-beta",
    "grok.temperature": 0.7,
    "grok.maxTokens": 2048,
    "grok.enableAutoComplete": true,
    "grok.enableChat": true,
    "grok.enableDebug": true,
    "grok.contextWindow": 128000,
    "grok.systemPrompt": "Eres un asistente de programación experto que ayuda a escribir código limpio, eficiente y bien documentado."
}
EOF
```

#### VS Code
```bash
# Instalar extensión Grok AI
code --install-extension grok-ai.grok-ai

# Configurar settings.json
cat > ~/.config/Code/User/settings.json << 'EOF'
{
    "grok.apiKey": "tu-api-key-aqui",
    "grok.model": "grok-beta",
    "grok.temperature": 0.7,
    "grok.maxTokens": 2048,
    "grok.enableAutoComplete": true,
    "grok.enableChat": true,
    "grok.enableDebug": true,
    "grok.contextWindow": 128000,
    "grok.systemPrompt": "Eres un asistente de programación experto que ayuda a escribir código limpio, eficiente y bien documentado."
}
EOF
```

## 🚀 Ejemplos de Uso

### Chat Interactivo
```bash
# Iniciar chat
grok-chat

# Ejemplos de prompts
"Explica cómo funciona un algoritmo de búsqueda binaria"
"Genera una función Python para calcular fibonacci"
"¿Cuál es la diferencia entre listas y tuplas en Python?"
```

### Generación de Código
```bash
# Generar función Python
grok-code "crear una función que calcule el factorial de un número" --lang python

# Generar script Bash
grok-code "crear un script que respalde archivos importantes" --lang bash --output backup.sh

# Generar clase Java
grok-code "crear una clase Persona con atributos nombre y edad" --lang java
```

### Debugging
```bash
# Depurar archivo
grok-debug --file mi_script.py --error "NameError: name 'variable' is not defined"

# Depurar código específico
grok-debug --code "x = 5\nprint(y)" --error "NameError: name 'y' is not defined"
```

## 🔧 Solución de Problemas

### Problemas Comunes

#### 1. API Key Inválida
```bash
# Verificar API Key
curl -X GET "https://api.x.ai/v1/models" \
  -H "Authorization: Bearer $GROK_API_KEY"

# Error común: 401 Unauthorized
# Solución: Verificar que la API Key sea correcta
```

#### 2. Límite de Cuota
```bash
# Error: 429 Too Many Requests
# Solución: Esperar y reintentar
# O verificar límites en https://console.x.ai/
```

#### 3. Conexión
```bash
# Error: Connection refused
# Solución: Verificar conexión a internet
ping api.x.ai

# O usar proxy si es necesario
export https_proxy=http://proxy.ejemplo.com:8080
```

#### 4. Dependencias
```bash
# Error: ModuleNotFoundError: No module named 'xai'
# Solución: Reinstalar el SDK
pip install --upgrade xai-sdk

# O reinstalar en entorno virtual
python3 -m venv venv
source venv/bin/activate
pip install xai-sdk
```

### Depuración Avanzada
```bash
# Ver logs del sistema
journalctl -f | grep python

# Verificar proceso
ps aux | grep python

# Verificar variables de entorno
env | grep GROK

# Test de conexión completa
python3 -c "
import os
from xai import Grok
try:
    client = Grok(api_key=os.getenv('GROK_API_KEY'))
    models = client.models.list()
    print('✅ Conexión exitosa')
    print(f'Modelos disponibles: {[m.id for m in models.data]}')
except Exception as e:
    print(f'❌ Error: {e}')
"
```

## 📚 Recursos Útiles

### Enlaces Oficiales
- **xAI Console**: https://console.x.ai/
- **Documentación**: https://docs.x.ai/
- **GitHub**: https://github.com/xai-org/grok
- **API Reference**: https://docs.x.ai/api-reference

### Modelos Disponibles
- **grok-beta**: Modelo generalista
- **grok-vision**: Modelo con capacidades de imagen
- **grok-coder**: Modelo especializado en código

### Precios y Límites
- **Gratis**: 100 solicitudes/mes
- **Pro**: 1000 solicitudes/mes
- **Enterprise**: Ilimitado

### Comunidad
- **Discord**: https://discord.gg/xai
- **Twitter**: https://twitter.com/xai
- **Reddit**: https://reddit.com/r/xai

## 🎯 Tips Adicionales

### Optimización de Prompts
```bash
# Prompts efectivos para código
"Genera código Python para [tarea] con manejo de errores"
"Crea una función [descripción] que sea eficiente y legible"
"Optimiza este código para mejor rendimiento: [código]"

# Prompts para debugging
"¿Por qué este código produce el error [error]? [código]"
"Cómo solucionar el problema [descripción] en este código: [código]"
```

### Integración con Git
```bash
# Hook de pre-commit para análisis con Grok
cat > .git/hooks/pre-commit << 'EOF'
#!/bin/bash
python3 ~/grok-ai/debug.py --file $(git diff --cached --name-only)
EOF

chmod +x .git/hooks/pre-commit
```

### Automatización
```bash
# Script de análisis automático
cat > ~/grok-ai/auto_analyze.py << 'EOF'
#!/usr/bin/env python3
import os
import subprocess
from xai import Grok

def analyze_project(directory):
    api_key = os.getenv('GROK_API_KEY')
    client = Grok(api_key=api_key)
    
    # Analizar estructura
    result = subprocess.run(['find', directory, '-name', '*.py'], capture_output=True, text=True)
    python_files = result.stdout.strip().split('\n')
    
    for file_path in python_files:
        if file_path:
            print(f"Analizando {file_path}...")
            # Aquí puedes añadir lógica de análisis
EOF

chmod +x ~/grok-ai/auto_analyze.py
```

---

## 🎉 ¡Listo!

Con esta guía completa deberías poder configurar y usar Grok AI en BlackArch sin problemas. Recuerda que necesitas una API Key válida de xAI para acceder a todas las funcionalidades.

**¿Necesitas ayuda con algún paso específico o has encontrado algún error?** 🚀
