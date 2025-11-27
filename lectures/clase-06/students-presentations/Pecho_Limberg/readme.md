
PECHO GARNICA LIMBERG - 221045392

🎓 UAGRM Social Media Management System
Sistema integral de gestión de redes sociales para la Universidad Autónoma Gabriel René Moreno (UAGRM), con capacidades de generación de contenido mediante IA y publicación automatizada multiplataforma.
📋 Características Principales
🤖 Generación de Contenido con IA

Adaptación Inteligente: Contenido optimizado automáticamente para cada red social
Validación Académica: Filtro de contenido apropiado para instituciones educativas
Generación Multimedia:

Imágenes con Stability AI
Videos para TikTok con audio sintetizado (gTTS)
Narración natural con reemplazo de siglas



🌐 Redes Sociales Soportadas

Facebook: Publicaciones de texto e imagen
Instagram: Posts con imágenes generadas por IA
LinkedIn: Contenido profesional
WhatsApp: Estados (Stories) con imagen
TikTok: Videos verticales con audio y efectos visuales (modo privado)

💬 Sistema de Chat Conversacional

Interfaz estilo ChatGPT
Historial de conversaciones persistente
Soporte Markdown en respuestas
Selector de redes objetivo

🔐 Autenticación y Seguridad

Sistema de login/registro con JWT
Tokens con expiración configurable (7 días por defecto)
PostgreSQL para almacenamiento seguro
Validación de usuarios por conversación

🏗️ Arquitectura del Sistema
┌─────────────────┐
│   Frontend      │
│   (React +      │
│   TypeScript)   │
└────────┬────────┘
         │
         │ HTTP/REST
         │
┌────────▼────────┐
│   Backend       │
│   (FastAPI)     │
├─────────────────┤
│ • Auth Service  │
│ • Chat Service  │
│ • LLM Service   │
│ • Social APIs   │
└────────┬────────┘
         │
    ┌────┴────┐
    │         │
┌───▼───┐ ┌──▼──────┐
│  DB   │ │ External│
│Postgre│ │   APIs  │
│  SQL  │ │         │
└───────┘ └─────────┘
          │
          ├─ Gemini 2.0
          ├─ Stability AI
          ├─ Pexels
          ├─ Meta Graph API
          ├─ TikTok API
          ├─ LinkedIn API
          └─ Whapi.Cloud
🚀 Instalación y Configuración
Requisitos Previos

Python 3.9+
Node.js 18+
PostgreSQL 14+
FFmpeg (para generación de videos TikTok)

Backend

Clonar el repositorio

bashgit clone <repository-url>
cd backend

Instalar dependencias

bashpip install -r requirements.txt

Configurar variables de entorno (.env)

env# Base de Datos
DATABASE_URL=postgresql://user:password@localhost:5432/redes_sociales_db

# Autenticación
TOKEN_EXPIRATION_DAYS=7

# APIs de IA
GOOGLE_API_KEY=your_gemini_api_key
STABILITY_API_KEY=your_stability_api_key
PEXELS_API_KEY=your_pexels_api_key

# APIs de Redes Sociales
META_ACCESS_TOKEN=your_meta_token
FACEBOOK_PAGE_ID=your_page_id
INSTAGRAM_ACCOUNT_ID=your_ig_account_id
LINKEDIN_ACCESS_TOKEN=your_linkedin_token
TIKTOK_ACCESS_TOKEN=your_tiktok_token
WHAPI_TOKEN=your_whapi_token
WHAPI_CHANNEL_ID=your_channel_id

Iniciar servidor

bashuvicorn main:app --reload --host 0.0.0.0 --port 8000
Frontend

Navegar al directorio

bashcd frontend

Instalar dependencias

bashnpm install

Iniciar servidor de desarrollo

bashnpm run dev
```

La aplicación estará disponible en `http://localhost:5173`

## 📖 Uso del Sistema

### 1. Autenticación
- Crear cuenta con username, email y password
- Iniciar sesión para acceder al dashboard

### 2. Chat de Generación de Contenido

**Ejemplo de uso:**
```
Usuario: "La FICCT anuncia inscripciones abiertas del 1 al 5 de diciembre"

Sistema: 
✅ Valida contenido académico
✅ Adapta para cada red seleccionada
✅ Genera recursos multimedia
✅ Publica automáticamente
✅ Retorna enlaces de las publicaciones
3. Selección de Redes

Utilizar los botones superiores para seleccionar redes objetivo
Múltiples redes pueden seleccionarse simultáneamente
El contenido se adaptará automáticamente a cada plataforma

🎨 Adaptación de Contenido por Red
Facebook

Tono: Profesional pero cercano
Formato: Texto largo permitido
Hashtags: 2-3 relevantes (#UAGRM)
Multimedia: Imagen opcional

Instagram

Tono: Visual, dinámico, juvenil
Formato: Texto corto (≤2,200 chars)
Hashtags: 5-8 hashtags
Multimedia: Imagen generada por IA (obligatoria)

TikTok

Tono: Viral, directo, juvenil
Formato: Texto muy corto con hook
Hashtags: 5-8 de tendencia
Multimedia: Video vertical 9:16 con audio sintetizado

LinkedIn

Tono: Profesional, corporativo
Formato: Texto medio (≤3,000 chars)
Hashtags: 3-5 profesionales
Multimedia: Solo texto

WhatsApp

Tono: Conversacional, directo
Formato: Mensaje estructurado
Hashtags: Ninguno
Multimedia: Imagen en base64

🧪 Testing
El proyecto incluye pruebas unitarias para cada integración:
bashcd backend
pytest tests/ -v
Cobertura de tests:

✅ Facebook Integration (test_facebook.py)
✅ Instagram Integration (test_instagram.py)
✅ LinkedIn Integration (test_linkedin.py)
✅ TikTok Integration (test_tiktok.py)
✅ WhatsApp Integration (test_whatsapp.py)

📊 Estructura de Base de Datos
Tabla users
sqlid: Integer (PK)
username: String (Unique)
email: String (Unique)
hashed_password: String
created_at: DateTime
is_active: Boolean
Tabla conversations
sqlid: Integer (PK)
user_id: Integer (FK)
title: String
created_at: DateTime
updated_at: DateTime
Tabla messages
sqlid: Integer (PK)
conversation_id: Integer (FK)
role: String ('user' | 'assistant')
content: Text
created_at: DateTime
🔧 Endpoints Principales
Autenticación

POST /api/auth/register - Registro de usuario
POST /api/auth/login - Inicio de sesión
POST /api/auth/logout - Cerrar sesión
GET /api/auth/me - Usuario actual

Chat

GET /api/chat/conversations - Listar conversaciones
POST /api/chat/conversations - Crear conversación
GET /api/chat/conversations/{id} - Obtener detalles
DELETE /api/chat/conversations/{id} - Eliminar conversación
POST /api/chat/conversations/{id}/messages - Enviar mensaje

Publicaciones

POST /api/posts/adapt - Adaptar contenido
POST /api/posts/publish-multi - Publicar en múltiples redes

🎯 Flujo de Publicación Completo
mermaidgraph TD
    A[Usuario envía mensaje] --> B[Validación académica]
    B --> C{¿Es contenido académico?}
    C -->|No| D[Rechazar con razón]
    C -->|Sí| E[Adaptar para cada red]
    E --> F[Generar recursos multimedia]
    F --> G[Publicar en redes]
    G --> H[Retornar resultados]
🐛 Solución de Problemas
FFmpeg no encontrado (TikTok)
bash# Windows
# Descargar de https://ffmpeg.org/download.html
# Agregar al PATH o configurar ruta en llm_service.py

# Linux/Mac
sudo apt install ffmpeg  # Debian/Ubuntu
brew install ffmpeg      # macOS
Error de autenticación en redes sociales

Verificar tokens en .env
Comprobar permisos de API
Revisar expiración de tokens
Ejecutar scripts de verificación en /backend/setup/

Error de base de datos
bash# Verificar conexión
psql -U postgres -h localhost -p 5432

# Reinicializar tablas
python -c "from auth.database import init_db; init_db()"
📄 Licencia
Este proyecto es parte del sistema de gestión de comunicación digital de la UAGRM.
👥 Contribuidores

Desarrollo: Sistema de Gestión de Redes Sociales UAGRM
Facultad: FICCT (Facultad de Ingeniería de Ciencias de la Computación)

📞 Soporte
Para reportar problemas o solicitar características, crear un issue en el repositorio del proyecto.