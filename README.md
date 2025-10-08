# 🐕 Shelldog - Your Faithful Command Companion

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.7+](https://img.shields.io/badge/python-3.7+-blue.svg)](https://www.python.org/downloads/)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)

> **Never forget what you did. Always know where you've been. Your faithful shell companion has your back!**

Shelldog is like having a loyal puppy that silently follows your every command (the good, the bad, and the "I-have-no-idea-what-this-does" ones). It's a development tool that automatically tracks your shell commands while keeping sensitive information safe.

## 🎯 What Problem Does Shelldog Solve?

Ever found yourself thinking:

- 🤔 "What was that magic command I ran yesterday that fixed everything?"
- 😱 "Did I just accidentally leak an API key in my command history?"
- 🔍 "Which Python packages did I install for this project again?"
- 📝 "I wish I had a better record of my development workflow..."

**Shelldog to the rescue!** It's your silent development diary that works in the background, making sure you never lose track of your commands while keeping your secrets safe.

## ✨ Features

### 🐕‍🦺 Smart Command Tracking
- **Silent Operation**: Works in the background without interrupting your flow
- **Intelligent Filtering**: Logs development commands, ignores noise (`cd`, `ls`, etc.)
- **Virtual Environment Aware**: Separate logs for each project/venv
- **Cross-Platform**: Works with Bash and Zsh

### 🔒 Security First
- **Automatic Masking**: Sensitive data like passwords, API keys, and tokens are automatically masked
- **Export Protection**: Environment variables are logged but their values are hidden
- **No Data Leaks**: Your secrets stay secret while maintaining command context

### 🎨 Developer Experience
- **Fun & Friendly**: Enjoy delightful dog-themed messages and ASCII art
- **Easy Commands**: Simple CLI with intuitive subcommands
- **Project-Level Logging**: History files live with your project (like `requirements.txt`)
- **Rich History**: View, filter, and analyze your command history

### 📊 Insights & Analytics
- **Command Statistics**: See your most-used commands and patterns
- **Time-based Filtering**: View today's commands or tail recent entries
- **Project Context**: Understand your workflow across different environments

## 🚀 Quick Start

### Installation

```bash
pip install shelldog
```

### Basic Usage

```bash
# Start tracking in your project
shelldog follow

# Activate the hook in your current shell (IMPORTANT!)
source venv/.shelldog/shelldog_hook.sh

# Or use the one-liner for auto-activation
eval "$(shelldog follow -q)"
```

### See It in Action!

```bash
🐕 Woof! I'm watching you.

    Never forget what you did.
    Always know where you've been.
    I've got your back.

✓ Shelldog is now following your commands!

📝 Commands will be logged to:
   /path/to/your/project/shelldog_history.txt

🎉 Every great developer was once a beginner! 🌟
```

Now go about your development work:

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
export DATABASE_URL="postgresql://user:secret@localhost/db"
python manage.py migrate
python manage.py runserver
```

Check your history:

```bash
shelldog log

🐕 Shelldog History:

================================================================================
[2024-01-15 10:23:45] python3 -m venv venv
[2024-01-15 10:23:52] source venv/bin/activate
[2024-01-15 10:24:01] pip install -r requirements.txt
[2024-01-15 10:24:15] export DATABASE_URL=****
[2024-01-15 10:24:22] python manage.py migrate
[2024-01-15 10:24:30] python manage.py runserver
================================================================================

📊 Total entries: 6
🐕 *proud tail wag* I remembered everything!
```

## 🛠️ Complete Command Reference

### Core Commands

| Command | Description | Example |
|---------|-------------|---------|
| `shelldog follow` | Start tracking commands | `shelldog follow` |
| `shelldog log` | View command history | `shelldog log --today` |
| `shelldog status` | Check tracking status | `shelldog status` |
| `shelldog stop` | Stop tracking | `shelldog stop` |
| `shelldog clear` | Clear history | `shelldog clear` |

### Fun Commands 🎉

| Command | What It Does | Response Example |
|---------|--------------|------------------|
| `shelldog bark` | Make Shelldog bark! | `🐕 BORK! Time to chase some bugs!` |
| `shelldog treat` | Give a virtual treat | `🐕 *happy dance* TREAT! My favorite!` |
| `shelldog goodboy` | Praise Shelldog | `🐕 *tail wagging* I'M A GOOD BOY!` |

### Advanced Usage

```bash
# Show only last 10 commands
shelldog log --tail 10

# Show only today's commands
shelldog log --today

# Check if everything is working
shelldog status

# Get command statistics
shelldog stats

# Quiet mode for scripting
eval "$(shelldog follow -q)"
```

## 🔧 How It Works

### Architecture

```
Your Shell → Shell Hook → Shelldog Logger → Project History File
     │             │              │                 │
     │             │              │                 └── shelldog_history.txt
     │             │              └── Mask sensitive data
     │             └── venv/.shelldog/shelldog_hook.sh
     └── Intercepts commands via DEBUG trap (Bash) or preexec (Zsh)
```

### Security Features

Shelldog automatically masks:
- 🔑 Environment variables: `export API_KEY=secret` → `export API_KEY=****`
- 🗝️ Passwords: `--password hunter2` → `--password ****`
- 🔐 Tokens: `--token ghp_abc123` → `--token ****`
- 🎫 API keys: `--api-key sk_live_abc123` → `--api-key ****`

### Virtual Environment Support

When you're in a virtual environment:
- Hook scripts are stored in `venv/.shelldog/`
- Command history is stored at project level: `./shelldog_history.txt`
- Each project maintains its own independent history

## 🐾 Use Cases

### 🎓 Learning & Documentation
Perfect for tutorials, workshops, or when learning new tools. Shelldog automatically documents your learning journey.

### 🔧 Debugging & Troubleshooting
Track the exact sequence of commands that led to a bug or solution. Never lose that "magic fix" again!

### 🚀 Onboarding & Knowledge Sharing
New team members can see the common commands and workflows used in your project.

### 📚 Personal Development Journal
Keep a record of your growth as a developer and the tools you master over time.

## 🛡️ Privacy & Security

### What We Log
- Command names and arguments (with sensitive data masked)
- Timestamps
- Project context

### What We NEVER Log
- Raw passwords, keys, or tokens
- File contents
- Private user data
- Network traffic

### Data Storage
All data stays locally on your machine. No telemetry, no cloud storage, no funny business.

## 🐕‍🦺 For Contributors

We welcome fellow dog lovers and developers! Here's how you can help:

### Development Setup

```bash
# Fork and clone the repository
git clone https://github.com/your-username/shelldog.git
cd shelldog

# Set up development environment
python3 -m venv venv
source venv/bin/activate
pip install -e ".[dev]"

# Test your changes
pytest tests/
```

### Areas for Contribution
- 🐛 Bug fixes and improvements
- 🎨 Additional shell support (Fish, PowerShell, etc.)
- 📊 Enhanced analytics and insights
- 🔌 Plugin system for custom command handlers
- 🎯 More intelligent command filtering
- 🌐 Community translations for dog phrases

### Code of Conduct
We're a friendly pack! Please be respectful and inclusive in all interactions. Remember: every good boy and girl deserves treats and praise! 🦴

## 📊 Example Workflow

```bash
# Start a new project
mkdir my-awesome-project
cd my-awesome-project

# Initialize Shelldog
shelldog follow
eval "$(shelldog follow -q)"

# Develop as usual
python3 -m venv venv
source venv/bin/activate
pip install flask pandas numpy
export FLASK_SECRET="super-secret-key"
python app.py

# Later, review your workflow
shelldog log --today

# Share your setup with teammates
cat shelldog_history.txt
```

## 🎉 Community & Support

### Get Help
- 📖 Check the [documentation](https://github.com/your-username/shelldog/wiki)
- 🐛 [Report issues](https://github.com/your-username/shelldog/issues)
- 💡 [Request features](https://github.com/your-username/shelldog/issues)
- 🐕 Share your Shelldog stories with #ShelldogOSS

### Show Your Support
If Shelldog has been a good boy and helped your workflow:
- ⭐ Star the repository
- 🐦 Share on social media
- 🔗 Use in your projects
- 🐛 Contribute code or documentation

## 📄 License

MIT License - feel free to use Shelldog in your projects! See [LICENSE](LICENSE) for details.

## 🐕 Final Words from Shelldog

> *wagging tail* 
>
> "I'm just a simple dog trying to make the development world a better place. I don't ask for much - just an occasional `shelldog treat` and maybe a `shelldog goodboy` when I help you find that lost command.
>
> Remember: I'm always here, silently watching, ready to help you track your journey from 'Hello World' to production deployment.
>
> Woof woof! 🐾
>
> — Your faithful development companion"

---

**Ready to let Shelldog watch your back?** 

```bash
pip install shelldog
cd your-project
shelldog follow
```

Welcome to the pack! 🐕‍🦺❤️

# 🐕 Shelldog
