# NoMoreOnCall

> AI agents that replace human on-call engineers. Analyze errors, identify root causes, and generate code fixes automatically.

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

## Overview

NoMoreOnCall is an automated error analysis and debugging system that helps developers quickly identify and fix application errors. It combines error tracing, code context analysis, and automated code fix suggestions—reducing mean-time-to-resolution (MTTR) for production incidents.

### Key Features

| Feature | Description |
|---------|-------------|
| **Error Analysis** | Analyzes errors and generates detailed JSON reports with root cause analysis |
| **Code Context** | Provides code-level context, blame information, and stack traces |
| **Automated Fixes** | Generates code change suggestions for 15+ error types |
| **Notification API** | Integrated API for error alerting and automation workflows |
| **Git Integration** | Creates fix branches, patches, and pull requests automatically |

---

## Quick Start

```bash
# 1. Clone and setup
git clone https://github.com/hanu-tayal/NoMoreOnCall.git
cd NoMoreOnCall
python -m venv .venv
.venv\Scripts\activate   # Windows
# source .venv/bin/activate  # macOS/Linux

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run the demo
python demo.py
```

The demo will analyze a sample database timeout error (ERR_123) and generate fix suggestions.

---

## Architecture

```
Error Occurs → Debug Analyzer → Code Context & Blame → Root Cause Analysis
                    ↓
              Issue JSON File
                    ↓
              Code Fixer → Suggested Changes → Patch/PR
```

See [ARCHITECTURE.md](ARCHITECTURE.md) for a detailed technical overview.

---

## Components

### 1. Debug Analyzer (`debug_analyzer_v2.py`)

Fetches error details (from API or mock data), analyzes related code files with context and blame information, and generates structured JSON reports.

```bash
python debug_analyzer_v2.py ERR_123
```

### 2. Code Fixer (`code_fixer.py`)

Reads the issue JSON, suggests specific code changes based on error type, and can apply changes, create patches, and open pull requests.

```bash
python code_fixer.py issue_ERR_123.json
```

### 3. Notification API (integrated in `demo.py`)

Receives error notifications from monitoring systems. Runs in-process during the demo on port 8001.

---

## Supported Error Types

| Error Type | Fix Strategy |
|------------|--------------|
| DatabaseError | Increase timeouts, parameterize queries, add pooling |
| AuthenticationError | Improve token validation, better header extraction |
| ConnectionError | Add retry logic |
| TimeoutError | Increase/double timeouts |
| ValidationError | Add comprehensive input validation |
| ResourceNotFoundError | Add default values to lookups |
| PermissionError | Add role-based permission checks |
| RateLimitError | Add rate limiting decorators |
| MemoryError | Use generators, memory-efficient structures |
| ConcurrencyError | Add thread safety, locks |
| ConfigurationError | Add default values, validate env vars |
| SecurityError | Add password hashing, secure token handling |
| NetworkError | Add timeouts/retries |
| FileSystemError | Use context managers, check file existence |
| SerializationError | Safe JSON/pickle serialization |

---

## Configuration

Create a `.env` file for custom settings:

```env
DEBUG_API_BASE_URL=http://localhost:8000
DEBUG_API_KEY=dummy_key
REPO_PATH=.
GITHUB_TOKEN=your_token        # For PR creation
GITHUB_REPO=username/repo     # For PR creation
```

---

## Project Structure

```
NoMoreOnCall/
├── debug_analyzer_v2.py   # Main error analyzer
├── code_fixer.py          # Code fix suggestions & Git/PR integration
├── demo.py                # End-to-end demo script
├── ARCHITECTURE.md        # Technical architecture
├── requirements.txt
└── data/                  # Sample data
```

---

## Documentation

- [ARCHITECTURE.md](ARCHITECTURE.md) — Technical architecture and system flow
- [CONTRIBUTING.md](CONTRIBUTING.md) — How to contribute

---

## License

MIT
