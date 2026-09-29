# Sentiala Shield

**Sentiala Shield** is an AI-native, local-first defensive cybersecurity platform designed to analyze URLs and domains, correlate publicly available security intelligence, calculate explainable risk scores, and generate structured security reports.

The project focuses on **defensive security, threat intelligence, OSINT-style domain intelligence, phishing-risk assessment, and evidence-based analysis**.

## Core Capabilities

* 🔍 URL and domain analysis
* 🛡️ Defensive phishing-risk assessment
* 🌐 DNS-over-HTTPS intelligence
* 📋 RDAP/domain registration analysis
* 🚨 URLhaus malware-intelligence integration
* 🧠 Explainable risk scoring
* 📊 Evidence-based findings
* 💾 Local caching for repeated investigations
* 📚 Scan history
* 📄 Markdown security reports
* 🧾 Machine-readable JSON reports
* 🔌 Provider-based intelligence architecture
* 🔐 Local-first processing
* ⚙️ CLI-based workflow
* 🧪 Automated test suite
* 🧩 Extensible provider architecture
* 🛑 Permission boundaries for sensitive capabilities

## Architecture

Sentiala Shield is organized into several layers:

```text
Sentiala Shield
│
├── apps/
│   ├── browser-extension/
│   ├── dashboard/
│   └── desktop-agent/
│
├── services/
│   └── core/
│       └── sentiala_core/
│           ├── AI / analysis
│           ├── URL analyzer
│           ├── risk engine
│           ├── orchestrator
│           ├── report generation
│           ├── history
│           ├── cache
│           └── intelligence providers
│
├── tests/
│   ├── provider tests
│   ├── risk-engine tests
│   ├── URL-analysis tests
│   ├── report tests
│   ├── cache tests
│   └── orchestrator tests
│
├── docs/
├── scripts/
├── README.md
├── SECURITY.md
├── CONTRIBUTING.md
└── pyproject.toml
```

## Intelligence Providers

The current architecture supports multiple intelligence providers, including:

* Cloudflare DNS-over-HTTPS
* RDAP
* URLhaus / abuse.ch

Providers are isolated behind a common interface so additional defensive intelligence sources can be added without redesigning the core engine.

Planned future integrations can include additional threat-intelligence services where appropriate.

## Risk Analysis

Sentiala Shield does not simply return a binary result.

It combines available evidence and produces an explainable assessment containing:

* Risk score
* Confidence
* Evidence
* Finding severity
* Provider/source information
* Analysis details
* Intelligence availability
* Recommendations/context

This makes the result easier to understand and audit.

## Privacy and Safety

Sentiala Shield is designed around a **local-first defensive security model**.

The project explicitly separates permitted defensive intelligence operations from sensitive capabilities.

The project does not provide functionality intended for:

* Credential theft
* Unauthorized access
* Remote control
* Private-file harvesting
* Exploitation of third-party systems

Only analyze systems, URLs, and domains that you are authorized to investigate.

---

# Installation — Windows

## 1. Clone the repository

```powershell
git clone https://github.com/Tanish139/sentiala-shield.git
cd sentiala-shield
```

## 2. Create a virtual environment

```powershell
python -m venv .venv
```

## 3. Activate the virtual environment

```powershell
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks activation, you can instead run:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv\Scripts\Activate.ps1
```

## 4. Install the project and development dependencies

```powershell
python -m pip install --upgrade pip
pip install -e ".[dev]"
```

## 5. Verify the CLI

```powershell
sentiala --help
```

You should see commands including:

```text
scan
history
providers
permissions
```

## 6. Run the test suite

```powershell
pytest
```

The current project test suite contains **68 passing tests**.

## 7. Run a safe offline scan

```powershell
sentiala scan example.com --offline
```

## 8. Generate JSON output

```powershell
sentiala scan example.com --offline --json
```

## 9. Generate a Markdown report

```powershell
sentiala scan example.com --offline --out report.md
```

## 10. View scan history

```powershell
sentiala history
```

## 11. View available providers

```powershell
sentiala providers
```

## 12. View security permissions

```powershell
sentiala permissions
```

---

# Installation — Kali Linux

## 1. Clone the repository

```bash
git clone https://github.com/Tanish139/sentiala-shield.git
cd sentiala-shield
```

## 2. Create a virtual environment

```bash
python3 -m venv .venv
```

If `venv` is unavailable:

```bash
sudo apt update
sudo apt install python3-venv
```

Then create the environment again:

```bash
python3 -m venv .venv
```

## 3. Activate the virtual environment

```bash
source .venv/bin/activate
```

## 4. Upgrade pip

```bash
python -m pip install --upgrade pip
```

## 5. Install the project

```bash
pip install -e ".[dev]"
```

## 6. Verify the CLI

```bash
sentiala --help
```

## 7. Run the tests

```bash
pytest
```

## 8. Run a safe offline scan

```bash
sentiala scan example.com --offline
```

## 9. Generate JSON output

```bash
sentiala scan example.com --offline --json
```

## 10. Generate a Markdown report

```bash
sentiala scan example.com --offline --out report.md
```

## 11. View history

```bash
sentiala history
```

## 12. View providers

```bash
sentiala providers
```

## 13. View permissions

```bash
sentiala permissions
```

---

# Development

Run the complete test suite:

```bash
pytest
```

Install the package in editable mode:

```bash
pip install -e ".[dev]"
```

The project uses `pytest` for automated testing and follows a provider-based architecture for external intelligence sources.

## Example

```bash
sentiala scan example.com --offline
```

Example output:

```text
Sentiala Shield
Target: example.com

Risk: SAFE
Score: 0/100
Confidence: 50%

No relevant public intelligence found.
```

Actual confidence and intelligence availability may vary depending on whether the scan is offline or uses live providers.

---

# Project Status

**Current release:** `0.1.0`

**Development status:** Alpha

The core defensive analysis engine, provider architecture, caching, reporting, CLI, and automated test suite are implemented.

The `apps/` directories contain the foundations/documentation for future interface components such as the browser extension, dashboard, and desktop agent.

---

# Responsible Use

Sentiala Shield is intended for:

* Defensive cybersecurity research
* Security education
* Threat-intelligence analysis
* Domain/URL investigation
* Phishing-risk assessment
* Security engineering
* Authorized security operations

Only use Sentiala Shield against targets you own or are explicitly authorized to analyze.

---

# License

Sentiala Shield is released under the MIT License.
