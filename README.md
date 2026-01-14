# 🍯 AI-Powered Dynamic Honeypot

> MSc Cybersecurity Thesis Project - Adaptive honeypot system using LLM-based response generation

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![Ollama](https://img.shields.io/badge/Ollama-Llama%203.2-green.svg)](https://ollama.ai)

## 📋 Table of Contents

- [Overview](#overview)
- [Why This Topic?](#why-this-topic)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Project Timeline](#project-timeline)
- [Setup & Installation](#setup--installation)
- [Metrics & Evaluation](#metrics--evaluation)
- [Budget](#budget)
- [Risks & Mitigation](#risks--mitigation)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Overview

This project develops an **AI-powered dynamic SSH honeypot** that uses Large Language Models (Llama 3.2 Instruct) to generate realistic, context-aware responses to attacker interactions. Unlike traditional static honeypots that are easily fingerprinted, this system adapts its behavior in real-time based on attacker profiles and interaction patterns.

### Research Goals

- Increase attacker engagement time compared to static honeypots
- Delay detection of honeypot nature through adaptive responses
- Collect higher quality threat intelligence data
- Demonstrate practical application of LLMs in cybersecurity defense

## 💡 Why This Topic?

### Relevance
Modern cyberattacks are increasingly sophisticated. Static honeypots are easily identified through fingerprinting techniques. AI-powered solutions can adapt and provide more realistic deception.

### Interdisciplinary Nature
Combines:
- Machine Learning (LLMs, anomaly detection)
- Network Security
- Behavioral Analysis
- Real-time Systems

### Practical Value
Addresses a real industry problem where organizations continuously seek better threat detection and intelligence gathering solutions.

## ✨ Features

### Core Features (MVP)
- ✅ Functioning SSH honeypot (Cowrie-based)
- ✅ Attack data collection and storage
- ✅ LLM integration for basic command responses
- ✅ Real-time logging and visualization

### Advanced Features
- 🎭 **Multiple Personas**: Different honeypot "personalities" (novice admin, production server, IoT device)
- 🧠 **Context-Aware Responses**: LLM-generated replies based on attacker behavior
- 🔄 **Adaptive Learning**: Feedback loop to optimize deception strategies
- 📊 **Anomaly Detection**: ML-based classification of attack types
- 🎯 **Credential Intelligence**: Password collection and threat intelligence correlation
- 🔗 **Multi-Session Tracking**: Attacker "memory" across multiple sessions

## 🛠 Tech Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Honeypot** | Cowrie | SSH/Telnet emulation |
| **AI/LLM** | Llama 3.2 Instruct (Ollama) | Dynamic response generation |
| **Backend** | Python 3.11+ | Core logic and integration |
| **Data Collection** | ELK Stack / Loki + Grafana | Log aggregation and storage |
| **ML (Anomaly)** | scikit-learn | Attack classification |
| **Monitoring** | Grafana | Real-time visualization |
| **Deployment** | Docker + Docker Compose | Containerized environment |
| **VCS** | Git + GitHub | Version control |

### Why Llama + Ollama?

- **Local execution**: Runs on MacBook Pro M4 (no API costs)
- **Privacy**: No data sent to external services
- **Low latency**: Direct local inference

## 🏗 Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                         Internet                             │
└────────────────────────┬────────────────────────────────────┘
                         │ SSH Attacks
                         ▼
                  ┌──────────────┐
                  │  Cowrie      │
                  │  Honeypot    │
                  └──────┬───────┘
                         │ Logs
                         ▼
          ┌──────────────────────────────┐
          │   Context Analyzer            │
          │   - Session metadata          │
          │   - Command sequence          │
          │   - Attacker profiling        │
          └──────┬───────────────────────┘
                 │
         ┌───────┴────────┐
         │                │
         ▼                ▼
   ┌─────────┐      ┌──────────┐
   │   ML    │      │  Llama   │
   │ Anomaly │      │  (Ollama)│
   │Detection│      │   LLM    │
   └────┬────┘      └─────┬────┘
        │                 │
        └────────┬────────┘
                 ▼
        ┌─────────────────┐
        │ Response Engine │
        │  - Persona mgmt │
        │  - Cache        │
        └────────┬────────┘
                 │
                 ▼
        ┌─────────────────┐
        │  ELK / Grafana  │
        │  Visualization  │
        └─────────────────┘
```

## 📅 Project Timeline

### 16-Week Detailed Plan

#### Phase 1: Setup & Infrastructure (Weeks 1-3)

**Week 1: Environment Setup**
- Literature review (honeypot types, AI applications)
- Cowrie installation in Docker
- Ollama + Llama 3.2 setup on MacBook Pro M4
- Git repository initialization
- **Output**: Working base honeypot + literature outline

**Week 2: Data Collection Infrastructure**
- ELK stack setup (or Loki + Grafana alternative)
- Cowrie log parsing and structured storage
- Monitoring dashboard basics
- Generate test attacks (nmap, hydra, metasploit)
- **Output**: Functional log pipeline, initial attack data

**Week 3: Baseline Data Collection**
- Connect honeypot to internet (VPS recommended)
- 7-10 days of passive data collection
- Initial data analysis: common attack types, usernames, commands
- Define baseline metrics for anomaly detection
- **Output**: Min. 100-500 attack sessions, analysis report

#### Phase 2: AI Integration & Core Functions (Weeks 4-7)

**Week 4: Ollama API Integration**
- Test Llama model with various prompts
- Develop Python API wrapper (caching, rate limiting)
- Prompt engineering for SSH session context
- Response time optimization (streaming, batch)
- **Output**: Working Llama integration, prompt template library

**Week 5: Attack Context Analysis**
- Session metadata processing (IP geolocation, timezone, attack speed)
- Command sequence analysis
- Attacker type categorization (script kiddie, bot, advanced)
- Context builder: session history + attacker profile → LLM context
- **Output**: Intelligent context extraction system

**Week 6: Dynamic Response Generation - Basics**
- LLM-based shell prompt customization
- Dynamic error message generation
- Fake filesystem responses (ls, cat, pwd)
- Response consistency checking (session memory)
- **Output**: Working dynamic response system for 5-10 basic commands

**Week 7: Response Strategy Implementation**
- Define different "personas":
  - Novice sysadmin (errors, slow responses)
  - Production server (fast, accurate)
  - IoT device (limited commands)
- Strategy switching based on attacker type
- A/B test preparation: AI vs. static responses
- **Output**: 3 different honeypot personas with working prototypes

#### Phase 3: Advanced Features & Learning (Weeks 8-11)

**Week 8: Adaptive Behavior - Basics**
- Session-based learning: detect successful deceptions
- Engagement time measurement and optimization
- LLM prompt fine-tuning based on real feedback
- Early detection indicators (quick exit, honeypot signature search)
- **Output**: First version of adaptive feedback loop

**Week 9: ML Anomaly Detection**
- Traditional ML model (Random Forest/Isolation Forest) for attack type detection
- Feature engineering: command frequency, timing, session length
- Real-time classification pipeline
- Hybrid LLM + ML: ML pre-filters → LLM generates response
- **Output**: Hybrid AI system, reduced LLM calls (cost optimization)

**Week 10: Credential Intelligence**
- Password collection and analysis
- Cross-reference with Rockyou, HIBP
- Credential stuffing detection
- LLM-based social engineering responses
- **Output**: Credential tracking system, threat intelligence database

**Week 11: Multi-Session Coordination**
- Link multiple sessions from same attacker
- Simulate attacker "memory" (if they return)
- Distributed honeypot preparation (multiple IPs, coordinated collection)
- Session state management optimization
- **Output**: Intelligent multi-session tracking

#### Phase 4: Testing & Evaluation (Weeks 12-14)

**Week 12: Controlled Testing**
- Automated attack scripts (various difficulty levels)
- Recruit friendly hackers (ethical testers if possible)
- A/B test execution:
  - Control group: static Cowrie
  - Experimental group: AI-powered version
- Metric collection: engagement time, session depth, command count
- **Output**: 50+ controlled test sessions, preliminary results

**Week 13: Live Testing & Data Analysis**
- Run both versions in parallel for 7-14 days
- Collect real attack data
- Statistical analysis (t-test, Mann-Whitney U)
- False positive analysis
- Detection evasion measurement
- **Output**: Complete dataset, statistical report

**Week 14: Results Evaluation**
- Aggregate and visualize all metrics
- Create comparison tables
- Document edge cases and bugs
- Cost-benefit analysis
- **Output**: Complete results chapter with graphs

#### Phase 5: Documentation & Presentation (Weeks 15-16)

**Week 15: Thesis Writing**
- Finalize introduction and literature review
- Detailed system architecture description (UML diagrams)
- Implementation chapter with code snippets
- Write results chapter
- Limitations and future work
- **Output**: First complete thesis draft

**Week 16: Finalization**
- Thesis proofreading, corrections, formatting
- Presentation creation (20-30 slides)
- Demo video (live honeypot operation)
- Code cleanup, README, GitHub documentation
- Submission preparation
- **Output**: Submission-ready thesis + defense-ready presentation

## 🚀 Setup & Installation

### Prerequisites

- **Hardware**: MacBook Pro M4 (or similar M-series chip)
- **OS**: macOS 14+ and/or Linux (Ubuntu at first place)
- **Software**:
  - Docker & Docker Compose
  - Python 3.11+
  - Ollama
  - Git

### Quick Start

```bash
# 1. Clone repository
git clone https://github.com/yourusername/ai-honeypot.git
cd ai-honeypot

# 2. Install Ollama (macOS)
brew install ollama

# 3. Download Llama model
ollama pull llama3.2

# 4. Start services
docker-compose up -d

# 5. Verify installation
curl http://localhost:11434/api/generate -d '{"model": "llama3.2", "prompt": "test"}'
```

### Configuration

Edit `config.yaml`:

```yaml
honeypot:
  host: 0.0.0.0
  port: 2222
  
llm:
  model: llama3.2
  temperature: 0.7
  max_tokens: 150
  
personas:
  - novice_admin
  - production_server
  - iot_device
```

## 📊 Metrics & Evaluation

### Key Metrics

| Metric | Description | Target |
|--------|-------------|--------|
| **Engagement Time** | How long attackers stay in system | +50% vs static |
| **Detection Evasion** | Time until honeypot is identified | +100% vs static |
| **Data Quality** | Amount of useful intelligence collected | +30% vs static |
| **Session Depth** | Number of commands executed | +40% vs static |
| **False Positive Rate** | Accuracy of attack type classification | <5% |
| **Response Latency** | LLM response time | <2 seconds |

### Evaluation Methods

- **A/B Testing**: Static Cowrie vs. AI-powered version
- **Statistical Analysis**: t-tests, Mann-Whitney U tests
- **Qualitative Analysis**: Manual review of attacker interactions
- **Cost Analysis**: Infrastructure costs vs. intelligence value

## 💰 Budget

| Item | Cost | Note |
|------|------|------|
| Proxmox (local) | $0 | i9, 32GB RAM, 1TB SSD |
| Ollama (local) | $0 | MacBook Pro M4 |
| GitHub/GitLab | $0 | Free |

## ⚠️ Risks & Mitigation

| Risk | Mitigation |
|------|-----------|
| Low attack volume | Multiple VPS with different IPs, Shodan submission |
| LLM too slow | Response caching, streaming, smaller model (3.2 1B) |
| Ethical/legal issues | Disclaimer banner, passive collection only, GDPR compliance |
| MacBook overheating | Batch processing, rate limiting, overnight runs |

## 📚 Key milestones

- [ ] **Week 3**: Working honeypot + min. 100 attack sessions
- [ ] **Week 7**: AI integration functional for 10+ commands
- [ ] **Week 11**: Complete system with adaptive behavior
- [ ] **Week 14**: Testing complete, statistical analysis ready
- [ ] **Week 16**: Thesis submitted, defense presentation ready

## 🔬 Research Questions

1. Can LLM-based responses increase attacker engagement time compared to static honeypots?
2. How effectively can ML models classify different attack types in real-time?
3. What impact do different honeypot "personas" have on data quality?
4. Is local LLM inference practical for real-time cybersecurity applications?

## 📖 Documentation - soon

- [Installation Guide](docs/installation.md)
- [API Reference](docs/api.md)
- [Prompt Engineering Guide](docs/prompts.md)
- [Deployment Guide](docs/deployment.md)

## 🤝 Contributing

This is an academic thesis project, but suggestions and feedback are welcome!

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Commit changes (`git commit -am 'Add improvement'`)
4. Push to branch (`git push origin feature/improvement`)
5. Open a Pull Request

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details

## 👨‍💻 Author

**Mark Meiszterics**
- MSc Cybersecurity Student
- Óbuda University

## 🙏 Acknowledgments

- Cowrie Honeypot Project
- Ollama Team
- Meta AI (Llama models)
- Thesis Advisor: Dr. Advisor Name

## 📚 References

- [Cowrie SSH Honeypot](https://github.com/cowrie/cowrie)
- [Ollama](https://ollama.ai)
- [Llama 3.2 Technical Report](https://ai.meta.com/llama/)
- Relevant academic papers (to be added)

---

⭐ **Star this repo if you find it useful!**

📧 Questions? Open an issue or contact me directly.
