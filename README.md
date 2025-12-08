# 💊 **Pharmacy Dashboard – MVP Documentation**

# Part 1
## **0. Team & Roles** 👥

### **Team Composition**

* **Solo Developer** (Full-Stack) Mathieu GODALIER

### **Roles Covered**

* Product Owner 🎯
* UI/UX Designer 🎨
* Backend Developer ⚙️
* Frontend Developer 🖥️
* DevOps / Tester ✅

### **Work Standards**

* Frequent commits with clear messages ✍️
* Continuous documentation 📖
* Focused work sessions (Pomodoro) 🍅
* Weekly progress review 🗓️
* Regular feature testing 🔎

### **Tools**

* **Versioning**: Git / GitHub 🐙
* **Documentation**: README, notes 📝
* **Project Management**: Trello 📋
* **Quick Notes**: TODO.md 📌

### **Decision Process**

* SMART approach for all major decisions 🧠

### **Stakeholders**

| Stakeholder | Role | Impact | Involvement |
| :--- | :--- | :--- | :--- |
| Pharmacists 🧑‍⚕️ | Primary Users | Critical | High |
| Pharmacy Assistants 🤝 | Secondary Users | High | Medium |
| Patients 🧍 | Information Providers | Low | Low |
| Doctors 🩺 | Directory Data | Low | Low |
| Developer 💻 | Creator / Maintainer | Critical | Very High |

---

## **1. Brainstorming & Idea Evaluation** 💡

### **Idea Generation**

* Mind Mapping 🗺️
* SCAMPER framework
* “How Might We” questions 🤔

> * Reduce stock errors
> * Improve team coordination
> * Prevent drug-interaction risks
> * Centralize pharmaceutical information

### **Idea Evaluation**

| # | Project Idea | Description | Feas. | Impact | Complexity | Risks | Score |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Complete Pharmacy Dashboard | Inventory + Sales + Calendar + AI | 4 | 5 | High | AI/time | **20** |
| 2 | Stock Management Only | Inventory + alerts | 5 | 3 | Low | Limited scope | 15 |
| 3 | Pharma Chatbot | Interactions + info | 3 | 4 | Medium | Data quality | 15 |
| 4 | Team Calendar | Shift management | 5 | 2 | Low | Low impact | 10 |
| 5 | Patient CRM | Client database | 4 | 3 | Medium | GDPR | 15 |

### **Selected Idea**

**Complete Pharmacy Dashboard — Score 20/20** ✔️🥇

---

# Part 2
## **2. MVP Definition** 🏗️

### **Problem** 📉

Pharmacies rely on fragmented and outdated tools (Excel, paper planning, isolated software). This fragmentation leads to:

* Time loss (20–30 min/day) ⏱️
* Frequent stock errors ❌
* No proactive alerts
* Poor internal coordination
* Slow access to essential information (drug interactions, doctors directory)

### **Solution** ✨

A unified, intelligent web dashboard providing:

* Real-time inventory and sales management 📈
* AI-assisted chatbot (interactions, alerts, schedule, directory) 🤖
* Team calendar 📅
* Basic client database 🗄️
* Regional doctors directory 🗺️
* Fully responsive interface 📱

### **Target Audience** 🎯

* Pharmacists
* Pharmacy assistants
* Technicians
> Âge: 25–60, basic to intermediate computer skills.

### **Application Type** 🛠️

* **Responsive Web App** (desktop/tablet)
* **Backend**: Flask + SQLAlchemy 🐍
* **Frontend**: HTML5, CSS3, JavaScript
* **API**: Flask-RESTX (Swagger built-in) 🔌
* **NLP**: NLTK / spaCy
* **Charts**: Chart.js
* **Database**: SQLite (MVP) 💾

### **Justification**

* High impact 🚀
* Manageable solo development
* Strong demo value
* Scalable architecture
* Real-world relevance

---

## **MVP SMART Objectives** 🚀

| # | Objective | Description | Deadline |
| :--- | :--- | :--- | :--- |
| 1 | Inventory & Sales Module | CRUD + alerts | Weeks 1–3 |
| 2 | Chatbot (4 query types) | Interactions, stock, directory, schedule | Weeks 4–6 |
| 3 | Responsive Dashboard UI | Home + 5 modules | Weeks 2–7 |

---

## **Key MVP Features** ⭐

### **1. Inventory Management** 📦

* Medication CRUD
* Stock tracking
* Low-stock alerts 🔔
* History
> **Priority: Critical**

### **2. Sales Tracking** 💰

* Sales records
* Statistics (top products, revenue)
* Graphs via Chart.js
* CSV export 📥
> **Priority: Critical**

### **3. Intelligent Chatbot** 🧠

* Drug-interaction checks ⚠️
* Doctors directory lookup
* Team schedule display
* Stock alerts
> **Priority: High**

### **4. Team Calendar** 🗓️

* Shifts, absences, availability
> **Priority: Medium**

### **5. Client Information** 🧑

* Basic client record
* Notes & quick search
> **Priority: Medium**

### **6. Doctors Directory** 📇

* Regional list
* Filters & search
> **Priority: Medium**

---

## **Project Scope** 🔭

| **In-Scope** (✅) | **Out-of-Scope** (❌) |
| :--- | :--- |
| Responsive dashboard | Mobile native apps |
| Stock tracking + alerts | Automatic supplier ordering |
| Sales system + charts | Predictive analytics |
| Rule-based chatbot | Generative AI chatbot |
| Team calendar | Google Calendar sync |
| Basic clients module | Advanced GDPR / external CRM |
| Static doctors directory | Cloud-scale architecture |
| Simple authentication | Full CI/CD pipeline |
| Local/simple server deployment | |
| Manual testing | |

---

## **Risks & Mitigation** 🚨

| Risk | Probability | Impact | Mitigation |
| :--- | :--- | :--- | :--- |
| Complex AI Chatbot | High | High | Rule-based system + light NLP 🤖 |
| Data Quality | Medium | Critical | Reliable sources + manual validation 🛡️ |
| Solo Workload | High | Medium | Strict MVP, weekly sprints 🏃 |
| Integration Issues | Medium | Medium | Well-documented API, modular archi |
| Performance | Low | Medium | Indexing, pagination, lazy loading |
| Security | Medium | High | Password hashing, ORM validation, HTTPS 🔐 |

---

## **3. Executive Summary** 👑

### **Vision**

A modern, centralized dashboard that simplifies pharmacy operations, enhances safety, and reduces errors through smart automation and AI assistance.

### **Modules**

1. Inventory with alerts 📦
2. Sales tracking + visual stats 📈
3. Multifunction AI chatbot 💬
4. Team calendar 📅
5. Client database 🗄️
6. Doctors directory 🩺

### **Tech Stack**

* Flask + SQLAlchemy 🐍
* RESTX (Swagger)
* HTML / CSS / JS
* SQLite 💾
* Chart.js
* NLTK/ spaCy

### **Value Proposition**

* Replaces 5+ existing tools
* Smart proactive alerts 💡
* Unique chatbot component
* Lightweight, low-cost, accessible
* Fast information access ⚡

### **Expected Impact** 📊

* **–30%** administrative time
* **–50%** stock outages
* Drug-interaction checks in **< 5 seconds**
* **–40%** schedule conflicts

### **Timeline (8–10 Weeks)** ⏳

* Weeks 1–2 → Architecture, DB, backend foundations
* Weeks 3–4 → Inventory + sales modules
* Weeks 5–6–7 → Chatbot
* Weeks 8–9 → Frontend + calendar + directory
* Weeks 10 → Testing, optimization, documentation

### **Success Metrics** 💯

* 100% MVP modules functional
* Chatbot ≥ 80% relevant answers
* Fully responsive UI
* Loading time < 2s
* ≥ 4/5 user satisfaction

