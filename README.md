# 🧞‍♂️ DevDebugGenie

> **Intelligent Multi-Agent Development Environment Troubleshooter**  
> Stop wasting 30% of your dev time on repetitive debugging. Let AI agents fix CORS errors, deployment failures, API issues, and database problems automatically.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![Google ADK](https://img.shields.io/badge/Google-ADK-4285F4?logo=google)](https://google.github.io/adk-docs/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.109+-009688?logo=fastapi)](https://fastapi.tiangolo.com/)

---

## 🎯 The Problem

As a full-stack developer, you've experienced this:

- ❌ **CORS errors** between your React frontend and FastAPI backend
- ❌ **Vercel deployment failures** due to missing dependencies or env variables
- ❌ **Railway build errors** with cryptic Python tracebacks
- ❌ **Supabase authentication 401s** that take hours to debug
- ❌ **AI-generated code** that's "almost right" but needs fixing

**Research shows developers waste 30% of their time on these repetitive issues.** 

DevDebugGenie solves this with a **multi-agent AI system** that understands your entire stack.

---

## ✨ Features

### 🤖 Specialized AI Agents

- **CORS Debugger** → Analyzes cross-origin errors, provides exact middleware fixes for FastAPI/Express/Flask
- **API Error Analyzer** → Debugs 401/403/500 errors, authentication issues, JWT problems
- **Database Query Agent** → Fixes SQL errors, Supabase RLS issues, query optimization
- **Vercel Deployment Agent** → Troubleshoots build failures, missing modules, env var issues
- **Railway Deployment Agent** → Solves Python dependency conflicts, port binding, database connections
- **Supabase Connection Agent** → Debugs authentication, RLS policies, connection timeouts

### 🚀 Key Capabilities

✅ **Multi-Agent Architecture**: 7 specialized agents coordinate to solve complex debugging workflows  
✅ **Context-Aware**: Understands your entire stack (frontend + backend + database + deployment)  
✅ **Instant Fixes**: Provides exact code snippets, not vague suggestions  
✅ **Platform-Specific**: Tailored solutions for Vercel, Railway, Supabase, Next.js, FastAPI  
✅ **Session Memory**: Learns from your debugging patterns for personalized help  
✅ **Production-Ready**: Deployed on Google Cloud Run with auto-scaling  

---

## 🏛️ Architecture

```
DevDebugGenie Coordinator (Gemini 2.0 Flash)
├── Error Analyzer Agents
│   ├── CORS Debugger
│   ├── API Error Analyzer
│   └── Database Query Agent
├── Deployment Agents
│   ├── Vercel Agent
│   ├── Railway Agent
│   └── Supabase Agent
└── Custom Tools
    ├── Log Parser
    └── Dependency Checker
```

**Built with:**
- [Google ADK](https://google.github.io/adk-docs/) (Agent Development Kit)
- [Gemini 2.0 Flash](https://ai.google.dev/gemini-api/docs/models) for intelligent routing
- FastAPI for REST API
- Google Cloud Run for deployment

---

## 🚀 Quick Start

### Prerequisites

- Python 3.11 or higher
- Google Gemini API key ([Get one here](https://aistudio.google.com/app/apikey))
- Git

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/rkbharti/devdebuggenie.git
cd devdebuggenie

# 2. Create virtual environment
python -m venv .venv

# Activate virtual environment
# Linux/Mac:
source .venv/bin/activate
# Windows:
.venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Set up environment variables
cp .env.example .env
# Edit .env and add your GOOGLE_API_KEY

# 5. Run the server
python server.py
```

The API will be available at `http://localhost:8080`

---

## 💻 Usage Examples

### Example 1: CORS Error

```bash
curl -X POST http://localhost:8080/chat \
  -H "Content-Type: application/json" \
  -d '{
    "message": "I'm getting CORS error when calling my FastAPI backend from React on localhost:3000"
  }'
```

**Response:**
```json
{
  "response": "I'll help you fix this CORS error. Add this middleware to your FastAPI app:\n\nfrom fastapi.middleware.cors import CORSMiddleware\n\napp.add_middleware(\n    CORSMiddleware,\n    allow_origins=[\"http://localhost:3000\"],\n    allow_credentials=True,\n    allow_methods=[\"*\"],\n    allow_headers=[\"*\"],\n)\n\nThis error occurs because browsers block requests from different origins for security. The middleware tells the browser it's safe to allow requests from localhost:3000."
}
```

### Example 2: Vercel Deployment Failure

```bash
curl -X POST http://localhost:8080/chat \
  -H "Content-Type: application/json" \
  -d '{
    "message": "My Vercel build is failing with: Module not found: Can't resolve 'axios'"
  }'
```

**Response:**
```json
{
  "response": "This error means axios is missing from your package.json. Here's how to fix it:\n\n1. Install axios:\n   npm install axios --save\n\n2. Ensure package.json is committed to git:\n   git add package.json package-lock.json\n   git commit -m 'Add axios dependency'\n   git push\n\n3. Vercel will automatically redeploy.\n\nWhy this happened: The module is used in your code but not listed in dependencies, so Vercel's build environment can't find it."
}
```

### Example 3: Supabase Authentication Error

```bash
curl -X POST http://localhost:8080/chat \
  -H "Content-Type: application/json" \
  -d '{
    "message": "Getting 401 error from Supabase: invalid JWT"
  }'
```

---

## 📁 Project Structure

```
devdebuggenie/
├── agents/
│   ├── coordinator_agent.py       # Main routing agent
│   ├── error_analyzer/
│   │   ├── __init__.py
│   │   ├── cors_debugger.py         # CORS error specialist
│   │   ├── api_error.py             # API error specialist
│   │   └── database_query.py        # Database error specialist
│   └── deployment/
│       ├── __init__.py
│       ├── vercel_agent.py          # Vercel deployment specialist
│       ├── railway_agent.py         # Railway deployment specialist
│       └── supabase_agent.py        # Supabase specialist
├── tools/
│   ├── __init__.py
│   ├── log_parser.py               # Parse deployment logs
│   └── dependency_checker.py       # Check package conflicts
├── memory/
│   └── session_store.py            # Session memory management
├── tests/
│   ├── test_agents.py
│   └── test_tools.py
├── docs/
│   ├── ARCHITECTURE.md             # Detailed architecture docs
│   ├── DEPLOYMENT.md               # Deployment guide
│   └── API.md                      # API documentation
├── server.py                       # FastAPI application
├── Dockerfile                      # Container configuration
├── docker-compose.yml              # Local development setup
├── requirements.txt                # Python dependencies
├── .env.example                    # Environment variables template
├── .gitignore
└── README.md
```

---

## 🛠️ Development

### Running Tests

```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=agents --cov=tools --cov-report=html

# Run specific test file
pytest tests/test_agents.py -v
```

### Code Formatting

```bash
# Format code with black
black .

# Lint with ruff
ruff check .

# Type checking with mypy
mypy agents/ tools/
```

### Local Development with Docker

```bash
# Build and run with docker-compose
docker-compose up --build

# Access API at http://localhost:8080
```

---

## ☁️ Deployment

### Google Cloud Run (Recommended)

```bash
# 1. Install Google Cloud SDK
# https://cloud.google.com/sdk/docs/install

# 2. Authenticate
gcloud auth login

# 3. Set project
gcloud config set project YOUR_PROJECT_ID

# 4. Deploy
gcloud run deploy devdebuggenie \
  --source . \
  --region us-central1 \
  --allow-unauthenticated \
  --set-env-vars GOOGLE_API_KEY=your_key_here
```

See [DEPLOYMENT.md](docs/DEPLOYMENT.md) for detailed deployment instructions.

---

## 📚 Documentation

- **[Architecture Guide](docs/ARCHITECTURE.md)** - Deep dive into multi-agent system design
- **[API Reference](docs/API.md)** - Complete API endpoint documentation
- **[Deployment Guide](docs/DEPLOYMENT.md)** - Deploy to Cloud Run, Railway, or Vercel
- **[Contributing Guide](CONTRIBUTING.md)** - How to contribute to the project

---

## 🛣️ Roadmap

- [x] Core multi-agent system with 6 specialized agents
- [x] FastAPI REST API
- [x] Session memory management
- [x] Deployment tools (Vercel, Railway, Supabase)
- [ ] Web UI dashboard
- [ ] VS Code extension
- [ ] GitHub Actions integration
- [ ] Slack/Discord bot
- [ ] Extended platform support (Netlify, Render, AWS)
- [ ] Code review agent
- [ ] Test generation agent
- [ ] Performance optimization agent

---

## 🤝 Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👤 Author

**Ravi Kumar Bharti**
- GitHub: [@rkbharti](https://github.com/rkbharti)
- Location: Delhi, India
- Bio: Aspiring Data Scientist

---

## 🙏 Acknowledgments

- [Google ADK Team](https://github.com/google/adk) for the amazing agent framework
- [Google Gemini](https://ai.google.dev/gemini-api) for powerful LLM capabilities
- All the developers who waste time debugging - this is for you! 🚀

---

## 💬 Support

If you find this project helpful:
- ⭐ Star this repository
- 🐛 Report bugs via [Issues](https://github.com/rkbharti/devdebuggenie/issues)
- 💡 Request features via [Discussions](https://github.com/rkbharti/devdebuggenie/discussions)

---

<div align="center">
  <strong>Stop debugging. Start building.</strong> 🚀
</div>