# Setup Guide - Multimodal Chat Telegram

## Step 1: Prepare Credentials

### Telegram Bot Token
1. Open Telegram and search for **@BotFather**
2. Send `/newbot` command
3. Follow the instructions to create your bot
4. Copy the bot token provided

### OpenAI API
1. Go to https://platform.openai.com/api-keys
2. Create a new API key
3. Copy the key (you'll need it in n8n)

### PostgreSQL (Optional but Recommended)
For conversation memory and context:
1. Set up a PostgreSQL database
2. Create a table named `conversaciones` with the following structure:
```sql
CREATE TABLE conversaciones (
  id SERIAL PRIMARY KEY,
  session_id VARCHAR(255),
  message TEXT,
  response TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
3. Get your connection string: `postgresql://user:password@host:port/database`

### Gmail (Optional)
If you want email functionality:
1. Enable Gmail API in Google Cloud Console
2. Create OAuth 2.0 credentials
3. Download the credentials JSON file

## Step 2: Import Workflow in n8n

1. Open your n8n instance
2. Go to "Workflows" → "Import"
3. Upload the `workflow.json` file
4. Click "Import"

## Step 3: Configure Credentials in n8n

### Telegram Bot Credentials
1. Find the "Telegram Trigger" node
2. Click on it and go to the credentials section
3. Select "Create New" → "Telegram"
4. Paste your bot token
5. Save

### OpenAI Credentials
1. Find nodes that use OpenAI (Transcribir Audio, Agente de IA, etc.)
2. For each node:
   - Click on the node
   - Go to credentials section
   - Select "Create New" → "OpenAI"
   - Paste your API key
   - Save

### PostgreSQL Credentials (Optional)
1. Find the "Memoria" node
2. Click on it
3. Go to credentials section
4. Select "Create New" → "PostgreSQL"
5. Enter your connection details:
   - Host
   - Port (default: 5432)
   - Database name
   - Username
   - Password
6. Save

### Gmail Credentials (Optional)
1. Find the "Gmail" node
2. Click on it
3. Go to credentials section
4. Select "Create New" → "Gmail"
5. Follow OAuth authentication
6. Save

## Step 4: Configure Telegram Webhook

1. In the "Telegram Trigger" node, copy the webhook URL
2. Use this command to set the webhook in Telegram:
```bash
curl -X POST https://api.telegram.org/bot<YOUR_BOT_TOKEN>/setWebhook \
  -H 'Content-Type: application/json' \
  -d '{"url":"<YOUR_WEBHOOK_URL>"}'
```

Replace:
- `<YOUR_BOT_TOKEN>` with your Telegram bot token
- `<YOUR_WEBHOOK_URL>` with the webhook URL from n8n

## Step 5: Test the Workflow

1. Activate the workflow (toggle "Active" in the top right)
2. Send a message to your Telegram bot
3. Check if you receive an automatic response
4. Review the "Executions" tab for any errors

## Step 6: Customize AI Behavior

### Modify the AI Agent Prompt

1. Open the "Agente de IA" node
2. Edit the "System Message" field
3. Customize the AI's behavior, tone, and instructions
4. Save changes

### Example: Change from Dog Breeding to Customer Support

Replace the system message with:
```
You are a customer support assistant. Your role is to:
1. Answer customer questions professionally
2. Help resolve issues
3. Provide product information
4. Escalate complex issues when needed

Always be polite, helpful, and maintain conversation context.
```

## Troubleshooting

### Webhook Not Receiving Messages
- Verify the webhook URL is correct
- Check that the workflow is active
- Review Telegram Bot API logs
- Ensure n8n is accessible from the internet

### No AI Responses
- Verify OpenAI API key is valid
- Check that you have available credits
- Review execution logs for errors
- Ensure the system message is properly configured

### Audio Transcription Fails
- Verify the audio file format is supported
- Check OpenAI API quota
- Ensure the audio is clear and not too long
- Review error messages in executions

### Image Analysis Not Working
- Verify the image format is supported (JPG, PNG, etc.)
- Check image size (should be reasonable)
- Ensure OpenAI API supports vision models
- Review error messages in executions

### PostgreSQL Connection Issues
- Verify connection string is correct
- Check database is running and accessible
- Ensure firewall allows connection
- Verify table exists with correct schema

## Advanced Configuration

### Add Custom Tools

You can add more tools to the AI agent by:
1. Adding new nodes (e.g., database queries, API calls)
2. Connecting them as tools to the "Agente de IA" node
3. Updating the system message to explain the new tools

### Enable Logging

For debugging:
1. Add a "Log" node after key steps
2. Configure what data to log
3. Review logs in the "Executions" tab

### Rate Limiting

To prevent abuse:
1. Add a "Rate Limit" node after the trigger
2. Configure limits per user/chat
3. Handle exceeded limits appropriately

## Resources

- [n8n Documentation](https://n8n.io/docs/)
- [Telegram Bot API](https://core.telegram.org/bots/api)
- [OpenAI API Reference](https://platform.openai.com/docs/api-reference)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)

---

Need help? Check the workflow execution logs for detailed error messages.
