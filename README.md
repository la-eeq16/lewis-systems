# Lewis Systems

> Engineering Intelligent Business Systems

![Status](https://img.shields.io/badge/Status-Active%20Development-brightgreen)
![Product](https://img.shields.io/badge/Product-ClientPilot-blue)
![Version](https://img.shields.io/badge/Product-v0.3.0-orange)
![License](https://img.shields.io/badge/Repository-Private-lightgrey)

---

## About Lewis Systems

Lewis Systems is a software and automation company based in Cape Town, South Africa.

Our mission is to design intelligent business systems that help professional service firms automate repetitive work, improve operational efficiency, and create exceptional client experiences.

Rather than building one-off automations, we develop complete software solutions that combine automation, artificial intelligence, and thoughtful system design.

---

# Current Product

## ClientPilot

ClientPilot is an AI-powered Client Intake & Lead Qualification Platform.

It automates the journey from a prospective client's first enquiry to a qualified consultation booking.

The initial release is focused on **small accounting firms**, with future versions expanding to additional professional service industries.

---

# Current Development Focus

Current Phase

🚧 Phase 3 – MVP Implementation

Current Module

Module 3 – Workflow Automation

Current Sprint

Sprint 2 – Workflow Automation (WF-001 Client Intake & Qualification)

Current Objective

Harden and extend WF-001, which is built on Make for the MVP, by adding AI qualification, Slack notifications, administrator alerts and Calendly integration.

Next Milestone

Add the AI evaluation step (Module 4) and the administrator alert for failed workflows. A later migration from Make to n8n is planned once the platform matures (see ADR-004).

---

# Vision

To become South Africa's leading provider of intelligent business systems for professional service businesses.

---

# Mission

Build reliable software that solves real business problems.

---

# Core Principles

Every product developed by Lewis Systems follows these principles:

- Documentation First
- Business First
- Simplicity
- Reliability
- Modular Design
- Reusability
- Continuous Improvement
- Security by Design

> **If it isn't documented, it isn't complete.**

---

## Technology Stack

### Development

- Visual Studio Code
- Git
- GitHub
- JavaScript

### Automation

- Make (MVP; n8n planned)

### Database / CRM

- Airtable

### Artificial Intelligence

- OpenAI

### Forms

- Google Forms

### Scheduling

- Calendly

### Communication

- Slack (planned)

### Email

- Gmail

---

# Repository Structure

```text
lewis-systems/
│
├── api/
│   └── API documentation
│
├── assets/
│   ├── branding/
│   ├── diagrams/
│   └── screenshots/
│
├── docs/
│   ├── adr/
│   ├── 00-PROJECT-INDEX.md
│   ├── 01-MASTER-PROJECT.md
│   ├── 02-PRODUCT-REQUIREMENTS.md
│   ├── 03-BUSINESS-REQUIREMENTS.md
│   ├── 04-SYSTEM-ARCHITECTURE.md
│   ├── 05-DATA-MODEL.md
│   ├── 06-DEVELOPMENT-STANDARDS.md
│   ├── 07-WORKFLOW-DESIGN.md
│   ├── 08-AI-PROMPTS.md
│   ├── 09-API-INTEGRATIONS.md
│   ├── 10-TESTING.md
│   ├── 11-ROADMAP.md
│   ├── 12-CHANGELOG.md
│   ├── 13-PROJECT-STATUS.md
│   ├── 14-CONTRIBUTING.md
│   ├── 15-CODING-STANDARDS.md
│   ├── 16-SECURITY.md
│   ├── 17-DEPLOYMENT.md
│   ├── 18-DATABASE-STANDARDS.md
│   └── modules/
│
├── examples/
|
├── integrations/
│
├── javascript/
│
├── journal/
│
├── prompts/
│
├── scripts/
│
├── templates/
│
├── testing/
│
├── workflows/
│
├── .gitignore
└── README.md
```

---

# Development Status

| Component                       | Status                          |
| ------------------------------- | ------------------------------- |
| Lewis Systems                   | 🟢 Active Development           |
| ClientPilot                     | 🚧 Phase 3 – MVP Implementation |
| Documentation Suite             | ✅ Complete                      |
| Module 1 – CRM Database         | ✅ Complete                      |
| Module 2 – Google Forms         | ✅ Complete                      |
| Module 3 – Workflow Automation  | 🚧 In Progress                  |
| Module 4 – OpenAI Integration   | ⏳ Pending                       |
| Module 5 – Slack Integration    | ⏳ Pending                       |
| Module 6 – Calendly Integration | ⏳ Pending                       |
| Module 7 – End-to-End Testing   | ⏳ Pending                       |
| Pilot Launch                    | ⏳ Pending                       |

---

# Development Roadmap

## ✅ Phase 1 – Foundation

- Repository Setup
- Engineering Documentation
- Product Requirements
- Business Requirements
- System Architecture
- Development Standards

---

## ✅ Phase 2 – Solution Design

- CRM Database Design
- Airtable CRM Implementation
- CRM QA Validation
- Repository Organisation

---

## 🚧 Phase 3 – MVP Implementation

✅ Module 1 – CRM Database

✅ Module 2 – Google Forms

🚧 Module 3 – Workflow Automation

⏳ Module 4 – OpenAI Qualification

⏳ Module 5 – Slack Notifications

⏳ Module 6 – Calendly Integration

⏳ Module 7 – End-to-End Testing

---

# Current Progress

## ✅ Completed

- Engineering documentation
- System architecture
- CRM data model
- Airtable CRM implementation
- Companies table
- Contacts table
- Leads table
- Qualifications table
- Meetings table
- Activities table
- Workflow Logs table
- Settings table
- QA validation
- Airtable views
- CRM Database Module
- Airtable relationships
- Workflow Logs
- Settings
- Module 1 documentation

---

## 🚧 Current Work

- WF-001A Client Intake (Make) – built and tested
- WF-001B Lead Qualification (Make) – built and tested (rule-based scoring)
- Administrator alert for failed workflows
- Documentation alignment across all modules

---

## 🔵 Upcoming

- Make → n8n migration review (after the first paying client)
- OpenAI lead qualification
- Slack notifications
- Calendly scheduling
- End-to-end workflow testing

# Development Methodology

Every ClientPilot module follows the same engineering lifecycle.

```
Requirements
      ↓
Design
      ↓
Build
      ↓
Test
      ↓
Document
      ↓
Git Commit
      ↓
Git Push
```

A feature is considered complete only after every stage has been successfully completed.

---

# Documentation Standards

Every feature added to ClientPilot must include:

- Purpose
- Business Requirements
- Technical Design
- Workflow Documentation
- Testing
- Revision History

---

# Founder

**La-eeq Lewis**

Founder & Software Automation Developer

Cape Town, South Africa

---

# Repository Information

**Repository Status:** Private

This repository contains the engineering documentation, source code, automation workflows, CRM implementation, API specifications, AI prompt library, testing assets, and development resources for Lewis Systems and its flagship product, ClientPilot.

Development follows a documentation-first engineering methodology. Modules 1 (CRM Database) and 2 (Google Forms) have been completed, tested, and validated. Development is currently focused on Module 3 (Workflow Automation): WF-001 is implemented on Make for the MVP, with AI qualification, Slack and Calendly to follow. A future migration to n8n is planned (ADR-004).

---

## Project Information

| Item            | Value                                 |
| --------------- | ------------------------------------- |
| Product Version | v0.3.0                                |
| Current Phase   | 🚧 Phase 3 – MVP Implementation       |
| Current Module  | Module 3 – Workflow Automation        |
| Repository      | Private                               |
| License         | Proprietary                           |


© Lewis Systems. All rights reserved.
