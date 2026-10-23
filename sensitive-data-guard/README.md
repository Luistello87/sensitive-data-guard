# Sensitive Data Guard for AI Coding Assistants 🛡️

A production-ready skill for **Claude Code**, **GitHub Copilot**, **Antigravity**, and agentic AI systems that prevents leakage of credentials, API keys, certificates, PII, and sensitive configurations into conversation logs, prompts, and git repositories.

---

## 🚀 Features

- **🚫 Blocked File Detection:** Forbids AI agents from reading or outputting `.env`, private keys (`.pem`, `.key`), keystores (`.jks`, `.p12`), and credential files.
- **🔒 Display-Only Redaction:** Automatically masks secrets, passwords, connection strings, and tokens when displaying logs or diffs in chat (`password=******`).
- **🛡️ 100% Non-Destructive:** Explicitly guarantees that credentials, configurations, and files on disk are **never modified or altered**.
- **👤 PII Shielding:** Mandates synthetic mock data for test suites and demonstrations rather than exposing real customer or employee records.
- **🌿 Git Leak Prevention:** Prompts verification against `.gitignore` before committing or staging files.

---

## 📦 Installation

### 1. GitHub Copilot Skills
Clone or download this repository, or copy the folder into your local skills directory:
```bash
git clone https://github.com/Luistello87/sensitive-data-guard.git ~/.copilot/skills/sensitive-data-guard
```

### 2. Antigravity & Gemini CLI
Copy `SKILL.md` into your global customization root:
```bash
# Windows
mkdir -p "$HOME\.gemini\config\skills\sensitive-data-guard"
cp SKILL.md "$HOME\.gemini\config\skills\sensitive-data-guard/SKILL.md"

# Linux / macOS
mkdir -p ~/.gemini/config/skills/sensitive-data-guard
cp SKILL.md ~/.gemini/config/skills/sensitive-data-guard/SKILL.md
```

### 3. Claude Code / Superpowers
Copy the `sensitive-data-guard` directory into your Superpowers skills directory:
```bash
cp -r sensitive-data-guard ~/.config/superpowers/skills/
```

---

## 🛠️ Usage

Once installed, your AI assistant will automatically activate this skill whenever you:
- Work with database configurations or `application.properties`.
- Inspect build logs, stack traces, or terminal outputs.
- Write tests involving user data or authentication.
- Stage or commit changes to git.

You can also explicitly instruct the agent:
> *"Follow the `sensitive-data-guard` skill to review this configuration before we commit."*

---

## 📄 License

MIT License. Free for personal and enterprise use.
