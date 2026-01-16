# Multimodal Chat Telegram

Intelligent Telegram chatbot with artificial intelligence using n8n. This workflow implements an advanced AI-powered chatbot to manage automatic conversations on Telegram with multimodal capabilities.

## 📋 Description

This n8n workflow automates Telegram conversations with:

- **AI Agent**: Automatically responds to messages using OpenAI's GPT-4
- **Audio Processing**: Transcribes voice messages to text
- **Image Analysis**: Analyzes and describes images sent by users
- **Conversation Memory**: Maintains context from previous conversations using PostgreSQL
- **Intelligent Routing**: Directs messages based on their type (text, audio, image)
- **Email Integration**: Can send emails through Gmail when needed
- **Database Tools**: Access to customer and product database for intelligent recommendations

## 🚀 Features

- ✅ Automatic responses with AI (GPT-4)
- ✅ Voice message transcription to text
- ✅ Image analysis and description
- ✅ Conversation context management
- ✅ Integration with Telegram Bot API
- ✅ Integration with OpenAI for language processing
- ✅ Email sending capabilities
- ✅ PostgreSQL memory storage
- ✅ Multimodal message handling (text, audio, images)

## 📦 Requirements

- n8n account
- Telegram Bot Token
- OpenAI API credentials
- PostgreSQL database (for conversation memory)
- Gmail credentials (optional, for email functionality)

## 🔧 Installation

1. Access your n8n instance
2. Import the `workflow.json` file
3. Configure the necessary credentials:
   - Telegram Bot Token
   - OpenAI API Key
   - PostgreSQL connection string
   - Gmail credentials (optional)

## 📝 Configuration

### Environment Variables

```bash
TELEGRAM_BOT_TOKEN=your_bot_token_here
OPENAI_API_KEY=your_key_here
POSTGRES_CONNECTION_STRING=postgresql://user:password@host:port/database
GMAIL_CREDENTIALS=your_gmail_credentials
```

### Main Nodes

- **Telegram Trigger**: Receives messages from Telegram
- **Switch**: Routes based on message type (text, audio, image)
- **Transcribir Audio**: Converts voice messages to text
- **Explicar Imagen**: Analyzes images using GPT-4 Vision
- **Agente de IA**: AI agent that processes and responds to messages
- **Memoria**: Stores conversation history in PostgreSQL
- **Cerebro**: GPT-4 language model for intelligent responses
- **Enviar Mensaje**: Sends responses back to Telegram

## 🎯 Use Cases

- **Dog Breeding Sales**: Automated customer service for puppy sales (AmorCanino example)
- **Customer Support**: Automatic support with context awareness
- **Sales Assistant**: Product recommendations and inquiries
- **Information Bot**: Answer questions with image and audio support
- **Lead Generation**: Collect customer data and schedule appointments

## 🔐 Security Notes

- Never commit API keys or tokens to version control
- Use n8n's credential management system
- Store sensitive data in environment variables
- Ensure PostgreSQL connection is secure

## 📞 Support

For more information about n8n, visit: https://n8n.io/docs/

For Telegram Bot API documentation: https://core.telegram.org/bots/api

For OpenAI documentation: https://platform.openai.com/docs/

## 📄 License

This project is available under an open license.

## 👤 Author

Created by: Yesid Fernando Cepeda B.

---

**Last updated**: 2026-01-16
