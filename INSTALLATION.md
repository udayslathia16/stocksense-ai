# 📥 Installation Guide

## System Requirements

- **Python**: 3.8 or higher
- **RAM**: Minimum 4GB
- **Disk Space**: 500MB free space
- **Internet**: Required for API calls

---

## Step-by-Step Installation

### 1. Install Python

#### Windows
1. Download Python from [python.org](https://www.python.org/downloads/)
2. Run installer
3. ✅ **Check "Add Python to PATH"**
4. Click "Install Now"
5. Verify installation:
```cmd
python --version
```

#### macOS
```bash
# Using Homebrew
brew install python3

# Verify
python3 --version
```

#### Linux (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install python3 python3-pip python3-venv

# Verify
python3 --version
```

---

### 2. Clone Repository
```bash
# Using HTTPS
git clone https://github.com/yourusername/stock-analysis-ai.git

# OR using SSH
git clone git@github.com:yourusername/stock-analysis-ai.git

# Navigate to directory
cd stock-analysis-ai
```

---

### 3. Create Virtual Environment

#### Windows
```cmd
python -m venv venv
venv\Scripts\activate
```

#### macOS/Linux
```bash
python3 -m venv venv
source venv/bin/activate
```

You should see `(venv)` prefix in your terminal.

---

### 4. Install Dependencies
```bash
# Upgrade pip
pip install --upgrade pip

# Install requirements
pip install -r requirements.txt
```

**Installation time**: ~2-3 minutes

---

### 5. Configure Environment Variables
```bash
# Copy example file
cp .env.example .env

# Edit with your favorite editor
# Windows:
notepad .env

# macOS:
nano .env

# Linux:
nano .env
```

Add your API keys:
```env
ANTHROPIC_API_KEY=sk-ant-xxxxx
OPENAI_API_KEY=sk-xxxxx
GEMINI_API_KEY=xxxxx
ALPHA_VANTAGE_KEY=xxxxx
```

---

### 6. Verify Installation
```bash
# Test Python imports
python -c "import gradio; print('Gradio OK')"
python -c "import anthropic; print('Anthropic OK')"
python -c "import openai; print('OpenAI OK')"
python -c "from nsepython import nse_eq; print('NSEPython OK')"
```

All should print "OK" without errors.

---

### 7. Run Application
```bash
python main.py
```

Expected output:
```
Running on local URL:  http://127.0.0.1:7860
Running on public URL: https://xxxxx.gradio.live

To create a public link, set `share=True` in `launch()`.
```

Open browser and go to: `http://localhost:7860`

---

## Troubleshooting Installation

### Issue: "python: command not found"
**Solution**: Use `python3` instead of `python`

### Issue: "pip: command not found"
**Solution**: 
```bash
python -m ensurepip --upgrade
```

### Issue: "Permission denied"
**Solution** (Linux/macOS):
```bash
sudo pip install -r requirements.txt
```

### Issue: SSL Certificate Error
**Solution**:
```bash
pip install --trusted-host pypi.org --trusted-host files.pythonhosted.org -r requirements.txt
```

### Issue: Module not found after installation
**Solution**:
```bash
# Deactivate and reactivate virtual environment
deactivate
source venv/bin/activate  # or venv\Scripts\activate on Windows

# Reinstall
pip install -r requirements.txt
```

---

## Updating the Application
```bash
# Pull latest changes
git pull origin main

# Update dependencies
pip install --upgrade -r requirements.txt

# Restart application
python main.py
```

---

## Uninstallation
```bash
# Deactivate virtual environment
deactivate

# Remove directory
cd ..
rm -rf stock-analysis-ai  # Linux/macOS
# or
rmdir /s stock-analysis-ai  # Windows
```