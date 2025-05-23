# Agent Test - MCP Research Server

[![Python](https://img.shields.io/badge/Python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![MCP](https://img.shields.io/badge/MCP-Model%20Context%20Protocol-purple.svg)](https://modelcontextprotocol.io/)
[![arXiv](https://img.shields.io/badge/arXiv-Research%20Papers-red.svg)](https://arxiv.org/)
[![UV](https://img.shields.io/badge/UV-Package%20Manager-orange.svg)](https://github.com/astral-sh/uv)

> MCP server for searching and managing arXiv research papers with intelligent paper information extraction and local storage.

## 🚀 Quick Start

```bash
# Clone the repository
git clone https://github.com/jieli-matrix/abacus-mcp.git
cd abacus-mcp

# Create virtual environment with Python 3.11
uv init -p 3.11
uv venv

# Activate virtual environment
source .venv/bin/activate  # Linux/macOS
# .venv\Scripts\activate   # Windows

# Install dependencies
uv sync

# Run the MCP server with Inspector
npx @modelcontextprotocol/inspector uv run research_server.py
```

## 🛠️ Features

- **📚 Paper Search**: Search arXiv papers by topic with relevance ranking
- **🔍 Information Extraction**: Extract detailed paper metadata (title, authors, summary, etc.)
- **💾 Local Storage**: Store paper information in organized JSON files
- **🤖 MCP Integration**: Compatible with MCP-enabled AI assistants
- **⚡ Fast Performance**: Built with UV package manager for speed

## 📦 Available Tools

### `search_papers`
Search for papers on arXiv based on a topic and store their information locally.

**Parameters:**
- `topic` (str): The research topic to search for
- `max_results` (int, optional): Maximum number of results to retrieve (default: 5)

**Returns:**
- List of paper IDs found in the search

**Example:**
```json
{
  "topic": "machine learning",
  "max_results": 3
}
```

### `extract_info`
Retrieve stored information about a specific paper from local storage.

**Parameters:**
- `paper_id` (str): The arXiv paper ID to look for

**Returns:**
- JSON string with paper information if found, error message if not found

**Example:**
```json
{
  "paper_id": "2301.12345"
}
```

## 🏗️ Project Structure

```
agent-test/
├── .venv/                 # Virtual environment 
├── research_server.py     # Main MCP server implementation
├── main.py               # Entry point
├── pyproject.toml        # UV project configuration
├── uv.lock              # Dependency lock file
├── papers/              # Generated paper storage directory
│   └── topic_name/
│       └── papers_info.json
├── README.md            
└── .gitignore          # Git ignore rules
```

## 🔧 Development

### Prerequisites

- Python 3.11+
- Node.js 18+ (for MCP Inspector)
- UV package manager

### Setup Development Environment

```bash
# Install UV (if not already installed)
pip install uv

# Install development dependencies
uv add mcp arxiv
```

## 🌐 Deployment Options

### Option 1: Local Development

For local development, no additional configuration is needed:

```bash
# Start the server locally
npx @modelcontextprotocol/inspector uv run research_server.py

# Access Inspector at http://localhost:6274
# Configure in Inspector UI:
# - Command: uv
# - Arguments: run research_server.py
# - No Inspector Proxy Address needed
```

### Option 2: Remote Server Deployment

If deploying on a remote server with restricted ports (e.g., only 50001-55000 open):

#### Step 1: SSH Port Forwarding

```bash
# Forward both Inspector ports from remote server to local
# Map remote 6274 -> local 52001 (within allowed range)
# Map remote 6277 -> local 52002 (within allowed range)
ssh -L 52001:localhost:6274 -L 52002:localhost:6277 username@your-server-ip
```

#### Step 2: Start Server on Remote

```bash
# On remote server
npx @modelcontextprotocol/inspector uv run research_server.py
```

#### Step 3: Configure Inspector

Access `http://localhost:6274` in your local browser and configure:
- **Command**: `uv`
- **Arguments**: `run research_server.py`
- **Inspector Proxy Address**: `http://localhost:52002`

## 📊 Usage Examples

### Search for AI Papers

```bash
# Start the server
npx @modelcontextprotocol/inspector uv run research_server.py

# In Inspector UI, call search_papers:
{
  "topic": "artificial intelligence",
  "max_results": 5
}
```

### Extract Paper Information

```bash
# After searching, extract specific paper info:
{
  "paper_id": "2301.07041"
}
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🔗 Resources

- [MCP Documentation](https://modelcontextprotocol.io/)
- [arXiv API Documentation](https://arxiv.org/help/api)
- [FastMCP](https://github.com/jlowin/fastmcp)
- [UV Package Manager](https://github.com/astral-sh/uv)

## 🐛 Troubleshooting

### Common Issues

| Issue | Solution |
|-------|----------|
| `ModuleNotFoundError: mcp` | Run `uv sync` to install dependencies |
| Inspector connection failed | Check Node.js version (`node --version`) |
