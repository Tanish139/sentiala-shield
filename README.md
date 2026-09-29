# 🛡️ Sentiala Shield

**Sentiala Shield** is an AI-native, evidence-based defensive cybersecurity and threat-intelligence platform designed to analyze URLs, domains, and IP addresses, correlate public security intelligence, calculate explainable risk, maintain local investigation history, and generate structured security reports.

The project follows a **local-first and privacy-conscious architecture**. Its core analysis engine is designed to work even when live intelligence providers are unavailable, while clearly distinguishing between verified intelligence and locally derived or unverified results.

> **Project status:** Alpha / Active Development
> **License:** MIT
> **Primary language:** Python
> **Supported platforms:** Windows, Linux, Kali Linux
> **Python:** 3.10+

---

## 🚀 What Sentiala Shield Does

Sentiala Shield provides a command-line security investigation workflow for suspicious or unknown:

* URLs
* Domains
* IP addresses
* Potential phishing destinations
* Potential malware-related infrastructure
* Suspicious domain characteristics
* Public threat-intelligence indicators

The system combines multiple analysis layers instead of relying on a single security signal.

### Core capabilities

* 🔎 URL and domain analysis
* 🌐 DNS intelligence
* 🏢 RDAP/domain registration intelligence
* 🦠 URLhaus malware intelligence integration
* 🧠 AI-oriented analysis architecture
* ⚖️ Explainable risk scoring
* 📊 Confidence scoring
* 🧾 Structured security reports
* 💾 Local investigation history
* ⚡ Local caching
* 🔐 Permission-aware AI architecture
* 📴 Offline analysis mode
* 🧪 Automated test suite
* 🖥️ Windows support
* 🐧 Linux/Kali Linux support
* 🔌 Provider-based intelligence architecture

---

# 🏗️ Architecture

The project is organized around a modular core:

```text
sentiala-shield/
│
├── apps/
│   ├── browser-extension/
│   ├── desktop-agent/
│   └── dashboard/
│
├── docs/
│   └── ARCHITECTURE.md
│
├── scripts/
│   └── demo.py
│
├── services/
│   └── core/
│       └── sentiala_core/
│           ├── ai.py
│           ├── cache.py
│           ├── cli.py
│           ├── history.py
│           ├── orchestrator.py
│           ├── report.py
│           ├── risk_engine.py
│           ├── types.py
│           ├── url_analyzer.py
│           │
│           └── providers/
│               ├── base.py
│               ├── doh.py
│               ├── rdap.py
│               └── urlhaus.py
│
├── tests/
│   ├── fixtures/
│   ├── conftest.py
│   ├── test_cache.py
│   ├── test_orchestrator.py
│   ├── test_providers.py
│   ├── test_report.py
│   ├── test_risk_engine.py
│   └── test_url_analyzer.py
│
├── .env.example
├── .gitignore
├── CHANGELOG.md
├── CONTRIBUTING.md
├── LICENSE
├── pyproject.toml
├── README.md
└── SECURITY.md
```

---

# 🧠 Analysis Pipeline

A typical investigation follows this general flow:

```text
Target URL / Domain / IP
          │
          ▼
    URL Analyzer
          │
          ▼
   Scan Context Creation
          │
          ▼
     Provider Layer
     ┌────┼─────┐
     ▼    ▼     ▼
    DNS  RDAP  URLhaus
     │    │     │
     └────┼─────┘
          ▼
   Evidence Collection
          │
          ▼
     Risk Engine
          │
          ▼
  Confidence Calculation
          │
          ▼
 Structured Security Report
          │
          ├── Terminal
          ├── JSON
          └── Markdown
```

This architecture allows additional intelligence providers and analysis modules to be added without rewriting the complete system.

---

# 🛡️ Risk Analysis

Sentiala Shield uses an explainable scoring model rather than simply returning:

> SAFE / DANGEROUS

The system considers available evidence and produces:

* Risk score
* Confidence score
* Findings
* Evidence classification
* Provider availability
* Investigation metadata
* Explanatory notes

This is important because **absence of threat intelligence does not automatically prove that a website is safe**.

For example, an offline scan may return a low risk score while explicitly indicating that live intelligence was not verified.

---

# 🔬 Intelligence Providers

Current provider architecture includes:

### Cloudflare DNS-over-HTTPS

Used for DNS resolution and related domain intelligence.

### RDAP

Used for domain registration information and registration-age-related analysis.

### URLhaus

Used for public malware URL/host intelligence from abuse.ch.

The provider system is intentionally modular so additional services can be integrated later.

Planned integrations can include services such as:

* Google Safe Browsing
* PhishTank
* VirusTotal
* Additional DNS intelligence
* Additional reputation feeds

These are **planned/extendable integrations and should not be interpreted as currently active unless configured and tested in the repository.**

---

# 📴 Offline Mode

Sentiala Shield supports:

```bash
sentiala scan example.com --offline
```

Offline mode is useful when:

* Internet access is unavailable
* Testing the local analysis engine
* Running deterministic demonstrations
* Testing the application without external providers
* Protecting against unnecessary external requests

Offline results clearly indicate when live intelligence has not been verified.

---

# 🧾 Report Generation

Sentiala Shield can generate structured output.

### Terminal

```bash
sentiala scan example.com --offline
```

### JSON

```bash
sentiala scan example.com --offline --json
```

### Markdown report

```bash
sentiala scan example.com --offline --out report.md
```

The report system is designed to preserve evidence and explain why a result was produced.

---

# 💾 Investigation History

Previous investigations can be stored locally.

View history with:

```bash
sentiala history
```

This provides a basic local investigation trail that can later be expanded into a larger case-management system.

---

# 🔐 Permission Model

Sentiala Shield includes a permission-oriented security model for AI/tool integration.

Current categories include:

```text
URL_ANALYSIS
DOMAIN_LOOKUP
DNS_RESOLUTION
THREAT_INTEL_LOOKUP
```

Restricted capabilities include sensitive operations such as:

```text
PRIVATE_FILE_ACCESS
CREDENTIAL_ACCESS
REMOTE_CONTROL
```

The purpose is to ensure that future AI capabilities operate within explicit boundaries instead of receiving unrestricted system access.

---

# 🧪 Testing

The project includes automated tests covering:

* URL analysis
* Risk scoring
* Provider behavior
* DNS intelligence
* RDAP intelligence
* URLhaus integration
* Caching
* Investigation history
* Report generation
* Orchestration

Run the complete test suite:

```bash
pytest
```

The current validated test suite reached:

```text
68 passed
```

---

# 🧩 Problems Encountered During Development

Building and testing Sentiala Shield exposed several practical issues. These were fixed during development and are documented here so other developers can reproduce the setup without repeating the same mistakes.

---

## 1. Incorrect project directory

### Problem

The project was initially run from an incorrect/incomplete directory.

This resulted in errors such as:

```text
does not appear to be a Python project:
neither setup.py nor pyproject.toml found
```

### Cause

The actual project files were inside the complete project directory, while the terminal was pointing at a different/incomplete folder.

### Solution

Verify that the directory contains:

```text
pyproject.toml
services/
tests/
README.md
```

Then run:

```bash
pip install -e ".[dev]"
```

---

# 2. Missing pytest

### Problem

Running:

```bash
pytest
```

initially failed because pytest was not installed.

### Solution

Install development dependencies:

```bash
pip install -e ".[dev]"
```

The `pyproject.toml` file defines:

```toml
[project.optional-dependencies]
dev = ["pytest>=8"]
```

After installation:

```bash
pytest
```

---

# 3. Test fixture path problem

### Problem

The test suite initially produced multiple failures/errors because test fixtures could not be located correctly.

The incorrect path logic used:

```python
FIXTURES = Path(__file__) / "fixtures"
```

### Cause

`Path(__file__)` points to the test file itself, not its containing directory.

### Solution

The fixture path was corrected to:

```python
FIXTURES = Path(__file__).parent / "fixtures"
```

After the correction, the complete test suite successfully reached:

```text
68 passed
```

---

# 4. Incorrectly entering Python code into PowerShell

### Problem

Python code such as:

```python
from pathlib import Path
```

was accidentally entered directly into PowerShell.

### Cause

Python source code belongs inside `.py` files or inside a Python interpreter, not directly in a normal PowerShell command prompt.

### Correct approach

Edit the appropriate Python file in VS Code and save it.

Then run:

```powershell
pytest
```

from the project directory.

---

# 5. Missing Python build package

### Problem

Running:

```bash
python -m build
```

failed because the `build` package was not installed.

### Solution

For normal development and testing, the project can be installed directly with:

```bash
pip install -e ".[dev]"
```

If package-building is required later, install the build tooling separately:

```bash
pip install build
```

Then:

```bash
python -m build
```

---

# 6. URLhaus live API reliability

### Problem

Live URLhaus access was not always available.

The application encountered provider-side/API response problems, including JSON decoding failures and configuration-related warnings.

### Solution

The URLhaus provider was made defensive:

* Network exceptions are handled
* Invalid JSON responses are handled
* Unexpected API statuses are handled
* Provider failure does not crash the complete scan
* The scanner can continue using other available intelligence
* The final report can indicate provider availability

This follows an important security principle:

> A failure in one external intelligence source should not bring down the complete investigation pipeline.

---

# 7. Live intelligence versus offline analysis

### Problem

A low-risk result could be misunderstood as proof that a domain is completely safe.

### Solution

Sentiala Shield separates:

* Risk
* Confidence
* Evidence
* Provider availability
* Live verification status

For example:

```text
Risk: 0/100
Confidence: 50%
```

does **not** mean:

> This website is guaranteed safe.

Instead, the report can indicate that live threat intelligence was not verified.

This distinction helps prevent false confidence.

---

# 8. Kali Linux ZIP structure problem

### Problem

The Kali environment initially contained an incomplete project directory.

The ZIP itself contained the complete project inside a nested:

```text
sentiala-shield/
```

directory.

### Solution

The project was extracted correctly and verified to contain:

```text
apps/
docs/
pyproject.toml
scripts/
services/
tests/
README.md
```

After recreating the virtual environment:

```bash
rm -rf .venv
python3 -m venv .venv
source .venv/bin/activate
```

the project installed successfully using:

```bash
pip install -e ".[dev]"
```

---

# 9. Kali Python environment

The project was tested in a Kali Linux virtual environment using a newer Python runtime.

The installation successfully resolved the required dependencies including:

* requests
* pytest
* Sentiala Shield itself

The recommended approach is always to use an isolated virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

---

# 10. Generated test artifacts

### Problem

A generated test report:

```text
test-report.md
```

appeared in Git tracking.

### Solution

Generated runtime/test files should not be committed.

The artifact was removed from Git tracking and the working tree was cleaned.

The `.gitignore` also excludes generated runtime files such as:

```text
.pytest_cache/
*.jsonl
intel_cache.json
.venv/
.env
```

---

# 🖥️ Windows Installation

Clone the repository:

```powershell
git clone https://github.com/Tanish139/sentiala-shield.git
cd sentiala-shield
```

Create a virtual environment:

```powershell
python -m venv .venv
```

Activate it:

```powershell
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks activation:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv\Scripts\Activate.ps1
```

Upgrade pip:

```powershell
python -m pip install --upgrade pip
```

Install Sentiala Shield:

```powershell
pip install -e ".[dev]"
```

Verify:

```powershell
sentiala --help
```

Run tests:

```powershell
pytest
```

Run an offline scan:

```powershell
sentiala scan example.com --offline
```

Run JSON output:

```powershell
sentiala scan example.com --offline --json
```

Generate a report:

```powershell
sentiala scan example.com --offline --out report.md
```

View history:

```powershell
sentiala history
```

View providers:

```powershell
sentiala providers
```

View permissions:

```powershell
sentiala permissions
```

---

# 🐧 Kali Linux Installation

Clone the repository:

```bash
git clone https://github.com/Tanish139/sentiala-shield.git
cd sentiala-shield
```

Create the virtual environment:

```bash
python3 -m venv .venv
```

If `venv` is unavailable:

```bash
sudo apt update
sudo apt install python3-venv
```

Then:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Upgrade pip:

```bash
python -m pip install --upgrade pip
```

Install development dependencies:

```bash
pip install -e ".[dev]"
```

Verify installation:

```bash
sentiala --help
```

Run tests:

```bash
pytest
```

Run an offline scan:

```bash
sentiala scan example.com --offline
```

Run JSON analysis:

```bash
sentiala scan example.com --offline --json
```

Generate a report:

```bash
sentiala scan example.com --offline --out report.md
```

View providers:

```bash
sentiala providers
```

View permissions:

```bash
sentiala permissions
```

View investigation history:

```bash
sentiala history
```

---

# 🌐 Example Investigation

Example:

```bash
sentiala scan https://www.bjemschool.org/
```

For an offline test:

```bash
sentiala scan https://www.bjemschool.org/ --offline
```

JSON:

```bash
sentiala scan https://www.bjemschool.org/ --json
```

Markdown:

```bash
sentiala scan https://www.bjemschool.org/ --out bjemschool-report.md
```

The result should be interpreted according to the evidence and confidence reported by Sentiala Shield. A scan is an analytical aid, not a guarantee that a website is completely safe or malicious.

---

# 📊 Current CLI

Sentiala Shield currently exposes:

```text
sentiala scan
sentiala history
sentiala providers
sentiala permissions
```

Check the CLI:

```bash
sentiala --help
```

Scan options:

```bash
sentiala scan --help
```

---

# 🔮 Future Development

The project architecture is designed to grow into a broader defensive security platform.

Potential future components include:

### Browser Extension

Real-time URL analysis while browsing.

### Desktop Agent

Local security monitoring and investigation support.

### Security Dashboard

Visual investigation interface with:

* Risk dashboards
* Investigation timelines
* Evidence views
* Provider status
* Historical scans
* Threat-intelligence correlation

### Advanced AI Layer

Future AI capabilities can assist with:

* Evidence summarization
* Explainable security analysis
* Report generation
* Investigation assistance
* Natural-language queries
* Correlation of multiple findings

AI capabilities will remain subject to explicit permission boundaries.

---

# 🔒 Privacy & Security Philosophy

Sentiala Shield is designed around:

* Local-first processing
* Minimal external data sharing
* Explicit provider communication
* Evidence-based analysis
* Permission-controlled AI capabilities
* No credential access
* No unrestricted remote control
* No unnecessary private-file access

Only the information required for a configured analysis provider should be sent to that provider.

Users should review provider policies and configuration before enabling live integrations.

---

# ⚠️ Responsible Use

Sentiala Shield is intended for:

* Defensive security research
* Website security analysis
* Phishing investigation
* Threat intelligence
* OSINT
* Security education
* Authorized security testing

Do not use the project to:

* Attack systems without authorization
* Steal credentials
* Bypass authentication
* Access private systems without permission
* Conduct unauthorized surveillance
* Distribute malware
* Perform destructive actions

The project is designed as a **defensive security tool**.

---

# 📌 Project Status

### Implemented and tested

* URL/domain analysis
* DNS provider
* RDAP provider
* URLhaus provider architecture
* Risk engine
* Confidence calculation
* Evidence model
* Local cache
* Investigation history
* Report generation
* JSON output
* Markdown output
* CLI
* Permission model
* Offline mode
* Automated test suite
* Windows installation
* Kali Linux installation

### Foundation / future development

* Browser extension
* Desktop agent
* Web dashboard
* Expanded AI capabilities
* Additional threat-intelligence providers
* Advanced correlation
* More automated investigation workflows

---

# 🧪 Validation

The core project was validated through automated testing.

Current recorded test result:

```text
68 passed
```

The project was also manually verified through CLI operations including:

```bash
sentiala --help
sentiala scan example.com --offline
sentiala scan example.com --offline --json
sentiala providers
sentiala permissions
sentiala history
```

---

# 📜 License

Sentiala Shield is released under the MIT License.

See:

```text
LICENSE
```

for the complete license text.

---

## ⭐ Why Sentiala Shield?

Sentiala Shield is built around a simple principle:

> **Security decisions should be based on evidence, not blind confidence.**

Instead of hiding uncertainty, the platform attempts to expose:

* What was checked
* Which providers responded
* What evidence was found
* How the risk was calculated
* How confident the system is
* What could not be verified

This makes Sentiala Shield a foundation for building a transparent, extensible defensive cybersecurity platform.
