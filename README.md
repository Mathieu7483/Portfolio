<p align="center"\>
<img src="https://github.com/Mathieu7483/Dashboard-Pharma/blob/main/Client/assets/img/accueil%20Dasboard%20Pharma.png"/>
</p\>

# 💊 **Pharmacy Dashboard – MVP Documentation**

## **Table of Contents** 📑

* **PART 1: Idea Development (Completed)**
    * 0. Team & Roles 👥
    * 1. Brainstorming & Idea Evaluation 💡
* **PART 2: Project Planning (In Progress)**
    * 2. MVP Definition 🏗️
    * 3. Executive Summary 👑
        * 3.1. Vision
        * 3.2. Modules
        * 3.3. Tech Stack
        * 3.4. Value Proposition
        * 3.5. Expected Impact
        * 3.6. Timeline (5-Stage Curriculum Structure) 🗺️
* **PART 3: Technical Documentation (To Come)** ⚪
* **PART 4: MVP Development (To Come)** ⚪
* **PART 5: Project Closure (To Come)** ⚪

---

# **PART 1: Idea Development (Completed)** ✅

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
* **Quick Notes**: TODO.md, notes, post-it 📌

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

# **PART 2: Project Planning** ✅

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
> Age: 25–60, basic to intermediate computer skills.

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

### **MVP SMART Objectives** 🚀

| # | Objective | Description | Deadline |
| :--- | :--- | :--- | :--- |
| 1 | Inventory & Sales Module | CRUD + alerts | Weeks 1–3 |
| 2 | Chatbot (4 query types) | Interactions, stock, directory, schedule | Weeks 4–7 |
| 3 | Responsive Dashboard UI | Home + 5 modules | Weeks 2–7 |

### **Key MVP Features** ⭐

1.  **Inventory Management** 📦: CRUD, Stock tracking, Low-stock alerts 🔔
2.  **Sales Tracking** 💰: Sales records, Statistics, Graphs via Chart.js, CSV export 📥
3.  **Intelligent Chatbot** 🧠: Drug-interaction checks ⚠️, Stock alerts, Directory lookup
4.  **Team Calendar** 🗓️: Shifts, absences, availability
5.  **Client Information** 🧑: Basic client record, Notes & quick search
6.  **Doctors Directory** 📇: Regional list, Filters & search

### **Project Scope** 🔭

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

### **Risks & Mitigation** 🚨

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

1.  Inventory with alerts 📦
2.  Sales tracking + visual stats 📈
3.  Multifunction AI chatbot 💬
4.  Team calendar 📅
5.  Client database 🗄️
6.  Doctors directory 🩺

### **Tech Stack**

* Flask + SQLAlchemy 🐍
* RESTX (Swagger)
* HTML / CSS / JS
* SQLite 💾
* Chart.js (for graphics)
* spaCy (for ChatBot Caducée)

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

### **Timeline (5-Stage Curriculum Structure)** 🗺️

We use this table to track project progress according to the curriculum's stages.

| Stage | Estimated Period | Primary Objective | Key Deliverables | Status |
| :--- | :--- | :--- | :--- | :--- |
| **Stage 1: Idea Development** | **Completed** | Define the need and the solution. | **MVP Documentation (Part 1)** | **✅ COMPLETED** |
| **Stage 2: Project Planning** | **Completed** | Define the structure, architecture, and data models. | **Detailed Timeline, DB/API Models** | **✅ COMPLETED** |
| **Stage 3: Technical Documentation** | Weeks 2–3 | Formalize the complete architecture, API, and technical specifications. | API Specifications (Swagger), Wireframes | **▶️ IN PROGRESS** |
| **Stage 4: MVP Development** | Weeks 4–10 | Build, test, and integrate key functionalities. | Functional Code (Backend/Frontend), Integration Tests | ⚪ TO COME |
| **Stage 5: Project Closure** | Weeks 11–12 | Finalize, document, and present the project. | Final Report, Demo, Final Optimization | ⚪ TO COME |

---

# **PART 3: Technical Documentation ** ✅
## 📖 Technical Documentation
For a detailed understanding of the system's architecture, design decisions, and development strategies, please refer to the complete technical documentation:

[Link to documentation.md](https://github.com/Mathieu7483/Portfolio/blob/main/documentation.md)

---

# **PART 4: MVP Development** ✅

### 1. Execution & Task Management

Following the initial plan, development was executed in localized sprints, ensuring each feature met the "Definition of Done."

* **Developer Focus:** Translation of User Stories into Python/Flask logic, adhering to PEP 8 standards and OOP principles.
* **SCM Role:** Managed version control using a **Feature Branch Workflow**. Each feature (Auth, Inventory, NLU) was developed in isolation before being merged via Pull Requests (PRs) to ensure main branch stability.
* **QA Integration:** Continuous verification of API endpoints using Postman to validate JSON schemas and HTTP response codes ($200$, $401$, $403$, etc.).

### 2. Progress Monitoring & Adaptive Adjustment

To maintain momentum and meet the Stage 4 deadline, the following tracking mechanisms were used:

* **Daily Stand-ups:** Brief internal reviews to identify "blockers" (e.g., resolving complex SQLAlchemy joins for the Sales analytics).
* **Metrics:** We tracked **Sprint Velocity** (tasks completed vs. planned) and **Bug Resolution Rates**.
* **Adjustments:** When NLU entity extraction proved more complex than anticipated, we re-prioritized the `product_alias` logic to ensure core stock queries remained functional for the MVP.

### 3. Sprint Reviews & Retrospectives

At the end of each iteration, the team conducted:

* **Sprint Reviews:** Demonstrating the functional Dashboard UI to simulate a pharmacist’s workflow.
* **Retrospectives:** Identifying that while the Facade Pattern slowed down initial development, it drastically reduced time-to-fix during the final integration phase.

### 4. Final Integration & QA Testing

The project concluded with a comprehensive **End-to-End (E2E)** testing phase:

* **Integration:** Verified that the Vanilla JS frontend correctly consumed the Flask REST API.
* **DB Integrity:** Confirmed that SQLite transactions maintained ACID compliance even under "stress" data seeding.
* **Final QA:** Executed `test_api_route.py` and `test_chatbot.sh` as a final gatekeeper before the Technical Manual Review.

---

## 5. Deliverables & Evidence

* **Source Repository:** [Link to your GitHub Repository](https://github.com/Mathieu7483/Dashboard-Pharma)
* **Sprint Planning & Retrospectives:** Documented in project `README.md` and Stage 4 documentation.
* **Testing Evidence:** Results from `test_api_route.py` and Postman collection exports.
* **Production/Demo Environment:** [Link to Video Demonstration](https://studio.youtube.com/video/emE1aqvT92M/edit)

---

## 6. Technical Manual Review Preparation (Oral Exam)

*As you prepare for the oral evaluation with your SWE (Software Engineer), ensure you can articulate the following:*

| Topic | Key Talking Points |
| --- | --- |
| **App Architecture** | The **Facade Pattern** decouples our API from the Database for maintainability. |
| **Database Design** | **3rd Normal Form (3NF)** implementation using SQLAlchemy to eliminate redundancy. |
| **Security & RBAC** | Use of **Bcrypt** for hashing and custom **Python Decorators** for Role-Based Access Control. |
| **NLU Logic** | How the `NLUProcessor` converts natural language into structured database queries. |
| **Testing** | Difference between unit testing endpoints and integration testing the chatbot engine. |


# **PART 5: Project Closure (In progress)** ▶️


