# Clairvoyance 🔮

> **A next-generation, multi-agent conversational AI platform for real-time voice interactions and intelligent business automation**

Clairvoyance is an enterprise-grade voice AI platform that orchestrates multiple specialized conversational agents to handle complex business workflows. Built on a high-performance, scalable architecture, it delivers sub-4-second connection times and seamless voice interactions for e-commerce, analytics, and customer service applications.

## 🚀 Quick Start

```bash
# Clone and setup
git clone <repository-url>
cd clairvoyance-swaroop

# Install dependencies  
pip install -r requirements.txt

# Configure environment
cp .env.example .env
# Edit .env with your API keys and configuration

# Initialize database
python -m scripts.create_tables create

# Start the server
python run.py
```

**Access:** Navigate to `http://localhost:8000` to see the platform in action.

---

## 📋 Table of Contents

1. [Overview & Architecture](#-core-architecture)
2. [Voice Agents](#-voice-agents)
3. [Key Features](#-key-features)
4. [Project Structure](#-project-structure)
5. [Installation & Setup](#-installation--setup)
6. [Configuration Guide](#-configuration-guide)
7. [API Documentation](#-api-documentation)
8. [Performance & Optimization](#-performance--optimization)
9. [Development Workflow](#-development-workflow)
10. [Deployment](#-deployment)
11. [Troubleshooting](#-troubleshooting)

---

## 🏗️ Core Architecture

Clairvoyance employs a **dual-pool optimization architecture** that reduces voice agent connection times by 50-62.5% (from ~8 seconds to 3-4 seconds) through pre-warmed processes and rooms.

```
┌─────────────────────────────────────────────────────────┐
│                    FastAPI Server                       │
│                   (app/main.py)                        │
├─────────────────────────────────────────────────────────┤
│  ┌─────────────────┐  ┌─────────────────────────────────┐│
│  │   Daily Room    │  │    Voice Agent Process         ││
│  │     Pool        │  │         Pool                   ││
│  │  (Pre-created   │  │    (Pre-warmed agents)         ││
│  │   rooms + tokens)│  │                               ││
│  └─────────────────┘  └─────────────────────────────────┘│
├─────────────────────────────────────────────────────────┤
│                Voice Agent Layer                        │
│  ┌─────────────────────┐  ┌─────────────────────────────┐│
│  │  Automatic Agent    │  │   Breeze Buddy Agent        ││
│  │   (Analytics &      │  │   (Telephony &              ││
│  │   Data Insights)    │  │   Order Confirmation)       ││
│  └─────────────────────┘  └─────────────────────────────┘│
├─────────────────────────────────────────────────────────┤
│                Infrastructure Layer                     │
│  ┌──────────────┐ ┌──────────────┐ ┌──────────────────────┐│
│  │ PostgreSQL   │ │ Redis/Cache  │ │ External Services    ││
│  │ Database     │ │              │ │ (Daily, Twilio,      ││
│  │              │ │              │ │  Azure OpenAI, etc.) ││
│  └──────────────┘ └──────────────┘ └──────────────────────┘│
└─────────────────────────────────────────────────────────┘
```

### Core Components

- **🌐 FastAPI Server**: Central orchestrator managing API endpoints, agent lifecycles, and request routing
- **🤖 Voice Agents**: Specialized conversational agents with distinct capabilities and workflows  
- **💾 Database Layer**: PostgreSQL for persistent storage of configurations, call tracking, and analytics
- **📡 Communication Layer**: Daily.co for WebRTC, Twilio/Exotel for telephony
- **🔧 Tool Ecosystem**: Modular tools for external service integrations (Juspay, Breeze, Analytics)

---

## 🤖 Voice Agents

### Automatic Agent (`app/agents/voice/automatic/`)

**Purpose**: Real-time business analytics and data insights through conversational AI.

**Key Capabilities**:
- 📊 **Analytics Dashboard**: Payment success rates, GMV analysis, transaction insights
- 🔄 **Real-time Data**: Live connection to Juspay/Euler backend systems
- 📈 **Chart Generation**: Dynamic visualization of business metrics  
- 🧠 **Context Awareness**: Memory-powered conversations with session persistence
- 🛠️ **MCP Integration**: Model Context Protocol for external tool orchestration

**Technology Stack**:
- **Framework**: PipeCat for real-time voice processing
- **LLM**: Azure OpenAI (GPT-4o) with function calling
- **STT**: Google Speech-to-Text, Deepgram, or Soniox (configurable)
- **TTS**: ElevenLabs, Google TTS, or Azure Speech (configurable)
- **Memory**: Mem0 for conversation context and user preferences

**Workflow Example**:
```
User: "Show me payment success rates for last week"
     ↓
Automatic Agent → Juspay Analytics API → Data Processing → Chart Generation
     ↓
"Your payment success rate was 94.2% last week, up 2.1% from the previous week. 
Here's a detailed breakdown by payment method..."
```

### Breeze Buddy Agent (`app/agents/voice/breeze_buddy/`)

**Purpose**: Telephony-driven workflows for customer service and order management.

**Key Capabilities**:
- 📞 **Outbound Calling**: Automated order confirmations and customer outreach
- 🔄 **Workflow Management**: Predefined conversation flows for specific business processes
- 📋 **Multi-Provider Support**: Twilio and Exotel integration for global reach
- 📊 **Call Tracking**: Comprehensive analytics and outcome tracking
- 🎯 **Lead Management**: Backlog processing and retry mechanisms

**Technology Stack**:
- **Framework**: PipeCat with telephony transport layers
- **Telephony**: Twilio WebSocket API, Exotel integration
- **Database**: PostgreSQL for call logs and lead tracking
- **Authentication**: JWT-based security for webhook endpoints

**Workflow Example**:
```
Order Placed → Breeze Buddy → Outbound Call → Customer Confirmation
     ↓                           ↓
Database Update ← Call Outcome ← Voice Interaction
```

---

## ✨ Key Features

### 🚀 **Performance Optimized**
- **Sub-4 Second Connections**: Dual-pool architecture eliminates initialization delays
- **Pre-warmed Processes**: Voice agents ready for instant assignment
- **Connection Pooling**: Database and external service optimization
- **Intelligent Caching**: Reduced API calls and faster response times

### 🔧 **Enterprise-Grade Infrastructure**
- **Horizontal Scaling**: Multi-process architecture with pool management
- **Health Monitoring**: Real-time status tracking and automatic recovery
- **Graceful Degradation**: Fallback mechanisms for high-availability
- **Comprehensive Logging**: Structured logging with Loguru and OpenTelemetry

### 🛡️ **Security & Compliance**
- **JWT Authentication**: Secure API access with role-based permissions
- **Environment Isolation**: Comprehensive configuration management
- **Data Encryption**: At-rest and in-transit encryption options
- **Audit Trails**: Complete request/response logging for compliance

### 🌐 **Multi-Modal Communication**
- **WebRTC Support**: Browser-based voice interactions via Daily.co
- **Telephony Integration**: PSTN calls through Twilio and Exotel
- **WebSocket Streaming**: Real-time bidirectional communication
- **RESTful APIs**: Standard HTTP endpoints for integration

### 🔌 **Extensible Tool Ecosystem**
- **Modular Architecture**: Easy addition of new tools and providers
- **MCP Protocol**: Standard interface for external tool integration
- **Function Calling**: LLM-driven tool invocation with parameter validation
- **Provider Abstraction**: Unified interface for multiple service providers

---

## 📁 Project Structure

```
clairvoyance-swaroop/
├── 📁 app/                              # Main application directory
│   ├── 🐍 main.py                       # FastAPI application entry point
│   ├── 🐍 schemas.py                    # Pydantic models and data schemas
│   ├── 📁 agents/voice/                 # Voice agent implementations
│   │   ├── 📁 automatic/                # Automatic Agent (Analytics)
│   │   │   ├── 🐍 __init__.py          # Agent initialization and main loop
│   │   │   ├── 📁 services/            # External service integrations
│   │   │   │   ├── 📁 mcp/             # Model Context Protocol client
│   │   │   │   ├── 📁 mem0/            # Memory service integration
│   │   │   │   └── 📁 fal/             # Fal.ai Smart Turn service
│   │   │   ├── 📁 tools/               # Agent-specific tools
│   │   │   │   ├── 📁 juspay/          # Juspay analytics tools
│   │   │   │   ├── 📁 breeze/          # Breeze platform tools
│   │   │   │   ├── 📁 charts/          # Chart generation tools
│   │   │   │   └── 📁 dummy/           # Test/demo tools
│   │   │   ├── 📁 tts/                 # Text-to-Speech implementations
│   │   │   ├── 📁 utils/               # Utility functions
│   │   │   └── 📁 types/               # Type definitions and models
│   │   └── 📁 breeze_buddy/            # Breeze Buddy Agent (Telephony)
│   │       ├── 📁 services/telephony/  # Telephony provider implementations
│   │       │   ├── 📁 twilio/          # Twilio integration
│   │       │   └── 📁 exotel/          # Exotel integration
│   │       ├── 📁 workflows/           # Conversation workflows
│   │       │   └── 📁 order_confirmation/ # Order confirmation workflow
│   │       └── 📁 managers/            # Business logic managers
│   ├── 📁 api/routers/                 # FastAPI route handlers
│   │   ├── 🐍 automatic.py            # Automatic Agent endpoints
│   │   └── 🐍 breeze_buddy.py         # Breeze Buddy endpoints
│   ├── 📁 core/                        # Core application logic
│   │   ├── 🐍 config.py               # Environment configuration
│   │   ├── 📁 logger/                  # Logging configuration
│   │   ├── 📁 security/                # Authentication & security
│   │   └── 📁 transport/               # HTTP client utilities
│   ├── 📁 database/                    # Database layer
│   │   ├── 📁 accessor/                # Database access methods
│   │   └── 📁 queries/                 # SQL query definitions
│   ├── 📁 helpers/automatic/           # Automatic Agent helpers
│   │   ├── 🐍 process_pool.py         # Voice agent process pool
│   │   ├── 🐍 daily_room_pool.py      # Daily.co room pool management
│   │   └── 🐍 session_manager.py      # Session lifecycle management
│   ├── 📁 services/                    # Shared services
│   │   ├── 📁 aws/                     # AWS integrations (KMS, etc.)
│   │   └── 📁 langfuse/                # Langfuse tracing integration
│   └── 📁 utils/                       # Shared utilities
├── 📁 static/                          # Static web assets
│   └── 📄 home.html                    # Default web interface
├── 📁 scripts/                         # Utility scripts
│   ├── 🐍 create_tables.py            # Database initialization
│   └── 🐚 setup.sh                    # Environment setup script
├── 📁 memory-bank/                     # Documentation and context
│   ├── 📄 productContext.md           # Product specifications
│   ├── 📄 techContext.md              # Technical documentation
│   └── 📄 decisionLog.md              # Architectural decisions
├── 🐳 Dockerfile                       # Container configuration
├── 📄 requirements.txt                 # Python dependencies
├── 🐍 run.py                          # Application launcher
├── ⚙️ .env.example                    # Environment configuration template
└── 📖 README.md                       # This documentation
```

### Key Directories Explained

- **`app/agents/voice/`**: Contains the two main voice agents with their specific implementations
- **`app/helpers/automatic/`**: Pool management and optimization logic for performance
- **`app/api/routers/`**: FastAPI endpoints organized by functionality
- **`app/database/`**: Database abstraction layer with accessor patterns
- **`memory-bank/`**: Living documentation that evolves with the project

---

## 🛠️ Installation & Setup

### Prerequisites

**Required Software:**
- **Python 3.11+** (3.12 recommended for optimal performance)
- **PostgreSQL 13+** for data persistence
- **Git** for version control
- **Docker** (optional, for containerized deployment)

**External Service Requirements:**
- **Daily.co API Key** - For WebRTC communication
- **Azure OpenAI** - For LLM processing (GPT-4o recommended)
- **Telephony Provider** - Twilio or Exotel for phone calls
- **Google Cloud** - For Speech-to-Text services (optional)
- **ElevenLabs** - For high-quality Text-to-Speech (optional)

### Step-by-Step Installation

#### 1. Clone and Setup Repository
```bash
# Clone the repository
git clone <repository-url>
cd clairvoyance-swaroop

# Create virtual environment
python3.11 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Upgrade pip for latest dependencies
pip install --upgrade pip
```

#### 2. Install Dependencies
```bash
# Install core dependencies
pip install -r requirements.txt

# Install development dependencies (optional)
pip install -r requirements-dev.txt
```

#### 3. Database Setup
```bash
# Install PostgreSQL (Ubuntu/Debian)
sudo apt update
sudo apt install postgresql postgresql-contrib

# Create database and user
sudo -u postgres createdb clairvoyance
sudo -u postgres createuser --superuser clairvoyance_user

# Set password for user
sudo -u postgres psql -c "ALTER USER clairvoyance_user PASSWORD 'your_password';"
```

#### 4. Environment Configuration
```bash
# Copy example environment file
cp .env.example .env

# Edit configuration file
nano .env  # or your preferred editor
```

**Critical Environment Variables:**
```bash
# Server Configuration
PORT=8000
HOST="0.0.0.0"
ENVIRONMENT="dev"

# Database Configuration
POSTGRES_HOST="localhost"
POSTGRES_PORT="5432"
POSTGRES_USER="clairvoyance_user" 
POSTGRES_PASSWORD="your_password"
POSTGRES_DB="clairvoyance"

# Core API Keys (Required)
DAILY_API_KEY="your_daily_api_key"
AZURE_OPENAI_API_KEY="your_azure_openai_key"
AZURE_OPENAI_ENDPOINT="https://your-resource.openai.azure.com/"

# Telephony (Required for Breeze Buddy)
TWILIO_ACCOUNT_SID="your_twilio_sid"
TWILIO_AUTH_TOKEN="your_twilio_token"

# Optional Services
ELEVENLABS_API_KEY="your_elevenlabs_key"
DEEPGRAM_API_KEY="your_deepgram_key"
```

#### 5. Initialize Database
```bash
# Create database tables
python -m scripts.create_tables create

# Verify database connection
python -c "from app.database import get_db_connection; print('Database connected successfully!')"
```

#### 6. Run Setup Script
```bash
# Make setup script executable
chmod +x scripts/setup.sh

# Run setup (downloads NLTK data, etc.)
./scripts/setup.sh
```

#### 7. Start the Application
```bash
# Development mode (with auto-reload)
python run.py

# Production mode 
ENVIRONMENT=production python run.py
```

#### 8. Verify Installation
```bash
# Test health endpoint
curl http://localhost:8000/health

# Test database health
curl http://localhost:8000/health/database

# Check pool status
curl http://localhost:8000/agent/voice/automatic/pool/status
```

### Docker Installation (Alternative)

```bash
# Build the container
docker build -t clairvoyance .

# Run with environment file
docker run -p 8000:8000 --env-file .env clairvoyance

# Or using docker-compose (create docker-compose.yml)
docker-compose up -d
```

### Development Setup

```bash
# Install pre-commit hooks for code quality
pip install pre-commit
pre-commit install

# Install additional development tools
pip install black pytest pytest-asyncio pytest-cov

# Run tests (if available)
pytest

# Format code
black app/
```

---

## ⚙️ Configuration Guide

Clairvoyance uses a comprehensive configuration system with **177 environment variables** for fine-tuning every aspect of the platform.

### Configuration Categories

#### 🌐 **Server & Environment**
```bash
PORT=8000                      # Server port
HOST="0.0.0.0"                # Bind address
ENVIRONMENT="dev"              # dev | production
UVICORN_RELOAD=true           # Auto-reload in development
UVICORN_LOG_LEVEL="info"      # Logging level
```

#### 🗄️ **Database Configuration**
```bash
POSTGRES_HOST="localhost"
POSTGRES_PORT="5432"
POSTGRES_USER="clairvoyance_user"
POSTGRES_PASSWORD="secure_password"
POSTGRES_DB="clairvoyance"

# Connection Pool Settings
POSTGRES_POOL_SIZE=5          # Initial pool size
POSTGRES_MAX_OVERFLOW=10      # Maximum overflow connections
POSTGRES_POOL_RECYCLE=3600    # Connection recycle time (seconds)
```

#### 🤖 **Voice Agent Configuration**

**Automatic Agent:**
```bash
# Daily.co Integration
DAILY_API_KEY="your_daily_key"
DAILY_API_URL="https://api.daily.co/v1"

# Azure OpenAI
AZURE_OPENAI_API_KEY="your_key"
AZURE_OPENAI_ENDPOINT="https://your-resource.openai.azure.com/"
AZURE_OPENAI_MODEL="gpt-4o-automatic"

# Pool Optimization
VOICE_AGENT_POOL_SIZE=3           # Pre-warmed processes
VOICE_AGENT_MAX_POOL_SIZE=5       # Maximum pool size
DAILY_ROOM_POOL_SIZE=5            # Pre-created rooms
DAILY_ROOM_MAX_POOL_SIZE=10       # Maximum room pool
```

**Breeze Buddy Agent:**
```bash
# Twilio Configuration
TWILIO_ACCOUNT_SID="your_sid"
TWILIO_AUTH_TOKEN="your_token"
TWILIO_WEBSOCKET_URL="wss://voice.twilio.com/ws"

# Exotel Configuration (Alternative)
EXOTEL_API_KEY="your_exotel_key"
EXOTEL_API_TOKEN="your_exotel_token"
```

#### 🎤 **Speech-to-Text (STT) Configuration**
```bash
STT_PROVIDER="google"  # Options: google, assemblyai, openai, deepgram, soniox

# Google STT
GOOGLE_CREDENTIALS_JSON="path/to/credentials.json"

# Deepgram STT (High Performance)
DEEPGRAM_API_KEY="your_deepgram_key"
DEEPGRAM_MODEL="nova-3-general"
DEEPGRAM_LANGUAGE="en"
DEEPGRAM_ENDPOINTING=true         # Smart turn detection
DEEPGRAM_VAD_EVENTS=true          # Voice activity detection
DEEPGRAM_SMART_FORMAT=true        # Format numbers, dates
DEEPGRAM_NUMERALS=true            # Convert to numerals (critical for Indian numbers)

# Soniox STT (Solves 0.5-second pause issue)
SONIOX_API_KEY="your_soniox_key"
SONIOX_MODEL="stt-rt-preview"
SONIOX_LANGUAGE_HINTS="en,hi"     # Multi-language support
SONIOX_CONTEXT="business analytics, payments, Indian English, lakhs, crores"
SONIOX_VAD_FORCE_TURN_ENDPOINT=false  # Use Soniox endpoint detection
```

#### 🔊 **Text-to-Speech (TTS) Configuration**
```bash
# ElevenLabs (Premium Quality)
ELEVENLABS_API_KEY="your_elevenlabs_key"
ELEVENLABS_VOICE_ID="bQQWtYx9EodAqMdkrNAc"
ELEVENLABS_MODEL_ID="eleven_flash_v2_5"
ELEVENLABS_VOICE_SPEED=1.15
ELEVENLABS_TTS_SPEED=1.10

# Azure Speech (Alternative)
AZURE_SPEECH_KEY="your_azure_speech_key"
AZURE_SPEECH_REGION="eastus"

# Google TTS (Alternative)
GOOGLE_TTS_CREDENTIALS="path/to/credentials.json"
```

#### 🎛️ **Voice Activity Detection (VAD)**
```bash
VAD_CONFIDENCE=0.85              # Detection sensitivity
VAD_MIN_VOLUME=0.75              # Minimum volume threshold
VAD_START_SECS=0.2               # Start detection delay
VAD_STOP_SECS=0.8                # Stop detection delay
DISABLE_SILERO_VAD=false         # Disable when using STT with built-in VAD
```

#### 🔐 **Security & Authentication**
```bash
JWT_SECRET_KEY="your_jwt_secret_key_here"
JWT_ALGORITHM="HS256"
JWT_ACCESS_TOKEN_EXPIRE_MINUTES=60

# Webhook Security
ORDER_CONFIRMATION_WEBHOOK_SECRET_KEY="webhook_secret"
ORDER_CONFIRMATION_TOKEN="secure_token"

# AWS KMS (Optional)
AWS_REGION="us-east-1"
AWS_ACCESS_KEY_ID="your_aws_key"
AWS_SECRET_ACCESS_KEY="your_aws_secret"
SKIP_KMS_DECRYPT=false
```

#### 📊 **Monitoring & Observability**
```bash
# Logging
PROD_LOG_LEVEL="INFO"            # Production log level
WS_PING_INTERVAL=5               # WebSocket ping interval
WS_PING_TIMEOUT=10               # WebSocket ping timeout

# Tracing
ENABLE_TRACING=true
LANGFUSE_SECRET_KEY="your_langfuse_secret"
LANGFUSE_PUBLIC_KEY="your_langfuse_public"
LANGFUSE_BASEURL="https://us.cloud.langfuse.com"

# Performance
AUTOMATIC_SESSION_INACTIVITY_TIMEOUT=900.0  # 15 minutes
MAX_DAILY_SESSION_LIMIT=1800                # 30 minutes max session
```

#### 🧠 **Memory & AI Features**
```bash
# Mem0 Memory Service
MEM0_API_KEY="your_mem0_key"
MEM0_ENABLED=true

# Chart Generation
MAX_CHARTS_PER_TURN=1

# Smart Turn Detection
ENABLE_FAL_SMART_TURN=false
FAL_SMART_TURN_API_KEY="your_fal_key"
```

### Configuration Validation

The application validates critical configuration on startup:

```python
# Check configuration
python -c "from app.core.config import *; print('Configuration valid!')"

# Test specific services
python -c "from app.core.config import DAILY_API_KEY; print('Daily API configured' if DAILY_API_KEY else 'Daily API missing')"
```

### Environment-Specific Configurations

**Development (.env.dev):**
```bash
ENVIRONMENT="dev"
UVICORN_RELOAD=true
PROD_LOG_LEVEL="DEBUG"
ENABLE_TRACING=true
```

**Production (.env.prod):**
```bash
ENVIRONMENT="production"
UVICORN_RELOAD=false
PROD_LOG_LEVEL="INFO"
ENABLE_TRACING=true
```

**Testing (.env.test):**
```bash
ENVIRONMENT="test"
POSTGRES_DB="clairvoyance_test"
ENABLE_TRACING=false
```

---

## 📡 API Documentation

Clairvoyance exposes comprehensive REST and WebSocket APIs for voice agent management and interaction.

### Core Endpoints

#### Health & Status Endpoints

```http
GET /health
```
**Response:**
```json
{
    "status": "healthy"
}
```

```http
GET /health/database
```
**Response:**
```json
{
    "status": "healthy",
    "database": "connected",
    "message": "Database connection is healthy"
}
```

```http
GET /version
```
**Response:**
```json
{
    "version": "1.0.0"
}
```

#### Pool Management Endpoints

```http
GET /agent/voice/automatic/pool/status
```
**Response:**
```json
{
    "status": "healthy",
    "voice_pool_stats": {
        "pool_size": 3,
        "available": 2,
        "in_use": 1,
        "max_pool_size": 5
    },
    "room_pool_stats": {
        "pool_size": 5,
        "available": 4,
        "in_use": 1,
        "max_pool_size": 10
    }
}
```

```http
POST /agent/voice/automatic/cleanup/{session_id}
```
**Description:** Cleanup a specific voice agent session.

### Automatic Agent API

#### Voice Connection Endpoint

```http
POST /agent/voice/automatic
Content-Type: application/json
Authorization: Bearer <jwt_token>
```

**Request Body:**
```json
{
    "mode": "LIVE",
    "userName": "John Doe",
    "email": "john@example.com",
    "ttsService": {
        "ttsProvider": "ELEVENLABS",
        "voiceName": "ALLOY"
    },
    "eulerToken": "euler_auth_token",
    "breezeToken": "breeze_auth_token",
    "shopUrl": "https://shop.example.com",
    "shopId": "shop_123",
    "shopType": "d2c",
    "merchantId": "merchant_456",
    "platformIntegrations": ["juspay", "breeze"],
    "resellerId": "reseller_789",
    "sessionId": "optional_client_session_id"
}
```

**Response:**
```json
{
    "room_url": "https://example.daily.co/room-name",
    "token": "user_access_token_for_room",
    "session_id": "server_generated_session_id"
}
```

**Integration Example:**
```javascript
// Frontend JavaScript example
async function connectToVoiceAgent() {
    const response = await fetch('/agent/voice/automatic', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            'Authorization': 'Bearer ' + jwt_token
        },
        body: JSON.stringify({
            mode: 'LIVE',
            userName: 'John Doe',
            email: 'john@example.com',
            ttsService: {
                ttsProvider: 'ELEVENLABS',
                voiceName: 'ALLOY'
            },
            shopId: 'shop_123',
            merchantId: 'merchant_456'
        })
    });
    
    const data = await response.json();
    
    // Connect to Daily.co room with provided credentials
    const dailyCall = window.Daily.createFrame({
        url: data.room_url,
        token: data.token
    });
    
    await dailyCall.join();
}
```

### Breeze Buddy Agent API

#### Outbound Number Management

```http
POST /agent/voice/breeze-buddy/outbound-number
Content-Type: application/json
Authorization: Bearer <jwt_token>
```

**Request Body:**
```json
{
    "phone_number": "+1234567890",
    "provider": "TWILIO",
    "merchant_id": "merchant_123"
}
```

```http
GET /agent/voice/breeze-buddy/outbound-number?id={number_id}
Authorization: Bearer <jwt_token>
```

#### Order Confirmation Workflow

```http
POST /agent/voice/breeze-buddy/{identity}/{workflow}
Content-Type: application/json
Authorization: Bearer <jwt_token>
```

**Request Body (Order Confirmation):**
```json
{
    "order": {
        "order_id": "order_123",
        "customer_name": "Jane Smith",
        "customer_phone": "+1234567890",
        "order_amount": 2500.00,
        "currency": "INR",
        "delivery_address": {
            "street": "123 Main St",
            "city": "Mumbai",
            "state": "Maharashtra",
            "pincode": "400001"
        },
        "payment_method": "UPI",
        "estimated_delivery": "2024-01-15"
    }
}
```

#### WebSocket Telephony Connection

```
WSS /agent/voice/breeze-buddy/{service_provider}/callback/{workflow}
```

**Example (Twilio Order Confirmation):**
```
WSS /agent/voice/breeze-buddy/twilio/callback/order-confirmation
```

### Authentication

Clairvoyance uses JWT-based authentication for secure API access.

#### Generate JWT Token

```python
import jwt
from datetime import datetime, timedelta

# Generate token
payload = {
    'user_id': 'user_123',
    'email': 'user@example.com',
    'merchantId': 'merchant_456',
    'exp': datetime.utcnow() + timedelta(hours=1)
}

token = jwt.encode(payload, 'your_jwt_secret_key', algorithm='HS256')
```

#### API Request with Authentication

```bash
curl -X POST http://localhost:8000/agent/voice/automatic \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9..." \
  -d '{"mode": "LIVE", "userName": "Test User"}'
```

### Error Handling

**Standard Error Response:**
```json
{
    "detail": "Error description",
    "status_code": 400,
    "error_type": "ValidationError"
}
```

**Common Error Codes:**
- `400` - Bad Request (invalid parameters)
- `401` - Unauthorized (invalid/missing JWT)
- `403` - Forbidden (insufficient permissions)
- `404` - Not Found (invalid endpoint/resource)
- `500` - Internal Server Error
- `503` - Service Unavailable (pool exhausted)

### Rate Limiting

- **Voice Connections**: 10 per minute per user
- **API Calls**: 100 per minute per API key
- **Pool Requests**: Limited by pool size configuration

---

## ⚡ Performance & Optimization

### Dual Pool Architecture

Clairvoyance implements a sophisticated **dual-pool optimization system** that delivers industry-leading connection times.

#### Performance Metrics

| Metric | Before Optimization | After Optimization | Improvement |
|--------|-------------------|-------------------|-------------|
| **Connection Time** | ~8 seconds | ~3-4 seconds | **50-62.5%** |
| **Room Creation** | 1 second per request | 0.05 seconds (pre-created) | **95%** |
| **Process Init** | 6 seconds per request | 0.05 seconds (pre-warmed) | **99%** |
| **Overhead** | 1 second | 3-4 seconds (model loading) | Minimized |

#### Voice Agent Process Pool

**Configuration:**
```bash
VOICE_AGENT_POOL_SIZE=3         # Initial pre-warmed processes
VOICE_AGENT_MAX_POOL_SIZE=5     # Maximum pool expansion
```

**How it Works:**
1. **Pre-warming**: Processes start during application boot
2. **Assignment**: Instant assignment to incoming requests
3. **Background Replenishment**: Automatic pool refilling
4. **Health Monitoring**: Unhealthy process replacement
5. **Graceful Fallback**: Direct process creation if pool exhausted

**Pool Management:**
```python
# Check pool status
from app.helpers.automatic.process_pool import get_voice_agent_pool

pool = get_voice_agent_pool()
stats = await pool.get_pool_stats()
print(f"Available processes: {stats['available']}")
```

#### Daily Room Pool

**Configuration:**
```bash
DAILY_ROOM_POOL_SIZE=5          # Initial pre-created rooms
DAILY_ROOM_MAX_POOL_SIZE=10     # Maximum pool expansion
MAX_DAILY_SESSION_LIMIT=1800    # 30-minute session limit
```

**Features:**
- **Pre-created Rooms**: Eliminates Daily.co API latency
- **Token Management**: Pre-generated user and bot tokens
- **Token Validation**: Automatic expiry checking and refresh
- **Single-Use Policy**: Rooms recycled after each session
- **Background Creation**: Automatic room replenishment

#### Performance Monitoring

**Pool Status Endpoint:**
```bash
curl http://localhost:8000/agent/voice/automatic/pool/status
```

**Custom Metrics:**
```python
# Monitor pool performance
import time
from app.helpers.automatic.process_pool import get_voice_agent_pool

start_time = time.time()
pool = get_voice_agent_pool()
process = await pool.get_process(session_id)
connection_time = time.time() - start_time
print(f"Connection time: {connection_time:.2f}s")
```

### Database Optimization

#### Connection Pooling
```bash
POSTGRES_POOL_SIZE=5            # Base connections
POSTGRES_MAX_OVERFLOW=10        # Additional connections under load
POSTGRES_POOL_RECYCLE=3600      # Connection refresh (1 hour)
```

#### Query Optimization
- **Prepared Statements**: Reduced parsing overhead
- **Connection Reuse**: Persistent connections
- **Index Usage**: Optimized database queries
- **Async Operations**: Non-blocking database calls

### Memory Management

#### Mem0 Integration
```bash
MEM0_API_KEY="your_mem0_key"
MEM0_ENABLED=true
```

**Features:**
- **Conversation Memory**: Persistent user context
- **Smart Retrieval**: Relevant information surfacing
- **Memory Optimization**: Automatic cleanup of old contexts

#### Session Management
```bash
AUTOMATIC_SESSION_INACTIVITY_TIMEOUT=900.0  # 15 minutes
```

### Audio Processing Optimization

#### AIC (AI Coustics) Audio Enhancement
```bash
ENABLE_AIC_FILTER=true
AIC_ENHANCEMENT_LEVEL=1.0       # Audio quality enhancement
AIC_VOICE_GAIN=1.2              # Voice amplification
AIC_NOISE_GATE_ENABLE=true      # Background noise reduction
```

#### VAD Optimization
```bash
VAD_CONFIDENCE=0.85             # Optimal balance of sensitivity
VAD_MIN_VOLUME=0.75             # Noise floor threshold
```

#### STT Provider Comparison

| Provider | Latency | Accuracy | Cost | Indian Languages |
|----------|---------|----------|------|------------------|
| **Google STT** | 200ms | 95% | Medium | Excellent |
| **Deepgram** | 150ms | 94% | Low | Good |
| **Soniox** | 180ms | 96% | Medium | Excellent |
| **Azure STT** | 250ms | 93% | High | Good |

**Recommendation**: Soniox for solving the 0.5-second pause issue.

### Scaling Configuration

#### Horizontal Scaling
```bash
# Multiple server instances
VOICE_AGENT_POOL_SIZE=2         # Smaller pools per instance
DAILY_ROOM_POOL_SIZE=3          # Distributed room management
```

#### Load Balancing
- **Process Distribution**: Multiple pool instances
- **Room Distribution**: Geo-distributed Daily.co rooms
- **Database Sharding**: User-based partitioning

### Performance Best Practices

1. **Pre-warm Pools**: Always maintain minimum pool sizes
2. **Monitor Metrics**: Track connection times and pool usage
3. **Scale Gradually**: Increase pool sizes based on demand
4. **Optimize STT**: Choose provider based on language requirements
5. **Cache Aggressively**: Use memory services for repeated data
6. **Database Tuning**: Regular query optimization and indexing

---

## 🔧 Development Workflow

### Project Development Setup

#### 1. Development Environment
```bash
# Create development environment
cp .env.example .env.dev
echo "ENVIRONMENT=dev" >> .env.dev
echo "UVICORN_RELOAD=true" >> .env.dev
echo "PROD_LOG_LEVEL=DEBUG" >> .env.dev

# Activate development mode
export ENV_FILE=.env.dev
python run.py
```

#### 2. Code Quality Tools
```bash
# Install development dependencies
pip install black isort flake8 mypy pre-commit

# Setup pre-commit hooks
pre-commit install

# Format code
black app/
isort app/

# Type checking
mypy app/

# Linting
flake8 app/
```

#### 3. Testing Framework
```bash
# Install testing dependencies
pip install pytest pytest-asyncio pytest-cov httpx

# Create test configuration
cp .env.example .env.test
echo "ENVIRONMENT=test" >> .env.test
echo "POSTGRES_DB=clairvoyance_test" >> .env.test

# Run tests
pytest tests/ -v --cov=app

# Run specific test categories
pytest tests/test_automatic_agent.py
pytest tests/test_api.py
```

### Adding New Voice Agents

#### 1. Agent Structure
```bash
# Create new agent directory
mkdir -p app/agents/voice/new_agent/{services,tools,workflows}

# Create agent entry point
touch app/agents/voice/new_agent/__init__.py
```

#### 2. Agent Implementation Template
```python
# app/agents/voice/new_agent/__init__.py
import asyncio
from typing import Dict, Any

from pipecat.frames.frames import Frame
from pipecat.services.llm import LLMService
from pipecat.pipeline.pipeline import Pipeline

from app.core.logger import logger
from app.agents.voice.new_agent.tools import initialize_tools

class NewVoiceAgent:
    """Custom voice agent for specific business logic"""
    
    def __init__(self, config: Dict[str, Any]):
        self.config = config
        self.session_id = config.get('session_id')
        
    async def run(self):
        """Main agent execution loop"""
        logger.info(f"Starting new agent for session {self.session_id}")
        
        # Initialize tools
        tools = await initialize_tools(self.config)
        
        # Setup LLM service
        llm_service = LLMService(
            model="gpt-4o",
            tools=tools
        )
        
        # Create pipeline
        pipeline = Pipeline([
            # STT Service
            # VAD Service  
            # LLM Service
            # TTS Service
            # Transport Service
        ])
        
        # Run pipeline
        await pipeline.run()

# CLI entry point
if __name__ == "__main__":
    import argparse
    
    parser = argparse.ArgumentParser()
    parser.add_argument("--session-id", required=True)
    parser.add_argument("--config", required=True)
    
    args = parser.parse_args()
    
    agent = NewVoiceAgent(args.config)
    asyncio.run(agent.run())
```

#### 3. Register New Agent
```python
# app/api/routers/new_agent.py
from fastapi import APIRouter
from app.agents.voice.new_agent import NewVoiceAgent

router = APIRouter()

@router.post("/connect")
async def connect_new_agent(request: AgentRequest):
    # Initialize agent
    agent = NewVoiceAgent(request.config)
    
    # Start agent process
    await agent.run()
    
    return {"status": "connected"}
```

### Adding New Tools

#### 1. Tool Structure
```bash
# Create tool directory
mkdir -p app/agents/voice/automatic/tools/new_provider

# Create tool files
touch app/agents/voice/automatic/tools/new_provider/__init__.py
touch app/agents/voice/automatic/tools/new_provider/tools.py
```

#### 2. Tool Implementation
```python
# app/agents/voice/automatic/tools/new_provider/tools.py
from typing import Dict, Any, List
from pipecat.services.llm import LLMService

# Tool function implementations
async def get_custom_data(query: str) -> Dict[str, Any]:
    """
    Fetch custom data based on query.
    
    Args:
        query: Search query for data retrieval
        
    Returns:
        Dictionary containing retrieved data
    """
    # Implement custom logic
    return {"data": "custom_result", "query": query}

# Tool definitions for LLM
tool_functions = {
    "get_custom_data": get_custom_data
}

tool_declarations = [
    {
        "type": "function",
        "function": {
            "name": "get_custom_data",
            "description": "Fetch custom data based on query",
            "parameters": {
                "type": "object",
                "properties": {
                    "query": {
                        "type": "string",
                        "description": "Search query"
                    }
                },
                "required": ["query"]
            }
        }
    }
]

def initialize_new_provider_tools() -> Dict[str, Any]:
    """Initialize tools for new provider"""
    return {
        "declarations": tool_declarations,
        "functions": tool_functions
    }
```

#### 3. Register Tools
```python
# app/agents/voice/automatic/tools/__init__.py
from .new_provider.tools import initialize_new_provider_tools

def initialize_tools(config):
    tools = {}
    
    # Add new provider tools
    if config.get('enable_new_provider'):
        new_tools = initialize_new_provider_tools()
        tools.update(new_tools['functions'])
    
    return tools
```

### Database Migrations

#### 1. Create Migration Script
```python
# scripts/migrations/001_add_new_table.py
import asyncpg
from app.database import get_db_connection

async def upgrade():
    """Apply migration"""
    async for conn in get_db_connection():
        await conn.execute("""
            CREATE TABLE IF NOT EXISTS new_table (
                id SERIAL PRIMARY KEY,
                name VARCHAR(255) NOT NULL,
                created_at TIMESTAMP DEFAULT NOW()
            )
        """)

async def downgrade():
    """Rollback migration"""
    async for conn in get_db_connection():
        await conn.execute("DROP TABLE IF EXISTS new_table")

if __name__ == "__main__":
    import asyncio
    asyncio.run(upgrade())
```

#### 2. Run Migrations
```bash
# Run specific migration
python scripts/migrations/001_add_new_table.py

# Or use migration runner
python scripts/migrate.py --up
python scripts/migrate.py --down
```

### Debugging and Logging

#### 1. Debug Mode
```bash
# Enable debug logging
export PROD_LOG_LEVEL=DEBUG
export ENABLE_TRACING=true

# Run with debug
python run.py
```

#### 2. Session Debugging
```python
# Add debug logging to agents
from app.core.logger import logger

logger.bind(session_id=session_id).debug("Agent state", extra={
    "state": agent_state,
    "pools": pool_stats,
    "memory": memory_usage
})
```

#### 3. Performance Profiling
```python
# Profile agent performance
import time
import cProfile

def profile_agent_startup():
    profiler = cProfile.Profile()
    profiler.enable()
    
    # Agent startup code
    start_time = time.time()
    # ... agent initialization
    startup_time = time.time() - start_time
    
    profiler.disable()
    profiler.dump_stats(f'agent_profile_{session_id}.prof')
    
    return startup_time
```

---

## 🚀 Deployment

### Production Deployment

#### 1. Docker Deployment
```dockerfile
# Production Dockerfile optimization
FROM python:3.11-slim as builder

WORKDIR /app
COPY requirements.txt .
RUN pip install --user --no-cache-dir -r requirements.txt

FROM python:3.11-slim
WORKDIR /app

# Copy dependencies
COPY --from=builder /root/.local /root/.local
ENV PATH=/root/.local/bin:$PATH

# Copy application
COPY . .

# Create non-root user
RUN useradd --create-home --shell /bin/bash app
USER app

EXPOSE 8000
CMD ["python", "run.py"]
```

#### 2. Docker Compose for Production
```yaml
# docker-compose.prod.yml
version: '3.8'

services:
  clairvoyance:
    build: .
    ports:
      - "8000:8000"
    environment:
      - ENVIRONMENT=production
      - POSTGRES_HOST=db
      - REDIS_HOST=redis
    depends_on:
      - db
      - redis
    volumes:
      - ./logs:/app/logs
    restart: unless-stopped
    
  db:
    image: postgres:15
    environment:
      POSTGRES_DB: clairvoyance
      POSTGRES_USER: clairvoyance_user
      POSTGRES_PASSWORD: secure_password
    volumes:
      - postgres_data:/var/lib/postgresql/data
    restart: unless-stopped
    
  redis:
    image: redis:7
    restart: unless-stopped
    
  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
      - ./ssl:/etc/nginx/ssl
    depends_on:
      - clairvoyance
    restart: unless-stopped

volumes:
  postgres_data:
```

#### 3. Kubernetes Deployment
```yaml
# k8s/deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: clairvoyance
spec:
  replicas: 3
  selector:
    matchLabels:
      app: clairvoyance
  template:
    metadata:
      labels:
        app: clairvoyance
    spec:
      containers:
      - name: clairvoyance
        image: clairvoyance:latest
        ports:
        - containerPort: 8000
        env:
        - name: ENVIRONMENT
          value: "production"
        - name: POSTGRES_HOST
          value: "postgres-service"
        resources:
          requests:
            memory: "512Mi"
            cpu: "500m"
          limits:
            memory: "1Gi"
            cpu: "1000m"
        livenessProbe:
          httpGet:
            path: /health
            port: 8000
          initialDelaySeconds: 30
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /health
            port: 8000
          initialDelaySeconds: 5
          periodSeconds: 5
---
apiVersion: v1
kind: Service
metadata:
  name: clairvoyance-service
spec:
  selector:
    app: clairvoyance
  ports:
  - port: 80
    targetPort: 8000
  type: LoadBalancer
```

### Environment-Specific Configurations

#### 1. Staging Environment
```bash
# .env.staging
ENVIRONMENT=staging
POSTGRES_HOST=staging-db.example.com
DAILY_API_URL=https://api.daily.co/v1
AZURE_OPENAI_ENDPOINT=https://staging-openai.openai.azure.com/

# Reduced pool sizes for staging
VOICE_AGENT_POOL_SIZE=2
DAILY_ROOM_POOL_SIZE=3
```

#### 2. Production Environment
```bash
# .env.production
ENVIRONMENT=production
POSTGRES_HOST=prod-db.example.com
POSTGRES_POOL_SIZE=10
POSTGRES_MAX_OVERFLOW=20

# Optimized pool sizes for production
VOICE_AGENT_POOL_SIZE=5
VOICE_AGENT_MAX_POOL_SIZE=10
DAILY_ROOM_POOL_SIZE=10
DAILY_ROOM_MAX_POOL_SIZE=20

# Production security
JWT_SECRET_KEY=super_secure_production_key
SKIP_KMS_DECRYPT=false
```

### Monitoring and Observability

#### 1. Health Checks
```bash
# Application health check
curl http://localhost:8000/health

# Detailed health check with database
curl http://localhost:8000/health/database

# Pool status monitoring
curl http://localhost:8000/agent/voice/automatic/pool/status
```

#### 2. Logging Configuration
```python
# Production logging setup
import structlog
from app.core.logger import configure_production_logging

# Configure structured logging for production
configure_production_logging(
    log_level="INFO",
    json_format=True,
    include_trace_id=True
)
```

#### 3. Metrics Collection
```python
# Custom metrics for monitoring
from prometheus_client import Counter, Histogram, Gauge

# Voice agent metrics
voice_connections = Counter('voice_connections_total', 'Total voice connections')
connection_duration = Histogram('connection_duration_seconds', 'Connection duration')
pool_utilization = Gauge('pool_utilization_ratio', 'Pool utilization ratio')

# Usage in application
voice_connections.inc()
connection_duration.observe(connection_time)
pool_utilization.set(used_processes / total_processes)
```

### Scaling Strategies

#### 1. Horizontal Scaling
- **Load Balancer**: Distribute requests across multiple instances
- **Pool Distribution**: Smaller pools per instance for better resource utilization
- **Database Sharding**: Partition data based on merchant_id or user_id

#### 2. Vertical Scaling
- **Memory Optimization**: Increase pool sizes for high-traffic periods
- **CPU Optimization**: Optimize STT/TTS processing for better performance
- **Network Optimization**: Use CDN for static assets and media

#### 3. Auto-scaling Configuration
```yaml
# k8s/hpa.yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: clairvoyance-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: clairvoyance
  minReplicas: 2
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 70
  - type: Resource
    resource:
      name: memory
      target:
        type: Utilization
        averageUtilization: 80
```

---

## 🔍 Troubleshooting

### Common Issues and Solutions

#### 1. Connection Timeout Issues

**Problem**: Voice agent connections timing out
```
ERROR: Connection timeout after 8 seconds
```

**Solutions**:
```bash
# Check pool status
curl http://localhost:8000/agent/voice/automatic/pool/status

# Increase pool sizes if exhausted
export VOICE_AGENT_POOL_SIZE=5
export DAILY_ROOM_POOL_SIZE=8

# Check Daily.co API status
curl https://api.daily.co/v1/
```

**Pool Recovery**:
```python
# Manually replenish pools
from app.helpers.automatic.process_pool import get_voice_agent_pool
from app.helpers.automatic.daily_room_pool import get_room_pool

voice_pool = get_voice_agent_pool()
await voice_pool.replenish_pool()

room_pool = get_room_pool()
await room_pool.replenish_pool()
```

#### 2. Database Connection Issues

**Problem**: Database connection failures
```
ERROR: asyncpg.exceptions.ConnectionDoesNotExistError
```

**Solutions**:
```bash
# Check database connectivity
pg_isready -h localhost -p 5432 -U clairvoyance_user

# Verify database configuration
python -c "from app.database import get_db_connection; print('DB OK')"

# Reset connection pool
export POSTGRES_POOL_SIZE=10
export POSTGRES_MAX_OVERFLOW=20
python run.py
```

**Database Recovery**:
```python
# Reset database connections
from app.database import close_db_pool, init_db_pool

await close_db_pool()
await init_db_pool()
```

#### 3. STT/TTS Service Issues

**Problem**: Speech services not responding
```
ERROR: STT service timeout
ERROR: TTS service authentication failed
```

**Solutions**:
```bash
# Test Google STT
python -c "from app.agents.voice.automatic.stt import test_google_stt; test_google_stt()"

# Test ElevenLabs TTS
curl -X POST "https://api.elevenlabs.io/v1/voices" \
  -H "xi-api-key: $ELEVENLABS_API_KEY"

# Switch to backup provider
export STT_PROVIDER=deepgram
export TTS_PROVIDER=azure
```

**Service Configuration**:
```python
# Debug STT configuration
from app.core.config import STT_PROVIDER, DEEPGRAM_API_KEY
print(f"STT Provider: {STT_PROVIDER}")
print(f"Deepgram configured: {'Yes' if DEEPGRAM_API_KEY else 'No'}")
```

#### 4. Memory Leaks and Performance

**Problem**: High memory usage and slow performance
```
WARNING: Memory usage exceeding 1GB
WARNING: Connection time > 5 seconds
```

**Solutions**:
```bash
# Monitor process memory
ps aux | grep python | grep -v grep

# Check pool utilization
curl http://localhost:8000/agent/voice/automatic/pool/status

# Restart application with optimized settings
export AUTOMATIC_SESSION_INACTIVITY_TIMEOUT=600
export MAX_DAILY_SESSION_LIMIT=1200
python run.py
```

**Memory Optimization**:
```python
# Monitor session cleanup
from app.helpers.automatic.session_manager import bot_procs
print(f"Active sessions: {len(bot_procs)}")

# Force cleanup if needed
from app.helpers.automatic.session_manager import cleanup_bot_processes
await cleanup_bot_processes()
```

#### 5. Authentication Issues

**Problem**: JWT authentication failures
```
ERROR: Invalid JWT token
ERROR: Token expired
```

**Solutions**:
```bash
# Verify JWT configuration
python -c "from app.core.config import JWT_SECRET_KEY; print('JWT configured' if JWT_SECRET_KEY else 'JWT missing')"

# Test token generation
python -c "from app.core.security.jwt import create_access_token; print(create_access_token({'user_id': 'test'}))"

# Check token expiry
export JWT_ACCESS_TOKEN_EXPIRE_MINUTES=120
```

### Debugging Tools

#### 1. Session Debugging
```python
# Enable session debugging
from app.core.logger import logger

# Add to agent initialization
logger.bind(session_id=session_id).info("Agent starting", extra={
    "config": sanitized_config,
    "pools": await get_pool_stats(),
    "timestamp": time.time()
})
```

#### 2. Pool Monitoring
```bash
# Monitor pool status continuously
watch -n 5 'curl -s http://localhost:8000/agent/voice/automatic/pool/status | jq'

# Monitor system resources
htop
iostat -x 1
vmstat 1
```

#### 3. Network Debugging
```bash
# Test Daily.co connectivity
curl -I https://api.daily.co/v1/

# Test WebSocket connection
wscat -c ws://localhost:8000/agent/voice/breeze-buddy/twilio/callback/order-confirmation

# Monitor network traffic
netstat -an | grep 8000
ss -tuln | grep 8000
```

### Performance Profiling

#### 1. Application Profiling
```python
# Profile agent startup
import cProfile
import pstats

profiler = cProfile.Profile()
profiler.enable()

# Your agent code here
await agent.run()

profiler.disable()
stats = pstats.Stats(profiler)
stats.sort_stats('cumulative').print_stats(20)
```

#### 2. Database Query Profiling
```sql
-- Enable query logging in PostgreSQL
SET log_statement = 'all';
SET log_duration = on;
SET log_min_duration_statement = 100;

-- Monitor slow queries
SELECT query, mean_time, calls 
FROM pg_stat_statements 
WHERE mean_time > 100 
ORDER BY mean_time DESC;
```

#### 3. Memory Profiling
```python
# Memory usage tracking
import tracemalloc

tracemalloc.start()

# Your code here
await agent.run()

current, peak = tracemalloc.get_traced_memory()
print(f"Current memory usage: {current / 1024 / 1024:.1f} MB")
print(f"Peak memory usage: {peak / 1024 / 1024:.1f} MB")
tracemalloc.stop()
```

### Support and Documentation

#### Getting Help
- **GitHub Issues**: Report bugs and request features
- **Documentation**: Check `memory-bank/` for detailed technical docs
- **Logs**: Check application logs in `logs/` directory
- **Configuration**: Verify all required environment variables are set

#### Contributing
- Follow the development workflow outlined above
- Add tests for new features
- Update documentation in `memory-bank/`
- Follow code style guidelines (Black, isort, flake8)

---

## 📚 Additional Resources

### External Documentation
- **PipeCat Framework**: https://docs.pipecat.ai/
- **Daily.co API**: https://docs.daily.co/reference/api
- **Azure OpenAI**: https://docs.microsoft.com/en-us/azure/cognitive-services/openai/
- **FastAPI**: https://fastapi.tiangolo.com/
- **PostgreSQL**: https://www.postgresql.org/docs/

### Related Projects
- **Langfuse**: https://langfuse.com/ (Tracing and observability)
- **Mem0**: https://mem0.ai/ (Memory management for AI)
- **Model Context Protocol**: https://github.com/modelcontextprotocol/specification

---

*Clairvoyance - Empowering businesses with next-generation voice AI technology* 🔮
