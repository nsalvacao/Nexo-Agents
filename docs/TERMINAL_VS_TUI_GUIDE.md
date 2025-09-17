# Terminal vs TUI Command Usage Guide

> **⚖️ LEGAL DISCLAIMER**: This guide covers usage of Google's AI CLI tool (`gemini-cli`). "Gemini" is a trademark of Google LLC. We are not affiliated with or endorsed by Google LLC.

## Understanding Google AI CLI Modes

The Google AI CLI (`gemini-cli`) operates in two distinct modes that have different command syntax and capabilities:

---

## 🖥️ Terminal Mode (Outside CLI)

Commands executed directly from your system terminal/command prompt, **before** entering the interactive CLI interface.

### When to Use Terminal Mode
- **One-time command execution** with immediate exit
- **Scripting and automation** where you need CLI results in scripts
- **CI/CD pipelines** for automated processing
- **Testing specific commands** without starting interactive session

### Terminal Mode Syntax
```bash
# Basic structure
gemini [options] "prompt"

# Include custom commands
gemini --include path/to/command.toml "command invocation"

# Multiple directory inclusion
gemini --include-directories dir1,dir2 "prompt"

# Model selection
gemini -m gemini-2.0-flash "prompt"
```

### Terminal Mode Examples
```bash
# Execute security analysis (one-time)
gemini --include nexo-agents/engineering/security-analyst.toml "/security-analyst deps scan"

# Code review with specific model
gemini -m gemini-2.0-flash --include nexo-agents/engineering/code-reviewer.toml "/code-reviewer file src/main.py"

# Quick AI assistance
gemini "Explain this error: ImportError: No module named 'requests'"

# Include multiple directories
gemini --include-directories lib,docs,src "Analyze the project architecture"
```

---

## 💬 TUI Mode (Inside CLI Interface)

Commands executed **inside** the interactive text user interface after running `gemini` and entering the CLI session.

### When to Use TUI Mode
- **Interactive conversations** with back-and-forth dialogue
- **Complex multi-step workflows** requiring iteration
- **Exploratory analysis** where you need to refine queries
- **Session continuity** with memory and context preservation

### TUI Mode Features
- **Slash commands** (`/command`) for CLI functionality
- **At commands** (`@file`) for file inclusion
- **Shell commands** (`!command`) for system integration
- **Session memory** and conversation history
- **Command composition** with `&&` operators

### TUI Mode Examples

#### Starting TUI Session
```bash
# Start interactive session
gemini

# Start with included directories
gemini --include-directories nexo-agents/engineering,nexo-agents/design
```

#### Inside TUI Interface
```bash
# View available commands
/help

# Execute custom commands (installed in ~/.gemini/commands/)
/security-analyst deps scan
/code-reviewer file src/main.py quality
/ai-engineer rag setup

# Command composition
/security-analyst deps && /code-reviewer security

# Include files in conversation
@src/main.py
@package.json

# Execute shell commands
!git status
!ls -la src/

# Memory management
/memory show
/memory add "Project uses React with TypeScript"

# Session management
/checkpoint save pre-refactor
/checkpoint resume
```

---

## 🔄 Command Discovery & Installation

### Global Installation (Available in all projects)
```bash
# Copy commands to global directory
cp nexo-agents/engineering/security-analyst.toml ~/.gemini/commands/

# Verify installation
ls ~/.gemini/commands/

# Use in any TUI session
gemini
/help  # security-analyst should appear in list
```

### Project-Specific Installation
```bash
# Create project commands directory
mkdir -p .gemini/commands/

# Copy commands for this project only
cp nexo-agents/engineering/code-reviewer.toml .gemini/commands/

# Use in TUI session within this project
gemini
/code-reviewer file src/main.py
```

### On-Demand Loading (Terminal Mode)
```bash
# Load command temporarily without installation
gemini --include nexo-agents/engineering/ai-engineer.toml "/ai-engineer llm setup"
```

---

## 📋 Command Reference Quick Guide

### Terminal Mode Commands
| Command | Purpose | Example |
|---------|---------|---------|
| `gemini "prompt"` | Direct AI query | `gemini "Explain async/await"` |
| `gemini --include file.toml "command"` | Load custom command | `gemini --include cmd.toml "/mycmd"` |
| `gemini --include-directories dirs "prompt"` | Include multiple dirs | `gemini --include-directories src,docs "analyze"` |
| `gemini -m model "prompt"` | Use specific model | `gemini -m gemini-2.0-flash "prompt"` |

### TUI Mode Commands
| Command | Purpose | Example |
|---------|---------|---------|
| `/help` | Show available commands | `/help` |
| `/command args` | Execute custom command | `/security-analyst deps` |
| `@file` | Include file content | `@src/main.py` |
| `!shell` | Execute shell command | `!git status` |
| `/memory` | Manage session memory | `/memory show` |
| `/checkpoint` | Save/restore session | `/checkpoint save tag` |
| `/quit` | Exit CLI | `/quit` or `Ctrl+C` twice |

---

## ⚡ Best Practices

### Use Terminal Mode For:
- **Automation scripts**: `gemini --include cmd.toml "/analyze" > report.txt`
- **CI/CD integration**: Automated code analysis in build pipelines
- **Quick one-off queries**: Fast answers without session overhead
- **Batch processing**: Processing multiple files programmatically

### Use TUI Mode For:
- **Interactive development**: Iterative code review and improvement
- **Complex analysis**: Multi-step problem solving with refinement
- **Learning and exploration**: Discovering command capabilities
- **Workflow composition**: Chaining multiple commands together

### Performance Considerations
- **Terminal mode**: Faster startup, no session overhead
- **TUI mode**: Session memory, context preservation, conversation history
- **Command installation**: Global commands load faster than `--include`
- **Directory inclusion**: More directories = slower initial context loading

---

## 🚨 Common Pitfalls

### ❌ Don't Mix Modes
```bash
# Wrong: Can't use TUI commands in terminal
gemini "/help"  # This won't work

# Correct: Enter TUI first
gemini
/help
```

### ❌ Don't Forget Command Discovery
```bash
# Wrong: Command not found if not installed
gemini
/my-custom-command  # Error if not in ~/.gemini/commands/

# Correct: Install first or use --include
cp my-custom-command.toml ~/.gemini/commands/
```

### ❌ Don't Use Wrong Syntax
```bash
# Wrong: TUI syntax in terminal
gemini @file.txt "analyze this"

# Correct: Include files properly in terminal
gemini --include-directories . "analyze file.txt"
```

---

## 🔍 Troubleshooting

### Command Not Found
```bash
# Check command installation
ls ~/.gemini/commands/
ls .gemini/commands/

# Verify TOML syntax
cat command.toml

# Test with --include
gemini --include command.toml "/help"
```

### TUI Not Responding
```bash
# Exit safely
Ctrl+C (twice)

# Or use quit command
/quit
```

### Shell Commands Not Working
```bash
# Check if shell commands are enabled
/tools

# Test simple shell command
!echo "test"
```

This guide ensures you understand the distinction between terminal and TUI modes, enabling effective use of both Google AI CLI interfaces with our custom commands.