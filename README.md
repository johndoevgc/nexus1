# NexusAI — Multi-Agent Intelligence Platform

Production-ready multi-agent chatbot for Azure Static Web Apps.

## Features

- **10 AI Models**: Claude 3.5, GPT-4o, Gemini 1.5 Pro, Grok 2, Mistral Large, Llama 3.1 405B, Command R+, DeepSeek R1, Sonar Pro, Phi-4
- **M365 Graph API**: Full Microsoft 365 integration with OAuth2 (Mail, Calendar, Teams, OneDrive, SharePoint)
- **UAT Test Suite**: 34 automated tests across 5 categories with pass/fail/warn reporting
- **Multi-Agent**: Unlimited agents with independent models, prompts, and chat histories
- **Azure SWA Ready**: Includes `staticwebapp.config.json` with security headers

## Azure Deployment

### Option 1 — Azure Portal
1. Go to https://portal.azure.com
2. Create → Static Web App
3. Connect to your GitHub/ADO repo containing these files
4. Set build preset: "Custom" with app_location: "/"

### Option 2 — Azure CLI
```bash
az login
az group create --name rg-nexusai --location eastus2
az staticwebapp create \
  --name nexusai-platform \
  --resource-group rg-nexusai \
  --location eastus2 \
  --source . \
  --branch main \
  --token $GITHUB_TOKEN
```

### Option 3 — GitHub Actions
The Azure portal auto-generates a GitHub Actions workflow when you link a repo.

## Configuration

All settings are stored in browser `localStorage`. No backend required.

### AI Models
Configure each model in **Settings → AI Models**:
- Azure OpenAI: resource name, deployment, API key, API version
- Anthropic Claude: API key, model ID
- Google Gemini: API key, project ID (optional)
- xAI Grok: API key
- Mistral: API key
- Meta Llama (Azure ML): endpoint URL, API key
- Cohere: API key
- DeepSeek: API key
- Perplexity: API key
- Microsoft Phi (Azure ML): endpoint URL, API key

### M365 Graph API
1. Register app in Microsoft Entra ID (https://entra.microsoft.com)
2. Add redirect URI matching your SWA URL
3. Copy Tenant ID, Client ID, create Client Secret
4. Configure in **Settings → M365 Graph API**
5. Toggle required permissions
6. Click **Authorize with Microsoft**

## Files
- `index.html` — Complete single-file application
- `staticwebapp.config.json` — Azure SWA routing + security headers
- `README.md` — This file

## Security Headers (included)
- `X-Frame-Options: SAMEORIGIN`
- `X-Content-Type-Options: nosniff`
- `Referrer-Policy: strict-origin-when-cross-origin`
- `Strict-Transport-Security: max-age=31536000`
- `Permissions-Policy: camera=(), microphone=(), geolocation=()`
