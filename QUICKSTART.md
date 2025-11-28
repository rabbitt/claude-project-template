# Quick Start Guide

Get up and running with this workflow in 15 minutes.

## Prerequisites

- Git installed and configured
- A project you want to manage with AI assistance
- Claude Code CLI (installation below)

## Step 1: Install Claude Code CLI

### macOS / Linux

```bash
# Using npm (Node.js required)
npm install -g @anthropic-ai/claude-code

# Or using Homebrew (macOS)
brew install anthropic/tap/claude-code
```

### Windows

```powershell
# Using npm (Node.js required)
npm install -g @anthropic-ai/claude-code

# Or using winget
winget install Anthropic.ClaudeCode
```

### Verify Installation

```bash
claude --version
```

### Authentication

```bash
# Authenticate with your Anthropic API key
claude auth login

# Or set environment variable
export ANTHROPIC_API_KEY="your-api-key-here"
```

## Step 2: Copy Template Files

### Option A: Clone the Template

```bash
# Clone to a temporary location
git clone https://github.com/your-username/claude-project-template.git /tmp/template

# Copy files to your project
cp -r /tmp/template/CLAUDE.md /tmp/template/docs your-project/

# Clean up
rm -rf /tmp/template
```

### Option B: Manual Setup

Create this directory structure in your project:

```
your-project/
├── CLAUDE.md                    # AI memory (copy from template)
└── docs/
    ├── process/
    │   ├── FEATURE_WORKFLOW.md  # 9-step process
    │   ├── FEATURE_PLAN.md      # Feature roadmap
    │   ├── TANGENT_TASKS.md     # Tangent tracker
    │   └── SESSION_LOG.md       # Work history
    ├── architecture/
    │   └── DECISIONS.md         # ADR log
    └── reference/
        ├── CONVENTIONS.md       # Coding standards
        ├── BUILD.md             # Build commands
        └── STRUCTURE.md         # File organization
```

## Step 3: Customize for Your Project

### 1. Edit CLAUDE.md

Update these sections:

```markdown
## Project Overview
[Describe YOUR project - what it does, tech stack, architecture]

## Current Status
- **Active Feature**: None (starting fresh)
- **Branch**: `main`
- **Progress**: Project setup
```

### 2. Edit FEATURE_PLAN.md

Add your initial features:

```markdown
## Feature Roadmap

### Phase 1: Foundation
- [ ] **Feature 1**: [Your first feature]
- [ ] **Feature 2**: [Your second feature]
```

### 3. Edit Reference Files

Choose the appropriate language example from `examples/` and customize:

- **C project**: Copy from `examples/c/`
- **C++ project**: Copy from `examples/cpp/`
- **Python library**: Copy from `examples/python-lib/`
- **Django project**: Copy from `examples/python-django/`
- **Go project**: Copy from `examples/golang/`

```bash
# Example: Setting up a Python library project
cp examples/python-lib/CONVENTIONS.md docs/reference/
cp examples/python-lib/BUILD.md docs/reference/
cp examples/python-lib/STRUCTURE.md docs/reference/
```

## Step 4: Start Your First Session

### Launch Claude Code

```bash
cd your-project
claude
```

### First Message to Claude

Start with something like:

```
Welcome to the project! Please read CLAUDE.md and the files listed
in the startup instructions to understand our workflow.

Let me know when you're ready, and we can start planning our first feature.
```

### Creating Your First Feature

Follow the workflow:

1. **Describe what you want**: "I want to add user authentication to the app"
2. **Review the 10K foot view**: Claude proposes high-level approach
3. **Approve to proceed**: "Looks good, let's plan the details"
4. **Review detailed plan**: Claude writes implementation plan
5. **Approve implementation**: "Approved, let's implement"
6. **Monitor progress**: Watch as Claude implements
7. **Review and test**: Verify the implementation works
8. **Approve merge**: "Approved for merge"
9. **Complete**: Feature is merged to main

## Step 5: End Your Session Properly

Before ending each session:

1. **Ask Claude to summarize**: "Please update CLAUDE.md with our progress"
2. **Verify updates**: Check that Current Status and Notes for Next Session are updated
3. **Commit if needed**: Save any in-progress work

### Starting the Next Session

```bash
cd your-project
claude
```

Then:

```
Let's continue where we left off. Please read CLAUDE.md and the
startup files to get context.
```

## Common Commands

### Claude Code CLI

```bash
# Start interactive session
claude

# Start with a specific file context
claude --file src/main.py

# Continue a previous conversation
claude --continue

# Run a single command
claude -c "explain what this function does"
```

### During Sessions

Useful phrases for directing Claude:

```
# Feature workflow
"Let's start Feature 3"
"Show me the 10K foot view for this feature"
"I approve the plan, let's implement"
"Let's review what we've done"
"Approved for merge"

# Tangent management
"This is a tangent - document it but let's stay focused"
"Add this to TANGENT_TASKS.md and continue"

# Context refresh
"Please re-read CLAUDE.md to refresh context"
"What's our current status?"

# Session management
"Update the session notes before we end"
"Summarize what we accomplished today"
```

## Troubleshooting

### Claude loses context mid-session

```
Let's refresh. Please re-read CLAUDE.md and docs/process/FEATURE_PLAN.md
to get back on track.
```

### Claude goes off-track with tangents

```
Stop - this is tangent territory. Please document this in
TANGENT_TASKS.md with a breadcrumb to our current feature,
and let's continue with [current feature].
```

### Claude makes changes without approval

```
Hold on - we need to follow the workflow. Please show me the plan
first before implementing.
```

### Starting fresh after a long break

```
It's been a while since we worked on this. Please read all the files
in CLAUDE.md's startup instructions and give me a status summary
before we continue.
```

## Next Steps

1. **Read the full README.md** for philosophy and detailed examples
2. **Read FEATURE_WORKFLOW.md** to understand the 9-step process
3. **Customize the template** for your specific project needs
4. **Start building!**

---

## Alternative: ChatGPT CLI Setup

If you prefer using OpenAI's ChatGPT:

### Installation

```bash
# Using pip
pip install chatgpt-cli

# Or using npm
npm install -g chatgpt-cli
```

### Authentication

```bash
# Set your OpenAI API key
export OPENAI_API_KEY="your-api-key-here"
```

### Usage

The workflow process is the same - just use your preferred AI tool. The key is the documentation structure and approval-gated workflow, not the specific AI.

---

## Quick Reference Card

```
┌─────────────────────────────────────────────────────────────┐
│                    SESSION CHECKLIST                        │
├─────────────────────────────────────────────────────────────┤
│ START OF SESSION:                                           │
│ □ cd to project directory                                   │
│ □ Run: claude                                               │
│ □ Ask Claude to read CLAUDE.md + startup files              │
│ □ Review current status together                            │
├─────────────────────────────────────────────────────────────┤
│ DURING SESSION:                                             │
│ □ Follow 9-step workflow for features                       │
│ □ Document tangents, don't pursue them                      │
│ □ Review and approve before merging                         │
├─────────────────────────────────────────────────────────────┤
│ END OF SESSION:                                             │
│ □ Ask Claude to update CLAUDE.md status/notes               │
│ □ Commit any work in progress                               │
│ □ Note where to pick up next time                           │
└─────────────────────────────────────────────────────────────┘
```
