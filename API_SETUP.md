# 🔑 API Keys Setup Guide

## Overview

This application requires API keys from multiple providers:
- **Alpha Vantage**: US stock market data (Required for US stocks)
- **Anthropic/OpenAI/Gemini**: AI analysis (At least one required)

---

## 1. Alpha Vantage API Key

### Get Free API Key

1. Visit [Alpha Vantage](https://www.alphavantage.co/support/#api-key)
2. Fill in your details:
   - First Name
   - Last Name
   - Email
   - Organization (optional)
3. Click "GET FREE API KEY"
4. Copy the API key (format: `XXXXXXXXXXXXXX`)

### Add to .env file
```env
ALPHA_VANTAGE_KEY=your_key_here
```

### Rate Limits (Free Tier)
- 5 API calls per minute
- 500 API calls per day

### Premium Plans
| Plan | Calls/Min | Calls/Day | Price |
|------|-----------|-----------|-------|
| Free | 5 | 500 | $0 |
| Basic | 30 | 7500 | $50/month |
| Premium | 120 | 30000 | $150/month |

---

## 2. Anthropic Claude API Key

### Get API Key

1. Visit [Anthropic Console](https://console.anthropic.com/)
2. Sign up / Log in
3. Go to "API Keys" section
4. Click "Create Key"
5. Copy the key (format: `sk-ant-xxxxx`)

### Add to .env file
```env
ANTHROPIC_API_KEY=sk-ant-xxxxx
```

### Pricing (Claude Sonnet 4.5)
- Input: $3 per million tokens
- Output: $15 per million tokens
- Free tier: $5 credit for new users

---

## 3. OpenAI API Key

### Get API Key

1. Visit [OpenAI Platform](https://platform.openai.com/)
2. Sign up / Log in
3. Go to [API Keys](https://platform.openai.com/api-keys)
4. Click "Create new secret key"
5. Copy the key (format: `sk-xxxxx`)

### Add to .env file
```env
OPENAI_API_KEY=sk-xxxxx
```

### Pricing (GPT-4o)
- Input: $2.50 per million tokens
- Output: $10 per million tokens
- New users: $5 free credit (expires in 3 months)

---

## 4. Google Gemini API Key

### Get API Key

1. Visit [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Sign in with Google account
3. Click "Create API Key"
4. Copy the key

### Add to .env file
```env
GEMINI_API_KEY=xxxxx
```

### Pricing (Gemini Pro)
- **Free tier**: 60 requests per minute
- Paid tier: Custom pricing

---

## Complete .env Example
```env
# Alpha Vantage (Required for US stocks)
ALPHA_VANTAGE_KEY=DEMO

# Choose at least ONE AI provider:

# Anthropic Claude
ANTHROPIC_API_KEY=sk-ant-api03-xxxxx

# OpenAI GPT-4
OPENAI_API_KEY=sk-xxxxx

# Google Gemini
GEMINI_API_KEY=AIzaSyxxxxx
```

---

## Verification

### Test API Keys
```bash
# Run test script
python test_apis.py
```

Expected output:
```
✅ Alpha Vantage: Working
✅ Anthropic: Working
✅ OpenAI: Working
✅ Gemini: Working
```

### Manual Testing

#### Alpha Vantage
```python
import requests
import os
from dotenv import load_dotenv

load_dotenv()
api_key = os.getenv("ALPHA_VANTAGE_KEY")

response = requests.get(
    f"https://www.alphavantage.co/query?function=GLOBAL_QUOTE&symbol=AAPL&apikey={api_key}"
)
print(response.json())
```

#### Anthropic
```python
import anthropic
import os
from dotenv import load_dotenv

load_dotenv()
client = anthropic.Anthropic(api_key=os.getenv("ANTHROPIC_API_KEY"))

message = client.messages.create(
    model="claude-sonnet-4-20250514",
    max_tokens=100,
    messages=[{"role": "user", "content": "Hello!"}]
)
print(message.content[0].text)
```

---

## Security Best Practices

### ✅ DO:
- Store keys in `.env` file
- Add `.env` to `.gitignore`
- Use environment variables
- Rotate keys regularly
- Use different keys for dev/prod

### ❌ DON'T:
- Commit `.env` to Git
- Share keys publicly
- Hardcode keys in code
- Use production keys in public repos
- Share API keys via email/chat

---

## Troubleshooting

### "Invalid API Key" Error

1. Check for extra spaces
2. Verify key is active
3. Check key permissions
4. Regenerate key if needed

### Rate Limit Exceeded

1. Wait 60 seconds
2. Upgrade to paid tier
3. Implement caching
4. Batch requests

### API Key Not Loading

1. Check `.env` file location (must be in root directory)
2. Verify no typos in variable names
3. Restart application after changes
4. Check `.env` file permissions

---

## Cost Management

### Estimate Monthly Costs

**Scenario**: 100 stock analyses per day

| Service | Usage | Est. Cost |
|---------|-------|-----------|
| Alpha Vantage | 100 calls/day | Free (within limits) |
| Claude | ~500K tokens | ~$10/month |
| GPT-4 | ~500K tokens | ~$15/month |
| Gemini | 100 requests/day | Free |

**Total**: $10-25/month (if using paid AI)

### Tips to Reduce Costs

1. Use free tier when possible
2. Cache results for popular stocks
3. Use Gemini (free tier) for testing
4. Implement request batching
5. Monitor usage dashboard

---

## Support

- Alpha Vantage: support@alphavantage.co
- Anthropic: support@anthropic.com
- OpenAI: help.openai.com
- Gemini: Google AI Studio support