# 🔧 Troubleshooting Guide

## Common Issues & Solutions

---

## 1. Installation Issues

### Issue: "ModuleNotFoundError: No module named 'gradio'"

**Cause**: Dependencies not installed

**Solution**:
```bash
# Make sure virtual environment is activated
source venv/bin/activate  # Linux/macOS
# or
venv\Scripts\activate  # Windows

# Reinstall requirements
pip install -r requirements.txt
```

---

### Issue: "Python version not supported"

**Cause**: Python version < 3.8

**Solution**:
```bash
# Check Python version
python --version

# Install Python 3.8+
# Download from python.org
```

---

## 2. API Issues

### Issue: "Insufficient data" for US stocks

**Cause**: Alpha Vantage timeout or invalid response

**Solution**:
```python
# In main.py, increase timeout:
# Find: timeout=30
# Change to: timeout=60
```

**Alternative**: Check API key is valid:
```bash
# Test manually
curl "https://www.alphavantage.co/query?function=GLOBAL_QUOTE&symbol=AAPL&apikey=YOUR_KEY"
```

---

### Issue: "Insufficient data" for Indian stocks (NORMAL)

**Cause**: NSE API doesn't provide historical data

**Solution**: This is expected behavior
- ✅ US stocks: Full indicators
- ⚠️ Indian stocks: Limited to current data

**To get full indicators for Indian stocks**: Use Yahoo Finance (requires code modification)

---

### Issue: "ReadTimeout" for Alpha Vantage

**Cause**: Network issues or slow API response

**Solutions**:
1. Increase timeout in `get_stock_history`:
```python
response = requests.get(ALPHA_VANTAGE_API, params=params, timeout=60)  # Increase from 30
```

2. Check network connection
3. Try VPN if geo-blocked
4. Wait and retry

---

### Issue: "Rate limit exceeded"

**Cause**: Too many API calls

**Solution**:
```
Alpha Vantage: Wait 1 minute (5 calls/min limit)
OpenAI/Claude: Check your plan limits
```

**Prevention**:
- Cache results
- Implement request queuing
- Upgrade to paid tier

---

## 3. Data Issues

### Issue: "Cannot fetch data for symbol"

**Cause**: Invalid stock symbol

**Solution**:
- ✅ Indian stocks: Use symbol without .NS/.BO (e.g., `TCS`, not `TCS.NS`)
- ✅ US stocks: Use correct ticker (e.g., `AAPL`, `MSFT`)

**Verify symbol**:
- NSE: Check on [nseindia.com](https://www.nseindia.com/)
- US: Check on [finance.yahoo.com](https://finance.yahoo.com/)

---

### Issue: Stock data outdated

**Cause**: Market closed or delayed data

**Solution**: 
- Indian market hours: 9:15 AM - 3:30 PM IST (Mon-Fri)
- US market hours: 9:30 AM - 4:00 PM EST (Mon-Fri)
- Data updates during market hours only

---

## 4. UI Issues

### Issue: Gradio interface not loading

**Cause**: Port 7860 already in use

**Solution**:
```python
# In main.py, change port:
app.launch(server_port=7861)  # or any other port
```

---

### Issue: Progress bar not showing

**Cause**: Old Gradio version

**Solution**:
```bash
pip install --upgrade gradio
```

---

### Issue: Markdown not rendering

**Cause**: Using gr.Textbox instead of gr.Markdown

**Solution**: Already fixed in latest code. Update your `main.py`.

---

## 5. AI Analysis Issues

### Issue: "Claude Analysis Error"

**Possible causes**:
1. Invalid API key
2. Insufficient credits
3. Rate limit exceeded
4. Model name incorrect

**Solutions**:
1. Verify API key in `.env`
2. Check account credits
3. Wait and retry
4. Verify model name: `claude-sonnet-4-20250514`

---

### Issue: "OpenAI Analysis Error"

**Solution**:
```python
# Check API key
import openai
openai.api_key = "your-key"
try:
    response = openai.ChatCompletion.create(...)
except Exception as e:
    print(e)  # See exact error
```

---

## 6. Performance Issues

### Issue: Analysis takes too long

**Cause**: Multiple API calls + AI processing

**Normal times**:
- US stocks: 15-30 seconds
- Indian stocks: 5-10 seconds

**If slower**:
1. Check internet speed
2. Reduce `outputsize` in Alpha Vantage call
3. Use faster AI model (Gemini)

---

### Issue: High memory usage

**Cause**: Large historical datasets

**Solution**:
```python
# In calculate_all_indicators, limit data:
sorted_dates = sorted(time_series.keys(), reverse=True)[:200]  # Only 200 days
```

---

## 7. Environment Issues

### Issue: .env file not loading

**Checklist**:
- ✅ File named exactly `.env` (not `env.txt` or `.env.txt`)
- ✅ Located in root directory (same as `main.py`)
- ✅ No spaces in variable names
- ✅ Format: `KEY=value` (no quotes needed)

**Test loading**:
```python
from dotenv import load_dotenv
import os

load_dotenv()
print(os.getenv("ALPHA_VANTAGE_KEY"))  # Should print your key
```

---

## 8. Network Issues

### Issue: "Connection refused"

**Solutions**:
1. Check firewall settings
2. Disable VPN temporarily
3. Check proxy settings
4. Try different network

---

### Issue: SSL Certificate Error

**Solution**:
```python
# Temporary fix (not recommended for production):
import requests
requests.packages.urllib3.disable_warnings()

response = requests.get(url, verify=False)
```

---

## 9. Code-Specific Issues

### Issue: "KeyError: 'Time Series (Daily)'"

**Cause**: API response format changed

**Debug**:
```python
# Add debugging:
print(f"Response keys: {data.keys()}")
print(f"Full response: {data}")
```

**Solution**: Already handled in updated code with better error checking.

---

### Issue: Division by zero in indicators

**Cause**: Insufficient price data

**Solution**: Already handled with None checks in indicator functions.