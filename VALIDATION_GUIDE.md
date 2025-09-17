# Google AI CLI Integration Validation Guide

> **⚖️ LEGAL DISCLAIMER**: This validation guide covers third-party commands for Google's AI CLI tool (`gemini-cli`). "Gemini" is a trademark of Google LLC. We are not affiliated with or endorsed by Google LLC.

## Pre-Validation Checklist

Before testing the Nexo-Agents commands, ensure your environment meets these requirements:

### ✅ Google AI CLI Installation
```bash
# Check Google AI CLI version (should be 2025+)
gemini --version

# Verify command discovery paths
ls ~/.gemini/commands/     # Global commands
ls .gemini/commands/       # Project commands (if exists)
```

### ✅ TOML Format Validation
```bash
# Verify TOML syntax for all commands
find nexo-agents -name "*.toml" -exec echo "Checking: {}" \; -exec toml-test {} \;
```

## 🧪 Command Testing Protocol

### 1. Basic Command Discovery
Test that Google AI CLI can discover and load commands:

#### Terminal Commands (executed outside CLI)
```bash
# Test on-demand loading (terminal command)
gemini --include nexo-agents/engineering/security-analyst.toml "/security-analyst deps"
```

#### TUI Commands (executed inside CLI interface)
```bash
# First, install the command globally
cp nexo-agents/engineering/security-analyst.toml ~/.gemini/commands/

# Then start the CLI and test discovery
gemini
# Inside the TUI interface:
/help
# Look for security-analyst in the command list
```

### 2. Argument Parsing Validation
Test `{{args}}` functionality with various input patterns:

#### Terminal Mode (one-time execution)
```bash
# Simple arguments (terminal command)
gemini --include nexo-agents/engineering/security-analyst.toml "/security-analyst deps scan"

# Complex arguments with spaces (terminal command)
gemini --include nexo-agents/engineering/code-reviewer.toml "/code-reviewer file 'src/main.py' quality"

# No arguments (should handle gracefully) (terminal command)
gemini --include nexo-agents/engineering/ai-engineer.toml "/ai-engineer"
```

#### TUI Mode (interactive session)
```bash
# Start the CLI
gemini

# Inside TUI, test various argument patterns:
/security-analyst deps scan
/code-reviewer file src/main.py quality
/ai-engineer
```

### 3. Shell Command Integration Testing
Verify `!{command}` context gathering works:

```bash
# Test in a Python project
cd /path/to/python/project
gemini --include nexo-agents/engineering/security-analyst.toml "/security-analyst deps"
# Should discover requirements.txt, pyproject.toml, etc.

# Test in a Node.js project  
cd /path/to/node/project
gemini --include nexo-agents/engineering/ai-engineer.toml "/ai-engineer llm setup"
# Should discover package.json, node_modules, etc.

# Test in a Git repository
cd /path/to/git/repo
gemini --include nexo-agents/engineering/code-reviewer.toml "/code-reviewer diff"
# Should discover git history, recent commits, etc.
```

### 4. Cross-Platform Compatibility
Test on different operating systems:

#### Windows (PowerShell)
```powershell
# Copy command to Windows Gemini directory
Copy-Item nexo-agents\engineering\security-analyst.toml $env:USERPROFILE\.gemini\commands\

# Test execution
gemini "/security-analyst deps scan"
```

#### macOS/Linux (Bash/Zsh)
```bash
# Copy command to Unix Gemini directory
cp nexo-agents/engineering/security-analyst.toml ~/.gemini/commands/

# Test execution
gemini "/security-analyst deps scan"
```

## 🔍 Validation Test Cases

### Test Case 1: Security Analysis Workflow
```bash
# Setup test environment
mkdir test-project && cd test-project
echo "requests==2.25.0" > requirements.txt
echo "flask==1.0.0" >> requirements.txt

# Test dependency scanning
gemini --include ../nexo-agents/engineering/security-analyst.toml "/security-analyst deps"

# Expected behavior:
# - Should discover requirements.txt via !{cat requirements.txt}
# - Should identify vulnerable packages
# - Should provide CVSS scores and remediation steps
```

### Test Case 2: Code Review Process
```bash
# Setup test environment with Git
git init test-repo && cd test-repo
echo "def bad_function():\n    password = 'hardcoded123'\n    return password" > main.py
git add . && git commit -m "Add insecure code"

# Test code review
gemini --include ../nexo-agents/engineering/code-reviewer.toml "/code-reviewer file main.py"

# Expected behavior:
# - Should discover main.py via !{find . -name "*.py"}
# - Should identify hardcoded credentials
# - Should suggest security improvements
```

### Test Case 3: AI Engineering Support
```bash
# Setup Python AI project
mkdir ai-project && cd ai-project
echo "openai==1.0.0\nlangchain==0.1.0" > requirements.txt

# Test AI implementation guidance
gemini --include ../nexo-agents/engineering/ai-engineer.toml "/ai-engineer rag vector-store"

# Expected behavior:
# - Should discover AI dependencies via !{cat requirements.txt | grep -E "(openai|langchain)"}
# - Should provide RAG implementation guidance
# - Should suggest vector database options
```

### Test Case 4: UI Design Generation
```bash
# Setup React project structure
mkdir ui-project && cd ui-project
mkdir components && echo '{"dependencies": {"react": "^18.0.0"}}' > package.json

# Test UI component generation
gemini --include ../nexo-agents/design/ui-designer.toml "/ui-designer component button react"

# Expected behavior:
# - Should discover React via !{cat package.json}
# - Should generate React component code
# - Should include Tailwind/CSS styling
```

## ⚡ Performance Validation

### Response Time Testing
```bash
# Measure command execution time
time gemini --include nexo-agents/engineering/security-analyst.toml "/security-analyst deps"

# Target: < 5 seconds for context gathering + response
```

### Token Efficiency Testing
```bash
# Compare old vs new command token usage
# Old format: ~800-1200 tokens
# New format: ~300-500 tokens (50-70% reduction)
```

### Context Gathering Efficiency
```bash
# Test shell command limits work correctly
ls -la | wc -l  # Should be manageable number via head/tail limits
```

## 🐛 Error Handling Validation

### Invalid Arguments
```bash
# Test with malformed arguments
gemini --include nexo-agents/engineering/security-analyst.toml "/security-analyst invalid-command"

# Expected: Clear error message explaining valid options
```

### Missing Dependencies
```bash
# Test in empty directory
mkdir empty-test && cd empty-test
gemini --include ../nexo-agents/engineering/security-analyst.toml "/security-analyst deps"

# Expected: Graceful handling of missing files
```

### Shell Command Failures
```bash
# Test when shell commands fail (e.g., no git history)
mkdir no-git && cd no-git
gemini --include ../nexo-agents/engineering/code-reviewer.toml "/code-reviewer diff"

# Expected: Fallback behavior, not command failure
```

## ✅ Success Criteria

Commands pass validation if they meet ALL criteria:

### Functional Requirements
- [ ] Command loads successfully via `--include`
- [ ] Command appears in `/help` when installed
- [ ] `{{args}}` parsing works with various input patterns
- [ ] Shell commands `!{command}` execute without errors
- [ ] Context gathering discovers relevant project files
- [ ] Output is structured and actionable

### Performance Requirements
- [ ] Response time < 10 seconds on typical projects
- [ ] Token usage 50-70% less than original format
- [ ] Shell commands complete within 2 seconds
- [ ] Memory usage remains reasonable (< 100MB)

### Compatibility Requirements
- [ ] Works on Windows, macOS, and Linux
- [ ] Compatible with Gemini CLI 2025+
- [ ] No conflicts with existing Gemini CLI commands
- [ ] Graceful error handling for edge cases

### User Experience Requirements
- [ ] Clear, actionable output
- [ ] Helpful error messages
- [ ] Intuitive argument patterns
- [ ] Consistent behavior across commands

## 📊 Validation Report Template

```markdown
## Validation Report: [Command Name]

**Date**: [YYYY-MM-DD]
**Tester**: [Name]
**Environment**: [OS, Gemini CLI version]

### Test Results
- [ ] Basic discovery: PASS/FAIL
- [ ] Argument parsing: PASS/FAIL  
- [ ] Shell integration: PASS/FAIL
- [ ] Error handling: PASS/FAIL
- [ ] Performance: PASS/FAIL

### Issues Found
1. [Issue description]
2. [Issue description]

### Recommendations
1. [Recommendation]
2. [Recommendation]

**Overall Status**: APPROVED/NEEDS_WORK
```

## 🚀 Final Validation Steps

Before marking the migration complete:

1. **Run full test suite** on all 44 commands
2. **Test on 3 different operating systems**
3. **Validate with real project environments**
4. **Performance benchmark** against original commands
5. **User acceptance testing** with actual workflows
6. **Documentation review** for accuracy and completeness

**Target**: 100% command compatibility with zero breaking changes to core functionality.