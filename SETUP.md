# Complete PrivateGPT Setup Guide with Ollama

This guide provides a complete step-by-step process to set up PrivateGPT with Ollama from a fresh git clone to running the application locally.

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Step 1: Clone Repository](#step-1-clone-repository)
3. [Step 2: Install System Dependencies](#step-2-install-system-dependencies)
4. [Step 3: Install Ollama](#step-3-install-ollama)
5. [Step 4: Install PrivateGPT Dependencies](#step-4-install-privategpt-dependencies)
6. [Step 5: Configure Environment](#step-5-configure-environment)
7. [Step 6: Start Ollama Service](#step-6-start-ollama-service)
8. [Step 7: Pull Required Models](#step-7-pull-required-models)
9. [Step 8: Run PrivateGPT](#step-8-run-privategpt)
10. [Step 9: Access the Application](#step-9-access-the-application)
11. [GPU Acceleration (Optional)](#gpu-acceleration-optional)
12. [Troubleshooting](#troubleshooting)
13. [Verification Checklist](#verification-checklist)

## Prerequisites

### System Requirements
- **Operating System**: Windows 10/11, macOS, or Linux
- **Python**: 3.11 or later
- **Git**: Latest version
- **Memory**: Minimum 8GB RAM (16GB recommended)
- **Storage**: At least 10GB free space
- **GPU**: Optional, but recommended for better performance

### Hardware Recommendations
- **CPU**: Multi-core processor (4+ cores recommended)
- **RAM**: 16GB or more for optimal performance
- **GPU**: NVIDIA GPU with CUDA support (optional but recommended)
- **Storage**: SSD for faster model loading

## Step 1: Clone Repository

```bash
# Clone the PrivateGPT repository
git clone https://github.com/zylon-ai/private-gpt.git

# Navigate to the project directory
cd private-gpt
```

## Step 2: Install System Dependencies

### Install Python 3.11+

**Windows:**
```powershell
# Download from https://www.python.org/downloads/
# Or use winget
winget install Python.Python.3.11
```

**macOS:**
```bash
# Using Homebrew
brew install python@3.11

# Or using pyenv
pyenv install 3.11
pyenv local 3.11
```

**Linux:**
```bash
# Ubuntu/Debian
sudo apt update
sudo apt install python3.11 python3.11-venv

# Or using pyenv
pyenv install 3.11
pyenv local 3.11
```

### Install Poetry

**All Platforms:**
```bash
# Install Poetry
curl -sSL https://install.python-poetry.org | python3 -

# Add Poetry to PATH (restart terminal after this)
export PATH="$HOME/.local/bin:$PATH"
```

**Windows PowerShell:**
```powershell
# Install Poetry
(Invoke-WebRequest -Uri https://install.python-poetry.org -UseBasicParsing).Content | python -

# Add to PATH
$env:PATH += ";$env:APPDATA\Python\Scripts"
```

### Install Make (Optional but Recommended)

**Windows:**
```powershell
# Using Chocolatey
choco install make

# Or using winget
winget install GnuWin32.Make
```

**macOS:**
```bash
brew install make
```

**Linux:**
```bash
# Ubuntu/Debian
sudo apt install make
```

## Step 3: Install Ollama

### Download and Install Ollama

**Windows:**
1. Go to [https://ollama.ai/download](https://ollama.ai/download)
2. Download the Windows installer
3. Run the installer and follow the prompts

**macOS:**
```bash
# Using Homebrew
brew install ollama

# Or download from https://ollama.ai/download
```

**Linux:**
```bash
# Install Ollama
curl -fsSL https://ollama.ai/install.sh | sh
```

### Verify Ollama Installation

```bash
# Check if Ollama is installed
ollama --version

# Should output something like: ollama version 0.1.29
```

## Step 4: Install PrivateGPT Dependencies

### Install Poetry Dependencies

```bash
# Install all required dependencies for Ollama setup
poetry install --extras "ui llms-ollama embeddings-ollama vector-stores-qdrant"
```

### Verify Installation

```bash
# Check if everything is installed correctly
poetry run python -c "import private_gpt; print('Installation successful!')"
```

## Step 5: Configure Environment

### Set Environment Variables

**Windows PowerShell:**
```powershell
# Set the profile to use Ollama
$env:PGPT_PROFILES="ollama"

```

**Windows Command Prompt:**
```cmd
set PORT=5002
```

**macOS/Linux:**
```bash
export PGPT_PROFILES="ollama"

```

## Step 6: Start Ollama Service

### Start Ollama in Background

```bash
# Start Ollama service (run this in a separate terminal and keep it running)
ollama serve
```

## Step 7: Pull Required Models

### Pull LLM Model

```bash
# Pull the LLM model (llama3.1 - about 4GB)
ollama pull llama3.1
```

### Pull Embedding Model

```bash
# Pull the embedding model (nomic-embed-text - about 275MB)
ollama pull nomic-embed-text
```

### Verify Models are Available

```bash
# List available models
ollama list

# Should show both llama3.1 and nomic-embed-text
```

## Step 8: Run PrivateGPT

### Start the Application

```bash
# Run PrivateGPT with Ollama
make run
```

### Verify Application is Running

You should see output similar to:

## Step 9: Access the Application

### Web Interface

- **Main URL**: `http://localhost:8001/`
- **API Documentation**: `http://localhost:8001/docs`
- **Health Check**: `http://localhost:8001/health`

### Test the Application

1. Open your browser and go to `http://localhost:8001/`
2. You should see the PrivateGPT Gradio interface
3. Try uploading a document (PDF, TXT, DOCX, etc.)
4. Ask a question about the uploaded document