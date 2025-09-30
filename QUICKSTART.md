# 🚀 Guía de Inicio Rápido TradingAgents

> 📋 **Versión**: cn-0.1.10 | **Última actualización**: 2025-07-18
> 🎯 **Objetivo**: Completar despliegue y comenzar análisis de acciones en 5 minutos

## 🎯 Elegir Método de Despliegue

### 🐳 Método Uno: Despliegue Docker (Recomendado)

**Escenarios aplicables**: Entorno de producción, experiencia rápida, inicio sin configuración

```bash
# 1. Clonar proyecto
git clone https://github.com/hsliuping/TradingAgents-CN.git
cd TradingAgents-CN

# 2. Configurar variables de entorno
cp .env.example .env
# Editar archivo .env, ingresar claves API

# 3. Construir e iniciar servicios
docker-compose up -d --build

# Nota: La primera ejecución construirá automáticamente la imagen Docker, tomará 5-10 minutos
# El proceso de construcción incluye:
# - Descargar imagen base y dependencias (~800MB)
# - Instalar herramientas del sistema (pandoc, wkhtmltopdf, etc.)
# - Instalar paquetes de dependencias Python
# - Configurar entorno de ejecución

# 4. Acceder a aplicación
# Interfaz Web: http://localhost:8501
# Gestión de base de datos: http://localhost:8081
# Gestión de caché: http://localhost:8082
```

### 🔧 Método de Construcción Paso a Paso (Opcional)

Si prefiere proceder paso a paso, puede construir la imagen por separado primero:

```bash
# Método A: Construcción paso a paso
# 1. Primero construir imagen Docker
docker build -t tradingagents-cn:latest .

# 2. Luego iniciar todos los servicios
docker-compose up -d

# Método B: Construcción e inicio con un comando (Recomendado)
docker-compose up -d --build
```

### 💻 Método Dos: Despliegue Local

**Escenarios aplicables**: Entorno de desarrollo, configuración personalizada, uso offline

```bash
# 1. Clonar proyecto
git clone https://github.com/hsliuping/TradingAgents-CN.git
cd TradingAgents-CN

# 2. Crear entorno virtual
python -m venv env
env\Scripts\activate  # Windows
# source env/bin/activate  # Linux/macOS

# 3. Actualizar pip (¡importante! evita errores de instalación)
python -m pip install --upgrade pip

# 4. Instalar dependencias
pip install -e .

# 5. Configurar variables de entorno
cp .env.example .env
# Editar archivo .env

# 6. Iniciar aplicación
# Método 1: Usar script de inicio simplificado (Recomendado)
python start_web.py

# Método 2: Usar script de inicio del proyecto
python web/run_web.py

# Método 3: Usar streamlit directamente (requiere instalar proyecto primero)
streamlit run web/app.py
```

## 🔧 Configuración del Entorno

### 📋 Configuración Necesaria

Crear archivo `.env` y configurar el siguiente contenido:

```bash
# === Configuración de modelos LLM (elegir al menos uno) ===

# 🇨🇳 DeepSeek (Recomendado - bajo costo, optimizado)
DEEPSEEK_API_KEY=sk-your_deepseek_api_key_here
DEEPSEEK_ENABLED=true

# 🇨🇳 Alibaba Cloud Qwen (Recomendado - buena comprensión)
QWEN_API_KEY=your_qwen_api_key
QWEN_ENABLED=true

# 🌍 Google AI Gemini (Recomendado - fuerte capacidad de razonamiento)
GOOGLE_API_KEY=your_google_api_key
GOOGLE_ENABLED=true

# 🤖 OpenAI (Opcional - capacidad general fuerte, costo alto)
OPENAI_API_KEY=your_openai_api_key
OPENAI_ENABLED=true
```

### 🔑 Obtener Claves API


| Proveedor        | Dirección de Obtención                                                | Características               | Costo      |
| ------------- | ------------------------------------------------------- | ------------------ | --------- |
| **DeepSeek**  | [platform.deepseek.com](https://platform.deepseek.com/) | Llamadas de herramientas, optimizado | 💰 Muy bajo   |
| **Alibaba Cloud**  | [dashscope.aliyun.com](https://dashscope.aliyun.com/)   | Comprensión, respuesta rápida   | 💰 Bajo     |
| **Google AI** | [aistudio.google.com](https://aistudio.google.com/)     | Capacidad de razonamiento, multimodal   | 💰💰 Medio |
| **OpenAI**    | [platform.openai.com](https://platform.openai.com/)     | Capacidad general fuerte         | 💰💰💰 Alto |

### 📊 Configuración Opcional

```bash
# === Configuración de fuentes de datos (opcional) ===
TUSHARE_TOKEN=your_tushare_token          # Datos de mercados mejorados
FINNHUB_API_KEY=your_finnhub_key          # Datos de acciones estadounidenses

# === Configuración de base de datos (Docker configura automáticamente) ===
MONGODB_URL=mongodb://mongodb:27017/tradingagents  # Entorno Docker
REDIS_URL=redis://redis:6379                       # Entorno Docker

# === Configuración de función de exportación ===
EXPORT_ENABLED=true                       # Habilitar exportación de informes
EXPORT_DEFAULT_FORMAT=word,pdf            # Formato de exportación predeterminado
```

## 🚀 Comenzar a Usar

### 1️⃣ Acceder a Interfaz Web

```bash
# Abrir navegador y visitar
http://localhost:8501
```

### 2️⃣ Configurar Parámetros de Análisis

- **🧠 Seleccionar modelo LLM**: DeepSeek V3 / Qwen / Gemini
- **📊 Seleccionar profundidad de análisis**: Rápido / Estándar / Profundo
- **🎯 Seleccionar analista**: Análisis de mercado / Análisis fundamental / Análisis de noticias

### 3️⃣ Ingresar Código de Acción

```bash
# 🇨🇳 Ejemplos de acciones asiáticas
000001  # Ping An Bank
600519  # Kweichow Moutai
000858  # Wuliangye

# 🇺🇸 Ejemplos de acciones estadounidenses  
AAPL    # Apple Inc.
TSLA    # Tesla
MSFT    # Microsoft
```

### 4️⃣ Comenzar Análisis

1. Clic en botón "🚀 Comenzar análisis"
2. **📊 Seguimiento de progreso en tiempo real**: Observar progreso de análisis y paso actual
   - Muestra tiempo usado y tiempo restante estimado
   - Actualización en tiempo real de estado y descripción de pasos de análisis
   - Soporte para actualización manual y control de actualización automática
3. **⏰ Análisis completado**: Esperar a que se complete el análisis (2-10 minutos, depende de la profundidad del análisis)
   - Muestra tiempo total preciso consumido
   - Muestra automáticamente estado "🎉 Análisis completado"
4. **📋 Ver informe**: Clic en botón "📊 Ver informe de análisis"
   - Muestra instantáneamente recomendaciones de inversión detalladas e informe de análisis
   - Soporte para visualización repetida y recuperación después de actualizar página
5. **📄 Exportar informe**: Opción de exportar en formatos Word/PDF/Markdown

### 🆕 Destacados de Nuevas Funciones v0.1.10

#### 🚀 Visualización de Progreso en Tiempo Real
- **Seguimiento de progreso asíncrono**: Muestra progreso de análisis en tiempo real, no más espera a ciegas
- **Reconocimiento inteligente de pasos**: Reconoce automáticamente paso y estado actual del análisis
- **Cálculo preciso de tiempo**: Muestra tiempo real consumido por análisis, no afectado por tiempo de visualización

#### 📊 Gestión Inteligente de Sesiones
- **Persistencia de estado**: Soporte para recuperar estado de análisis después de actualizar página
- **Degradación automática**: Cambio automático a almacenamiento de archivos cuando Redis no está disponible
- **Experiencia de usuario**: Proporciona gestión de sesiones más estable y confiable

#### 🎨 Optimización de Interfaz
- **Botón ver informe**: Ver informe con un clic después de completar análisis
- **Limpieza de botones duplicados**: Elimina botones de actualización duplicados, interfaz más limpia
- **Diseño responsive**: Mejora adaptación móvil y de diferentes pantallas

## 📄 Función de Exportación de Informes

### Formatos Soportados


| Formato            | Uso               | Características               |
| --------------- | ------------------ | ------------------ |
| **📝 Markdown** | Visualización en línea, control de versiones | Ligero, editable     |
| **📄 Word**     | Informes comerciales, edición y modificación | Formato profesional, fácil de editar   |
| **📊 PDF**      | Publicación formal, archivo para impresión | Formato fijo, apariencia profesional |

### Pasos de Exportación

1. Completar análisis de acciones
2. Clic en botón de exportación en página de resultados
3. Seleccionar formato de exportación
4. Descarga automática a local

## 🎯 Características Funcionales

### 🤖 Colaboración Multi-Agente

- **📈 Analista de Mercado**: Indicadores técnicos, análisis de tendencias
- **💰 Analista Fundamental**: Datos financieros, modelos de valoración
- **📰 Analista de Noticias**: Sentimiento de noticias, impacto de eventos
- **🐂🐻 Investigadores**: Debate alcista y bajista
- **🎯 Decisor de Trading**: Toma de decisiones integrales

### 🧠 Selección Inteligente de Modelos

- **DeepSeek V3**: Bajo costo, llamadas de herramientas fuertes, optimizado
- **Qwen**: Buena comprensión, respuesta rápida, Alibaba Cloud
- **Gemini**: Fuerte capacidad de razonamiento, multimodal, Google
- **GPT-4**: Capacidad general más fuerte, costo alto

### 📊 Soporte Completo de Datos

- **🇨🇳 Acciones Asiáticas**: Cotizaciones en tiempo real, datos históricos, indicadores financieros
- **🇺🇸 Acciones Estadounidenses**: NYSE/NASDAQ, datos en tiempo real
- **📰 Noticias**: Noticias financieras en tiempo real, análisis de sentimiento
- **💬 Social**: Sentimiento Reddit, popularidad del mercado

## 🚨 Preguntas Frecuentes

### ❓ ¿Qué hacer si falla el análisis?

1. **Verificar claves API**: Confirmar que las claves son correctas y tienen saldo
2. **Conexión de red**: Asegurar que la red es estable y puede acceder a API
3. **Cambiar modelo**: Intentar cambiar a otro modelo LLM
4. **Ver registros**: Revisar información de error en consola

### ❓ ¿Cómo mejorar la velocidad del análisis?

1. **Elegir modelo rápido**: DeepSeek V3 responde más rápido
2. **Habilitar caché**: Usar Redis para cachear datos repetidos
3. **Modo rápido**: Seleccionar profundidad de análisis rápido
4. **Optimización de red**: Asegurar entorno de red estable

### ❓ ¿Problemas con despliegue Docker?

```bash
# Verificar estado de servicios
docker-compose ps

# Ver registros
docker logs TradingAgents-web

# Reiniciar servicios
docker-compose restart
```

## 📚 Próximos Pasos

### 🎯 Uso Avanzado

1. **📖 Leer documentación**: [Documentación completa](./docs/)
2. **🔧 Entorno de desarrollo**: [Guía de desarrollo](./docs/DEVELOPMENT_SETUP.md)
3. **🚨 Solución de problemas**: [Resolución de problemas](./docs/troubleshooting/)
4. **🏗️ Comprender arquitectura**: [Arquitectura técnica](./docs/architecture/)

### 🤝 Participar en Contribuciones

- 🐛 [Reportar problemas](https://github.com/hsliuping/TradingAgents-CN/issues)
- 💡 [Sugerencias de funciones](https://github.com/hsliuping/TradingAgents-CN/discussions)
- 🔧 [Enviar código](https://github.com/hsliuping/TradingAgents-CN/pulls)
- 📚 [Mejorar documentación](https://github.com/hsliuping/TradingAgents-CN/tree/develop/docs)

---

## 🎉 ¡Felicitaciones por Completar el Inicio Rápido!

**💡 Consejo**: Se recomienda probar primero con un código de acción familiar para experimentar el proceso de análisis completo.

**📞 Soporte Técnico**: [GitHub Issues](https://github.com/hsliuping/TradingAgents-CN/issues)

---

*Última actualización: 2025-07-13 | Versión: cn-0.1.7*
