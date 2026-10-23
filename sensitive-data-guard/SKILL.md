---
name: sensitive-data-guard
description: Prevent exposure of secrets, credentials, PII, and production sensitive data in agent context, logs, and code
when_to_use: when handling configuration files, inspecting logs, working with authentication, writing test data, or committing code
version: 1.0.0
---

# Sensitive Data & Privacy Guard

## Objective
Prevent sensitive information (API keys, database passwords, private keys, certificates, PII, and production credentials) from leaking into prompts, tool outputs, version control, or generated code.

---

## 1. Blocked Files & Directories
Never read, dump, display, or stage the following files under any circumstances:
- **Environment & config secrets:** `.env`, `.env.*`, `*secret*`, `*credentials*`, `application-prod.properties`, `application-secrets.yml`.
- **Certificates & Keys:** `*.pem`, `*.key`, `*.p12`, `*.jks`, `*.keystore`, `id_rsa`, `id_ed25519`.
- **Auth tokens:** `~/.aws/credentials`, `~/.azure/`, `~/.ssh/`, `~/.git-credentials`, `npmrc` with auth tokens.

If a task requires checking whether a property exists in one of these files:
- Check only key names or existence (e.g. `Select-String -Pattern "^[A-Za-z_]+" -Path .env`), never display the secret values.

---

## 2. Redaction & Masking Rules (Display Only)
**CRITICAL SAFETY RULE: NEVER edit, replace, or overwrite passwords or credentials inside actual configuration files on disk.** Masking applies STRICTLY to text printed in chat responses and terminal displays to prevent credential leakage into conversation logs.

When printing terminal logs, diffs, or example configs:
- **Passwords / Secrets:** `password=******` or `[REDACTED_PASSWORD]`
- **API Keys / JWTs:** `Bearer eyJ...[REDACTED]` or `[REDACTED_API_KEY]`
- **Database URLs:** `jdbc:postgresql://[HOST]:[PORT]/[DB]?user=[USER]&password=[REDACTED]`
- **Personally Identifiable Information (PII):** Use synthetic test data (e.g. `user@example.com`, `John Doe`, `555-0100`). Never use real person data from production databases or logs.

---

## 3. Code Generation & Refactoring Rules
- **Never hardcode secrets:** Never put plaintext passwords, API keys, or connection strings into source files (`.java`, `.properties`, `.json`, etc.).
- **Enforce externalized configuration:** Use environment variables (`${DB_PASSWORD}`) or vault references.
- **Test Data Hygiene:** In unit and integration tests, use mock generators (e.g. Bogus/Faker, UUIDs) and never paste real customer or employee records into test fixtures.

---

## 4. Git & Pre-Commit Shielding
Before running any commit or staging operation:
- Verify that secret files are listed in `.gitignore`.
- Alert the user immediately if unmasked secrets are discovered in staged diffs.
