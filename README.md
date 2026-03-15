# AtlasLink - A customer care voice agent

## AI Voice Agent for Telephone Support

This guide outlines how to build a production-ready AI Calling Agent that answers real customer support calls 24/7 using Python and VideoSDK's AI Phone Agent with SIP Telephony. Unlike browser-based bots, this agent connects directly to the telephone network (PSTN).

## 🚀 Quick Start Guide

- **Prerequisites**: Install Python, sign up for a VideoSDK account, and get a Google Gemini API Key.
- **Environment Setup**: Create a `main.py`, `requirements.txt`, and `.env` file. Add your keys to `.env`.
- **Install Dependencies**: Run `pip install -r requirements.txt` (see documentation for required libraries like `videosdk-agents` and `google-generativeai`).
- **Register the Agent**: Run your Python script to register the agent with VideoSDK
- **Telephony Integration**: Purchase a number on Twilio (11:00) and configure the SIP Trunking to route calls to VideoSDK 
- **Create Routing Rules**: Configure inbound/outbound rules in the VideoSDK dashboard to map your Twilio number to your agent

## 🛠️ Architecture Overview

The system uses the SIP Protocol (Session Initiation Protocol) to bridge telephony networks with the AI brain.

```
User Call → SIP Provider (Twilio) → VideoSDK Cloud (Processes Agent Logic) → AI Response (via Google Gemini) → Voice Synthesis → User
```

## Implementation Overview

This voice agent is built using **VideoSDK Agents** framework, which provides a robust infrastructure for handling real-time voice interactions. The implementation includes:

- **Custom Agent Class**: A `MyVoiceAgent` class that extends VideoSDK's `Agent` base class, configured with friendly instructions for customer care interactions. It includes greeting and farewell messages that are automatically played when calls start and end.

- **Google Gemini Realtime Integration**: Uses Google's Gemini 2.5 Flash model with native audio support for real-time voice processing. The agent is configured with the "Leda" voice and audio-only response modality.

- **Real-Time Pipeline**: Sets up a `RealTimePipeline` that connects the Gemini model to VideoSDK's session management, enabling seamless bidirectional audio communication.

- **Telephony Registration**: The agent registers with VideoSDK's telephony service using a unique agent ID (`MyTelephonyAgent`), allowing it to handle up to 10 concurrent phone calls on `localhost:8081`.

- **Session Management**: Each call creates a new `AgentSession` that manages the lifecycle of the conversation, from connection to graceful shutdown.
