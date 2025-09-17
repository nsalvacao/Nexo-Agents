# Nexo-Agents for Google AI CLI

**Production-ready AI agent commands following official Google AI CLI standards**

> **⚖️ LEGAL DISCLAIMER**: This project provides independent third-party commands for Google's AI CLI tool (technical command: `gemini-cli`). "Gemini" is a trademark of Google LLC. This project is not affiliated with, endorsed by, or sponsored by Google LLC. All trademarks are property of their respective owners. Use of trademark names is for identification and interoperability purposes only under nominative fair use principles.

A comprehensive collection of 44 specialized AI commands designed for seamless integration with Google's AI CLI native discovery mechanism. Each command is optimized for CLI usage with dynamic argument parsing, contextual shell integration, and structured output.

---

## ✨ What Makes This Different

### Official Google AI CLI Compliance
- **Native `{{args}}` parsing** for dynamic command arguments
- **Shell command integration** via `!{command}` for context gathering
- **CLI-optimized prompts** focused on specific tasks, not role-playing
- **Structured output** designed for automation and scripting

### Context-Aware Intelligence
Every command automatically analyzes your project environment:
```bash
# Automatic context discovery
!{find . -name "*.py" | head -5}        # Code files
!{cat package.json requirements.txt}    # Dependencies  
!{git log --oneline -3}                 # Recent changes
```

## 🚀 Quick Start

### Method 1: Native Discovery (Recommended)
Copy commands to your Google AI CLI directory for automatic discovery:

```bash
# Global installation (available in any project)
cp commands/engineering/security-analyst.toml ~/.gemini/commands/

# Project-specific installation 
cp commands/engineering/code-reviewer.toml .gemini/commands/

# Use with natural command syntax (inside the CLI TUI)
/security-analyst deps scan
/code-reviewer file src/main.py
```

### Method 2: On-Demand Loading
Load commands temporarily without installation:

```bash
# Terminal command (outside CLI)
gemini --include commands/engineering/ai-engineer.toml "/ai-engineer llm openai"
```

## 📋 Command Structure

All commands follow the optimized Google AI CLI pattern:

```toml
description = "Brief description for /help menu"

prompt = """
You are a [role] specializing in [domain].

Task: {{args}}

## CONTEXT ANALYSIS
Project files: !{find . -name "*.ext" | head -5}
Dependencies: !{cat package.json requirements.txt 2>/dev/null}

## [SPECIFIC_CAPABILITIES]
- Capability 1 with clear parameters
- Capability 2 with usage examples
- Capability 3 with expected outputs

[Implementation guidance]
"""
```

## 🗂️ Complete Command Directory

### 🔧 Engineering (11 commands)
| Command | Purpose | Example Usage |
|---------|---------|---------------|
| `ai-engineer` | AI/ML implementation | `/ai-engineer rag setup` |
| `backend-architect` | API & system design | `/backend-architect api user-management` |
| `code-reviewer` | Code quality analysis | `/code-reviewer diff HEAD~1` |
| `data-engineer` | Data pipelines & ETL | `/data-engineer pipeline csv-to-db` |
| `devops-automator` | CI/CD & infrastructure | `/devops-automator docker setup` |
| `frontend-developer` | UI implementation | `/frontend-developer component react` |
| `mobile-app-builder` | Mobile development | `/mobile-app-builder flutter auth` |
| `rapid-prototyper` | MVP development | `/rapid-prototyper api-server python` |
| `security-analyst` | Security analysis | `/security-analyst deps scan` |
| `sre` | Site reliability | `/sre monitoring setup` |
| `test-writer-fixer` | Test automation | `/test-writer-fixer unit api.py` |

### 📊 Product (3 commands)
| Command | Purpose | Example Usage |
|---------|---------|---------------|
| `feedback-synthesizer` | User feedback analysis | `/feedback-synthesizer reviews summary` |
| `sprint-prioritizer` | Task prioritization | `/sprint-prioritizer backlog features` |
| `trend-researcher` | Market research | `/trend-researcher tech ai-tools` |

### 📈 Marketing (8 commands)
| Command | Purpose | Example Usage |
|---------|---------|---------------|
| `app-store-optimizer` | ASO optimization | `/app-store-optimizer keywords productivity` |
| `content-creator` | Content generation | `/content-creator blog ai-trends` |
| `growth-hacker` | Growth experiments | `/growth-hacker viral email` |
| `instagram-curator` | Visual content | `/instagram-curator tech-posts feed` |
| `nexo-social-strategist` | Social strategy | `/nexo-social-strategist campaign launch` |
| `reddit-community-builder` | Community growth | `/reddit-community-builder programming post` |
| `tiktok-strategist` | Short-form video | `/tiktok-strategist tech-tips series` |
| `twitter-engager` | Tweet optimization | `/twitter-engager thread ai-trends` |

### 🎨 Design (5 commands)
| Command | Purpose | Example Usage |
|---------|---------|---------------|
| `brand-guardian` | Brand consistency | `/brand-guardian logo-usage check` |
| `ui-designer` | Interface design | `/ui-designer button primary react` |
| `ux-researcher` | User experience | `/ux-researcher usability mobile` |
| `visual-storyteller` | Visual narrative | `/visual-storyteller infographic data` |
| `whimsy-injector` | Delightful UX | `/whimsy-injector animation hover` |

### 📋 Project Management (3 commands)
| Command | Purpose | Example Usage |
|---------|---------|---------------|
| `experiment-tracker` | A/B test management | `/experiment-tracker feature-flag setup` |
| `project-shipper` | Release coordination | `/project-shipper deploy checklist` |
| `studio-producer` | Team coordination | `/studio-producer sprint-planning` |

### 🏢 Studio Operations (5 commands)
| Command | Purpose | Example Usage |
|---------|---------|---------------|
| `analytics-reporter` | Data insights | `/analytics-reporter metrics dashboard` |
| `finance-tracker` | Budget analysis | `/finance-tracker costs cloud` |
| `infrastructure-maintainer` | Infrastructure ops | `/infrastructure-maintainer scaling aws` |
| `legal-compliance-checker` | Compliance review | `/legal-compliance-checker gdpr audit` |
| `support-responder` | Customer support | `/support-responder ticket-analysis` |

### 🧪 Testing (6 commands)
| Command | Purpose | Example Usage |
|---------|---------|---------------|
| `api-tester` | API validation | `/api-tester endpoints auth` |
| `nexo-test-engineer` | Test strategy | `/nexo-test-engineer coverage report` |
| `performance-benchmarker` | Performance testing | `/performance-benchmarker load-test api` |
| `test-results-analyzer` | Test analysis | `/test-results-analyzer failures pattern` |
| `tool-evaluator` | Tool assessment | `/tool-evaluator testing-framework` |
| `workflow-optimizer` | Process improvement | `/workflow-optimizer ci-pipeline` |

### 🎭 Bonus (3 commands)
| Command | Purpose | Example Usage |
|---------|---------|---------------|
| `joker` | Tech humor | `/joker code-review funny` |
| `nexo-coach` | AI guidance | `/nexo-coach workflow optimization` |
| `studio-coach` | Team development | `/studio-coach retro facilitation` |

## 💡 Real-World Usage Examples

> **Note**: The following commands are executed inside the Google AI CLI TUI interface (after running `gemini` in your terminal).

### Security Audit Workflow
```bash
/security-analyst deps          # Scan dependencies
/security-analyst code          # Static analysis  
/security-analyst secrets       # Credential check
/code-reviewer security         # Review security patterns
```

### Feature Development Pipeline
```bash
/backend-architect api user-profile    # Design API
/frontend-developer component profile  # Build UI
/test-writer-fixer integration api     # Create tests
/code-reviewer diff HEAD~3             # Review changes
```

### Growth Experiment Setup
```bash
/trend-researcher social ai-tools      # Market research
/growth-hacker viral email 2-weeks     # Design experiment
/content-creator email-sequence launch # Content creation
/analytics-reporter conversion funnel  # Setup tracking
```

## 🔄 Workflows & Composition

> **Note**: Command composition using `&&` is executed within the Google AI CLI TUI interface.

Commands are designed for composition in development workflows:

```bash
# Code quality pipeline (executed in TUI)
/code-reviewer file src/ && /security-analyst code && /test-writer-fixer coverage

# Product launch sequence (executed in TUI)
/trend-researcher market-analysis && /feedback-synthesizer user-interviews && /sprint-prioritizer launch-features

# Infrastructure deployment (executed in TUI)
/devops-automator ci-setup && /sre monitoring && /security-analyst iac
```

## 🛠️ Custom Command Development

Use our optimized templates:

- **`templates/COMMAND_TEMPLATE.toml`** - Simple commands
- **`templates/COMMAND_TEMPLATE_ADVANCED.toml`** - Complex workflows

Key principles:
1. **Use `{{args}}`** for dynamic input
2. **Include `!{shell commands}`** for context
3. **Structure output** for automation
4. **Keep prompts focused** on specific tasks

## 📈 Performance & Optimization

### Context Efficiency
- **Smart file discovery** limits results (`| head -5`)
- **Conditional commands** prevent errors (`2>/dev/null`)
- **Focused queries** improve response speed

### Token Optimization
- **50-70% token reduction** vs. original commands
- **Focused prompts** eliminate unnecessary context
- **Structured output** improves parsing efficiency

## 🚦 Migration from v1.x

If you're upgrading from the previous version:

1. **All commands now use `{{args}}`** instead of manual parsing
2. **Shell integration** provides automatic context
3. **Simplified descriptions** for better `/help` output
4. **Structured output** replaces free-form responses

See `PROJECT_STATUS.md` for current development status and quality metrics.

## 📚 Additional Resources

- **`LEGAL_COMPLIANCE.md`** - Legal guidelines and trademark compliance
- **`PROJECT_STATUS.md`** - Current development status and quality metrics
- **`docs/TERMINAL_VS_TUI_GUIDE.md`** - Complete usage guide for both CLI modes
- **`templates/`** - Command templates for creating new commands
- **`VALIDATION_GUIDE.md`** - Testing and validation procedures
- [Google AI CLI Documentation](https://github.com/google-gemini/gemini-cli) - Official docs

## 📁 Repository Structure

```
nexo-agents/
├── README.md                    # Main documentation
├── LEGAL_COMPLIANCE.md          # Legal guidelines & compliance
├── PROJECT_STATUS.md            # Development status & quality metrics
├── VALIDATION_GUIDE.md          # Testing and validation procedures
├── commands/                    # All command files (public)
│   ├── engineering/             # Development and engineering commands
│   ├── design/                  # Design and UX commands
│   ├── marketing/               # Marketing and growth commands
│   ├── product/                 # Product management commands
│   ├── testing/                 # Testing and QA commands
│   ├── project-management/      # Project coordination commands
│   ├── studio-operations/       # Business operations commands
│   └── bonus/                   # Fun and utility commands
├── docs/                        # Additional documentation
│   └── TERMINAL_VS_TUI_GUIDE.md # Detailed usage guide
├── templates/                   # Command templates (public)
│   ├── COMMAND_TEMPLATE.toml
│   └── COMMAND_TEMPLATE_ADVANCED.toml
└── private/                     # Development files (excluded from git)
    ├── migration_scripts/
    ├── backups/
    └── logs/
```

---

**Version**: 2.0 (Google AI CLI Optimized)  
**Commands**: 44 production-ready agents  
**Compatibility**: Google AI CLI (`gemini-cli`) 2025+ with official TOML format  
**License**: MIT
