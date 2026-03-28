# SovereignLM - Privacy-first AI Studio
# Copyright (C) 2026 [Ivan Vankov Fortanet @copaeks]
#
# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU Affero General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
# GNU Affero General Public License for more details.
#
# You should have received a copy of the GNU Affero General Public License
# along with this program. If not, see <https://www.gnu.org/licenses/>.


# SovereignLM

A **privacy-first**, feature-rich desktop application for chatting with local and cloud Large Language Models (LLMs). Built with Electron + React + TypeScript frontend and Python + FastAPI backend.

**Version 2.0** introduces Universal API Router, Architecture Switching, ComfyUI Integration, Enhanced Agent Swarm, and GUI Layers.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Privacy](https://img.shields.io/badge/privacy-first-green.svg)
![No Telemetry](https://img.shields.io/badge/telemetry-none-red.svg)

## ✨ Features

### 🔒 Privacy First
- **Zero telemetry** - No usage data collection whatsoever
- **No analytics** - No tracking of any kind
- **No automatic updates** - Manual updates only
- **Local processing** - All AI runs on your machine (when using local models)
- **Explicit connections only** - Network calls only for user-initiated actions

### 🌐 Universal API Router (v2.0)
Connect to multiple LLM providers with automatic failover:
- **OpenAI** (GPT-4, GPT-3.5)
- **Anthropic** (Claude 3 Opus, Sonnet, Haiku)
- **Groq** (Fast inference)
- **Fireworks** (Various models)
- **Local Models** (Llama.cpp, Transformers)

Features:
- Automatic provider selection based on availability
- Fallback between providers
- Per-provider configuration (API keys, models, priority)

### 🔄 Architecture Switching (v2.0)
Seamlessly switch between execution modes without losing context:
- **Sequential** - Single agent (simple queries, low resources)
- **Parallel/Swarm** - Multi-agent (complex tasks, parallel processing)
- **Cloud** - External APIs (when local resources constrained)
- **Adaptive** - Auto-switch based on task complexity and resources

### 🐝 Enhanced Agent Swarm (v2.0)
Hierarchical, dynamic, resource-efficient multi-agent system:

**Orchestrator Agent**
- Analyzes and decomposes tasks into DAGs
- Plans execution strategy
- Synthesizes final results

**Worker Agents**
- Specialized roles: Researcher, Coder, Writer, Analyst, Creative
- Execute subtasks in parallel
- Share memory and communicate via message bus

**Dynamic Task Decomposition**
- Automatically breaks complex queries into subtasks
- Handles comparisons, coding, writing, research, creative tasks
- Creates execution DAG with dependencies

**Adaptive Parallelism**
- Monitors CPU, RAM, VRAM in real-time
- Adjusts concurrent agent count dynamically
- Gracefully degrades to sequential when resources tight

**Memory & Context Sharing**
- Vector database (ChromaDB) for semantic search
- Key-value store for structured data
- Message bus for event publishing/subscribing
- All agents access shared knowledge

**Tool Calling**
- ComfyUI for image/video generation
- Git operations
- File operations
- Web search
- Custom tool registration

**Fault Tolerance**
- Automatic retry with exponential backoff
- Task reassignment on worker failure
- Escalation after 3 failures

### 🎨 ComfyUI Integration (v2.0)
Generate images and videos within the chat workflow:
- Text-to-image generation
- Image-to-image transformation
- Upscaling
- Workflow templates
- Progress tracking

### 🖥️ GUI Layers (v2.0)
Three user interface modes:

**Simple Mode**
- Minimal UI with just chat
- Natural language profile creator
- Perfect for casual users

**Pro Mode**
- Full feature access
- Models, Profiles, HuggingFace, Git
- Universal router configuration
- ComfyUI integration

**Developer Mode**
- Everything in Pro mode
- Workflow editor (visual node-based editor)
- Swarm visualization
- Architecture switching controls
- Memory inspection
- Tool registry access

### 💬 Core Chat Interface
- WebSocket-based streaming responses
- Markdown rendering with syntax highlighting
- Model and profile selectors
- Architecture mode badge
- Resource usage display

### 🤗 HuggingFace Integration
- Search models by name and task
- Download with progress tracking
- Automatic GGUF detection
- Import local models

### 👤 Natural Language Profile Creator
Create AI personas by describing them:
- "A funny historian who answers with curious anecdotes"
- "A patient coding mentor who explains step by step"

Generates complete profiles with system prompts, temperature, and parameters.

### 🌿 Git Integration
- Version control for profiles
- Auto-commit on changes (optional)
- Clone/push/pull for sync

## 🏗️ Architecture

```
LM Chat Pro/
├── backend/                      # Python FastAPI Backend
│   ├── app/
│   │   ├── main.py              # FastAPI with WebSockets
│   │   ├── config.py            # Settings (privacy-first)
│   │   ├── models/              # Local model management
│   │   ├── profiles/            # Profile management
│   │   ├── router/              # 🆕 Universal API Router
│   │   │   ├── base.py          # Router interface
│   │   │   ├── dispatcher.py    # Provider selection
│   │   │   └── adapters/        # Provider implementations
│   │   ├── architectures/       # 🆕 Architecture switching
│   │   │   ├── base.py          # Architecture interface
│   │   │   ├── sequential.py    # Single agent
│   │   │   ├── parallel.py      # Swarm mode
│   │   │   ├── cloud.py         # External APIs
│   │   │   └── orchestrator.py  # Auto-switching
│   │   ├── swarm_new/           # 🆕 Enhanced Agent Swarm
│   │   │   ├── orchestrator.py  # Main orchestrator
│   │   │   ├── worker.py        # Worker agents
│   │   │   ├── scheduler.py     # Task scheduling
│   │   │   └── task_decomposer.py
│   │   ├── memory/              # 🆕 Memory Store
│   │   │   └── store.py         # Vector DB + KV store
│   │   ├── tools/               # 🆕 Tool Registry
│   │   │   └── registry.py      # Tool management
│   │   └── comfy/               # 🆕 ComfyUI Integration
│   │       ├── client.py        # ComfyUI API client
│   │       └── manager.py       # Generation management
│   └── requirements.txt
├── frontend/                     # Electron + React + TypeScript
│   ├── src/
│   │   ├── components/
│   │   │   ├── workflow/        # 🆕 Workflow editor
│   │   │   ├── ArchitectureBadge.tsx
│   │   │   ├── GUILayerProvider.tsx
│   │   │   └── ...
│   │   ├── pages/
│   │   │   ├── ProvidersPage.tsx      # 🆕 Router config
│   │   │   ├── ComfyUIPage.tsx        # 🆕 Image generation
│   │   │   ├── WorkflowPage.tsx       # 🆕 Developer editor
│   │   │   ├── SimpleChatPage.tsx     # 🆕 Simple mode
│   │   │   └── ...
│   │   ├── store/
│   │   │   └── guiStore.ts      # 🆕 GUI layer state
│   │   └── ...
│   └── package.json
└── profiles/                     # User profiles
```

## 🚀 Installation

### Prerequisites
- Python 3.9+
- Node.js 18+
- Git
- (Optional) ComfyUI for image generation

### Backend Setup

```bash
cd backend
python -m venv venv

# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate

pip install -r requirements.txt
```

### Frontend Setup

```bash
cd frontend
npm install
```

### Running in Development

```bash
# Terminal 1: Start backend
cd backend
python run.py

# Terminal 2: Start frontend
cd frontend
npm run dev
```

### ComfyUI Setup (Optional)

```bash
git clone https://github.com/comfyanonymous/ComfyUI.git
cd ComfyUI
pip install -r requirements.txt
python main.py
```

## 📖 Usage Guide

### 1. GUI Layer Selection

Choose your interface complexity from the sidebar:
- **Simple**: Just chat
- **Pro**: Full features
- **Developer**: Workflow editor + advanced tools

### 2. Configure Providers (Pro/Developer)

Go to **Providers** page to add:
- OpenAI API key
- Anthropic API key
- Local model paths

### 3. Architecture Switching

The system can automatically switch between:
- **Sequential**: Single model, low resource usage
- **Swarm**: Multiple agents, parallel processing
- **Cloud**: External APIs when local resources tight
- **Adaptive**: Auto-select based on task

Click the badge in the header to manually switch.

### 4. Using the Swarm

Enable "Swarm Mode" in chat settings:
- Complex queries are automatically decomposed
- Multiple agents work in parallel
- Results are synthesized automatically
- Resource usage is monitored and throttled

### 5. Image Generation with ComfyUI

Ensure ComfyUI is running, then:
1. Go to **ComfyUI** page
2. Select a workflow (text-to-image, etc.)
3. Enter your prompt
4. Click Generate

### 6. Workflow Editor (Developer)

Create custom workflows by connecting nodes:
- LLM nodes for language processing
- ComfyUI nodes for image generation
- Swarm nodes for multi-agent tasks
- Tool nodes for external actions
- Git nodes for version control

## 🔌 Communication Architecture

### HTTP REST API
- `/api/router/*` - Universal router management
- `/api/architecture/*` - Architecture switching
- `/api/swarm/*` - Swarm status and workers
- `/api/comfy/*` - ComfyUI operations
- `/api/memory/*` - Memory store access
- `/api/tools/*` - Tool registry
- `/api/workflow/run` - Execute workflows

### WebSocket Endpoints
- `/ws/chat` - Standard chat
- `/ws/chat_universal` - Universal router chat with architecture switching

## 🧠 How the Swarm Works

### Task Decomposition

When you send a complex query:
```
"Compare Python and JavaScript for web development"
```

The orchestrator:
1. **Detects** this is a comparison task
2. **Decomposes** into:
   - Analyze Python for web dev
   - Analyze JavaScript for web dev
   - Synthesize comparison
3. **Creates DAG** with dependencies
4. **Schedules** execution in levels

### Resource-Aware Execution

```python
# Scheduler monitors resources
if cpu < 50% and memory_free > 2GB:
    increase_parallelism()
elif cpu > 80% or vram_near_limit:
    throttle_or_degrade()
```

### Memory Sharing

All agents have access to:
- **Vector DB**: Semantic search of past results
- **Key-Value Store**: Structured data
- **Message Bus**: Real-time events

Example:
```python
# Agent 1 generates image
await memory.store(
    content="Generated image of a cat",
    entry_type="image_gen",
    metadata={"task_id": "abc123"}
)

# Agent 2 can find it
results = await memory.search(
    query="cat image",
    entry_type="image_gen"
)
```

## 🔒 Security & Privacy

> **⚠️ IMPORTANT PRIVACY DISCLAIMER**
>
> LM Chat Pro is **privacy-first only when using local models and local memory**.
> Any connection to cloud providers (OpenAI, Anthropic, Groq, Fireworks, etc.) 
> sends data to third-party servers. You are responsible for reviewing their 
> privacy policies. We do not collect telemetry or log your data.

### No Telemetry
```python
TELEMETRY_ENABLED = False  # Hardcoded
CHECK_FOR_UPDATES = False
```

### Restricted Connections
Only connects to:
1. Local backend
2. User-configured providers (OpenAI, etc.) - **data leaves machine**
3. HuggingFace (explicit actions) - **data leaves machine**
4. ComfyUI (if running locally)
5. GitHub (explicit actions) - **data leaves machine**

### Local-First Design
- All inference can run locally
- Cloud only when explicitly configured
- No data leaves machine for local models

### Offline Mode (v3.0)
Enable `OFFLINE_MODE=true` in settings to block all external connections:
- Only local providers (Llama.cpp, Transformers, Ollama) are allowed
- Cloud provider requests are blocked
- A "Fully Offline" badge appears in the UI

### Secure API Key Storage (v3.0)
API keys are stored in OS-native secure storage:
- **Windows**: Credential Manager
- **macOS**: Keychain
- **Linux**: Secret Service API (libsecret)
- **Fallback**: Encrypted file with Fernet symmetric encryption

Keys are never stored in plain text files. Use the migration script to move existing `.env` keys:
```bash
cd backend
python -m app.security.migrate_env_keys
```

### Network Audit (v3.0)
All outbound connections are logged to a local audit file. Access via:
- API: `GET /api/network/audit`
- Developer mode UI: Network Monitor

### Input Sanitization (v3.0)
All user inputs are sanitized before processing:
- Path traversal protection
- Shell injection prevention
- Capability-based tool permissions
- Sandbox mode for file operations

## 🛠️ Advanced Configuration

### Environment Variables
```bash
# .env file
DEFAULT_ARCHITECTURE=adaptive
MAX_CONCURRENT_AGENTS=4
COMFYUI_HOST=127.0.0.1
COMFYUI_PORT=8188
MEMORY_VECTOR_DB=chroma
```

### Adding Custom Tools

```python
from app.tools.registry import tool_registry, Tool, ToolCategory

async def my_tool_handler(param1: str):
    # Your tool logic
    return ToolResult(success=True, data={"result": "..."})

tool_registry.register(Tool(
    name="my_custom_tool",
    description="Does something useful",
    category=ToolCategory.CUSTOM,
    handler=my_tool_handler,
    parameters={"param1": {"type": "string"}},
    required_params=["param1"],
    returns={"type": "object"},
))
```

## 📄 License

MIT License - See LICENSE file

## 🙏 Acknowledgments

- [llama.cpp](https://github.com/ggerganov/llama.cpp)
- [HuggingFace](https://huggingface.co/)
- [ComfyUI](https://github.com/comfyanonymous/ComfyUI)
- [ChromaDB](https://www.trychroma.com/)
- [React Flow](https://reactflow.dev/)

---

**Made with 🔒 privacy in mind. Your data stays yours.**
