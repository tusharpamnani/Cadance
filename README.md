# Cadence

Instead of writing PRDs in a doc and losing them, Cadence keeps requirements gathering, versioning, and state in your terminal. An agentic SDLC CLI tool for solo developers and small teams who want structured, AI-assisted product and engineering requirements without leaving the terminal.

## Features

- **AI-powered requirements**: Chat with an agent to iteratively build a Product Requirements Document (PRD)
- **Structured SDLC**: Tracks iterations through defined states from creation to completion
- **TUI interface**: Split-pane terminal UI with chat on the left and live markdown preview on the right
- **Iteration management**: Create, resume, and complete iterations with persistent state

## Installation

```bash
pip install -e .
```

> **Note:** Cadence is not yet published to PyPI. Install from source using the command above.

## Setup

Set your Gemini API key before using the chat phases:

```bash
export GEMINI_API_KEY="your-api-key-here"
```

The API key is only required for interactive chat phases (`product_requirements_gathering`). Other commands (`init`, `new`, `resume` listing) work without it.

## Quickstart

```bash
# Initialize a Cadence project in your repo
cadence init

# Create a new iteration
cadence iterations new
```

This drops you into a split-pane TUI: chat on the left, live markdown preview on the right. Describe your requirements and the agent will ask clarifying questions while building a PRD.

When the PRD looks good, type `/done` inside the TUI to mark the phase complete and exit. Type `/clear` to reset the chat and start over.

The iteration then moves through these phases:
1. **Product Requirements** — Build a PRD with the agent
2. **Engineering Requirements** — Translate PRD into technical specs
3. **Implementation** — Agent writes code based on the specs

```bash
# Resume an iteration (lists active ones if no slug given)
cadence iterations resume
```

Resuming drops you back into the TUI at whatever state the iteration is in — you'll see your progress so far and can pick up where you left off.

## Usage

### Initialize a project

```bash
cadence init
```

Creates a `.cadence/` directory with configuration and folder structure:

- `.cadence/config.json` — Project configuration
- `.cadence/agents/` — Agent definitions and prompts (reserved for future use)
- `.cadence/prompts/` — Reusable prompt templates (reserved for future use)
- `.cadence/logs/` — Session and interaction logs
- `.cadence/iterations/` — Per-iteration metadata, PRDs, and chat history

### Create a new iteration

```bash
cadence iterations new
```

### Resume an iteration

```bash
# List active iterations and select one
cadence iterations resume

# Resume a specific iteration
cadence iterations resume <slug>
```

## SDLC States

| State | Description |
|-------|-------------|
| `created` | Iteration created |
| `product_requirements_gathering` | Chatting with agent to build PRD |
| `product_requirements_gathered` | PRD complete |
| `engineering_requirements_gathering` | Translating PRD into engineering specs |
| `engineering_requirements_gathered` | Engineering requirements complete |
| `implementation_in_progress` | Agentic coding based on requirements |
| `implementation_completed` | Implementation done |
| `completed` | Iteration finished |

## Requirements

- Python >= 3.8
- `GEMINI_API_KEY` environment variable (for chat phases only)

## License

MIT
