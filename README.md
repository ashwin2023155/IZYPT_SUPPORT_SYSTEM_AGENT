# IZYPT Chatbot Backend & Voice Agent

A comprehensive AI-powered customer support and sales agent for IZYPT, featuring multi-turn conversation capabilities, database integration, and voice support via Twilio.

##  Key Features

- **Google Gemini Integration**: Uses `gemini-2.5-flash` for high-quality, fast, and accurate responses.
- **Database Integration**: Real-time lookup of orders, customer details, and status updates.
- **Voice Agent**: Full duplex voice support via Twilio (Speech-to-Text and Text-to-Speech).
- **FastAPI Backend**: Robust REST API handling chat sessions, history, and webhooks.
- **Context Awareness**: Remembers conversation history for natural multi-turn dialogue.

## 🛠️ Tech Stack

- **AI Model**: Google Gemini API (`gemini-2.5-flash`)
- **Backend Framework**: FastAPI + Uvicorn
- **Database**: SQLite
- **Voice Integration**: Twilio Programmable Voice
- **Language**: Python 3.9+

##  Project Structure

```
IZYPT/
├── api.py                   # Main FastAPI application entry point
├── agent.py                 # Core agent logic and orchestration
├── gemini_agent.py          # Gemini API integration wrapper
├── database_tools.py        # SQLite database query functions
├── conversation_manager.py  # Session and history management
├── twilio_handler.py        # Twilio TwiML generation and webhook handlers
├── config.py                # Configuration settings and API keys
├── requirement.txt          # Python dependencies
└── IZYPT_DB/
    └── orders_database.db   # Order and customer database
```

## ⚙️ Configuration (`config.py`)

- **USE_GEMINI_API**: `True` (Recommended)
- **GEMINI_API_KEY**: Your Google Gemini API key
- **TWILIO_**: Credentials for voice integration
- **Prompts**: System prompts for Voice, Support, and Sales modes

## 🏃‍♂️ How to Run

### 1. Install Dependencies
```bash
pip install -r requirement.txt
```

### 2. Set Up Environment
Ensure you have your API keys set in `config.py` or environment variables:
- `GEMINI_API_KEY`
- `TWILIO_ACCOUNT_SID`
- `TWILIO_AUTH_TOKEN`

### 3. Start the Server
```bash
uvicorn api:app --host 0.0.0.0 --port 8000 --reload
```

##  Voice Agent Setup

To enable the phone number **(484) 559-7215**:

1. **Start ngrok**: `ngrok http 8000`
2. **Update Twilio Webhook**: Set Voice Webhook to `https://YOUR-NGROK-URL/twilio/voice`
3. **Call the number**: The agent will answer and look up orders in real-time.

## 🧪 Testing

- **Quick Text Test**: `python quick_test.py`
- **Gemini Test**: `python test_gemini.py`
- **API Docs**: Visit `http://localhost:8000/docs`

##  Database Schema

**Orders Table**:
- `order_id`: Unique identifier (e.g., #ORD-123)
- `phone`: Customer phone number
- `status`: Order status (DELIVERED, CANCELLED, etc.)
- `amount`: Order total
- `items`: List of items ordered

The agent automatically extracts phone numbers and order IDs from conversation to query this data.
