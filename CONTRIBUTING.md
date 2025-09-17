# Contributing to Nexo-Agents

> **⚖️ LEGAL DISCLAIMER**: By contributing to this project, you acknowledge this is a third-party tool for Google's AI CLI (`gemini-cli`). "Gemini" is a trademark of Google LLC. We are not affiliated with or endorsed by Google LLC.

## 🎉 Welcome Contributors!

We're excited you're interested in contributing to Nexo-Agents! This project provides professional-grade commands for Google's AI CLI, and we welcome contributions that help expand and improve our command library.

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
- [Getting Started](#getting-started)
- [Command Development Guidelines](#command-development-guidelines)
- [Pull Request Process](#pull-request-process)
- [Reporting Issues](#reporting-issues)
- [Community and Communication](#community-and-communication)

## 📜 Code of Conduct

This project adheres to a professional, inclusive, and welcoming environment. By participating, you agree to:

- **Be respectful** and constructive in all interactions
- **Focus on technical merit** rather than personal opinions
- **Help newcomers** and share knowledge generously
- **Maintain professional standards** in all communications
- **Respect intellectual property** rights of all parties

## 🤝 How Can I Contribute?

### Priority Contribution Areas

#### 🔥 High-Impact Contributions
- **New command categories** (e.g., DevOps, Data Science, Mobile)
- **Command improvements** with better context gathering
- **Documentation enhancements** for clarity and completeness
- **Testing and validation** procedures

#### 💡 Community Value Contributions
- **Usage examples** and real-world workflows
- **Template improvements** for easier command creation
- **Cross-platform testing** (Windows/Mac/Linux)
- **Performance optimizations** for faster execution

#### 🛠️ Technical Contributions
- **Shell command integrations** for better context
- **Error handling improvements** for robustness
- **Output format standardization** across commands
- **Integration testing** with Google AI CLI updates

### What We Don't Accept

❌ **Commands that violate Google's terms of service**  
❌ **Contributions with hardcoded credentials or sensitive data**  
❌ **Commands that suggest official Google endorsement**  
❌ **Changes that break existing command compatibility**  
❌ **Non-technical or marketing-focused contributions**

## 🚀 Getting Started

### Prerequisites

1. **Google AI CLI installed** and working (version 2025+)
2. **Basic TOML knowledge** for command file format
3. **Understanding of CLI/TUI differences** (see `docs/TERMINAL_VS_TUI_GUIDE.md`)
4. **Git and GitHub** familiarity for collaboration

### Development Setup

```bash
# Fork and clone the repository
git clone https://github.com/YOUR_USERNAME/nexo-agents.git
cd nexo-agents

# Install a test command to verify your setup
cp commands/engineering/security-analyst.toml ~/.gemini/commands/

# Test installation
gemini
# In TUI: /help (should show security-analyst)
# Test command: /security-analyst deps
```

### First Contribution Workflow

1. **Browse existing commands** in `commands/` directory
2. **Read templates** in `templates/` directory
3. **Review documentation** especially `docs/TERMINAL_VS_TUI_GUIDE.md`
4. **Pick a contribution area** from our priority list
5. **Start small** - improve existing commands before creating new ones

## 🎯 Command Development Guidelines

### Technical Requirements

#### ✅ Command File Structure
```toml
description = "Brief, clear description for /help menu"

prompt = """
You are a [specific role] expert specializing in [domain].

Task: {{args}}

## CONTEXT GATHERING
Project files: !{find . -name "*.ext" | head -5}
Dependencies: !{cat package.json requirements.txt 2>/dev/null | head -10}
Recent changes: !{git log --oneline -3 2>/dev/null || echo 'No git history'}

## TASK TYPES
- `type1` - Description of capability
- `type2` - Description of capability

## OUTPUT FORMAT
- **Analysis**: Clear problem identification
- **Solution**: Step-by-step implementation
- **Next Steps**: Follow-up recommendations

For unclear requests, ask for specific task type and scope.
"""
```

#### ✅ Quality Standards
- **Use `{{args}}`** for dynamic argument parsing
- **Include `!{shell commands}`** for project context gathering
- **Limit shell output** with `| head -5` or similar
- **Handle errors gracefully** with `2>/dev/null` or `|| echo`
- **Provide structured output** for automation compatibility
- **Focus prompts** on specific tasks, not role-playing

#### ✅ Documentation Requirements
- **Clear description** for `/help` menu display
- **Task types** section with specific capabilities
- **Context gathering** appropriate for the domain
- **Usage examples** in comments or documentation

### Command Categories

#### New Commands Should Fit These Categories
- **`commands/engineering/`** - Development, testing, infrastructure
- **`commands/design/`** - UI/UX, visual design, branding
- **`commands/marketing/`** - Content, growth, analytics
- **`commands/product/`** - Management, research, strategy
- **`commands/testing/`** - QA, automation, validation
- **`commands/project-management/`** - Coordination, planning
- **`commands/studio-operations/`** - Business operations, support
- **`commands/bonus/`** - Utilities, humor, coaching

### Template Usage

#### For Simple Commands
Use `templates/COMMAND_TEMPLATE.toml` for:
- Single-purpose commands
- Straightforward context gathering
- Standard output patterns

#### For Complex Commands
Use `templates/COMMAND_TEMPLATE_ADVANCED.toml` for:
- Multi-step workflows
- Complex context analysis
- Advanced shell integrations

## 🔄 Pull Request Process

### Before Submitting

1. **Test your command** thoroughly in both terminal and TUI modes
2. **Validate TOML syntax** (check for common errors)
3. **Follow naming conventions** (lowercase, hyphen-separated)
4. **Update documentation** if needed
5. **Check legal compliance** (no Google trademark violations)

### PR Requirements

#### ✅ Required Elements
- **Clear title** describing the change
- **Description** explaining the purpose and functionality
- **Testing evidence** showing command works correctly
- **Category placement** justification for new commands
- **Documentation updates** if adding new concepts

#### 📝 PR Template
```markdown
## Description
Brief description of changes and motivation.

## Type of Change
- [ ] New command
- [ ] Command improvement
- [ ] Documentation update
- [ ] Bug fix
- [ ] Template enhancement

## Testing
- [ ] Tested in terminal mode (`gemini --include`)
- [ ] Tested in TUI mode (after installation)
- [ ] Works on [Windows/Mac/Linux]
- [ ] Shell commands execute without errors
- [ ] Output format is structured and useful

## Checklist
- [ ] TOML syntax is valid
- [ ] Follows naming conventions
- [ ] Uses {{args}} for arguments
- [ ] Includes appropriate context gathering
- [ ] Documentation updated if needed
- [ ] No hardcoded credentials or sensitive data
```

### Review Process

1. **Automated checks** - TOML validation, naming conventions
2. **Technical review** - Command functionality and code quality
3. **Documentation review** - Clarity and completeness
4. **Testing verification** - Cross-platform compatibility
5. **Legal compliance** - Trademark and licensing review

We aim to review PRs within **48 hours** and provide constructive feedback.

## 🐛 Reporting Issues

### Bug Reports

Use our bug report template for:
- Commands not working as expected
- TOML syntax errors
- Documentation inaccuracies
- Cross-platform compatibility issues

#### 🐛 Bug Report Template
```markdown
## Bug Description
Clear description of what's not working.

## Steps to Reproduce
1. Step one
2. Step two
3. Step three

## Expected Behavior
What should happen.

## Actual Behavior
What actually happens.

## Environment
- OS: [Windows/Mac/Linux]
- Google AI CLI version: [run `gemini --version`]
- Command file: [path to .toml file]
- Usage mode: [terminal/TUI]

## Additional Context
Any other relevant information.
```

### Feature Requests

For new command ideas or enhancements:
- **Describe the use case** and target audience
- **Explain the value** and differentiation
- **Suggest implementation approach** if possible
- **Consider existing alternatives** and why they're insufficient

### Documentation Issues

Report documentation problems including:
- Unclear instructions
- Missing information
- Broken links
- Outdated examples

## 💬 Community and Communication

### Getting Help

- **GitHub Issues** - Technical questions and bug reports
- **GitHub Discussions** - General questions and community chat
- **Documentation** - Check `docs/` directory first
- **Templates** - Use provided templates as starting points

### Communication Guidelines

- **Search existing issues** before creating new ones
- **Use descriptive titles** for issues and PRs
- **Provide context** and examples when asking questions
- **Be patient and respectful** with maintainers and contributors
- **Help others** when you can share relevant knowledge

### Response Times

- **Issues**: We aim to respond within 24-48 hours
- **Pull Requests**: Initial review within 48 hours
- **Questions**: Community members often respond quickly

## 🏆 Recognition

### Contributor Recognition
- **All contributors** are acknowledged in project documentation
- **Significant contributions** receive special recognition
- **Consistent contributors** may be invited to maintainer roles
- **Quality improvements** are highlighted in release notes

### Ways to Stand Out
- **Thorough testing** across platforms
- **Clear documentation** and examples
- **Community support** helping other contributors
- **Innovative commands** that solve real problems

## 📚 Additional Resources

- **`docs/TERMINAL_VS_TUI_GUIDE.md`** - Essential usage patterns
- **`VALIDATION_GUIDE.md`** - Testing procedures
- **`templates/`** - Command creation templates
- **`LEGAL_COMPLIANCE.md`** - Legal guidelines and requirements
- [Google AI CLI Documentation](https://github.com/google-gemini/gemini-cli) - Official reference

---

## 🚀 Ready to Contribute?

1. **Fork the repository** on GitHub
2. **Create a feature branch** (`git checkout -b feature/amazing-command`)
3. **Make your changes** following our guidelines
4. **Test thoroughly** in both terminal and TUI modes
5. **Submit a pull request** with clear description

**Thank you for helping make Google AI CLI more powerful for everyone!** 🎉

---

**Questions?** Open an issue or check our documentation. We're here to help you succeed as a contributor.