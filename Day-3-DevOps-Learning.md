
# Day 3 – DevOps, Agile and SRE

**Today's Goal:** Understand how software development teams plan, develop, release and maintain applications reliably.

## Learning Objectives

1. Understand Agile methodology.
2. Understand Scrum and Kanban.
3. Difference between Agile and DevOps.
4. Understand SRE (Site Reliability Engineering).
5. Understand SLA, SLI and SLO with practical examples.

---

## Part 1 – What is Agile?

Agile is a software development methodology in which a team develops and delivers software in small, manageable parts instead of waiting to complete the entire project.

### Example: E-commerce Website

Imagine a company wants to develop an online shopping application.

Instead of building everything at once:

- Sprint 1: User registration and login.
- Sprint 2: Product listing.
- Sprint 3: Shopping cart.
- Sprint 4: Payment gateway.
- Sprint 5: Order tracking.

The team develops, tests and reviews the application in smaller cycles.

### Benefits of Agile

- Faster delivery.
- Continuous feedback.
- Better collaboration.
- Easier handling of changing requirements.
- Early identification of problems.

## Part 2 – What is a Sprint?

A Sprint is a fixed period during which a team completes a planned set of work.

Typically, a Sprint lasts 1–4 weeks.

| Sprint Activity | Purpose |
|---|---|
| Sprint Planning | Decide what work to do |
| Daily Stand-up | Discuss progress and blockers |
| Development | Build features |
| Testing | Verify functionality |
| Sprint Review | Demonstrate completed work |
| Retrospective | Identify improvements |

### Interview Question: What is a Sprint?

"My understanding is that a Sprint is a fixed time period in Agile, usually one to four weeks, in which the team plans, develops and delivers a specific set of tasks."

## Part 3 – Scrum and Kanban

These are two popular ways of managing Agile work.

### A. Scrum

Scrum is an Agile framework where a team works in fixed-length Sprints.

Important Scrum terms:

| Term | Meaning |
|---|---|
| Product Owner | Decides priorities and requirements |
| Scrum Master | Helps the team follow Scrum |
| Development Team | Builds and tests the product |
| Product Backlog | List of all required work |
| Sprint Backlog | Tasks selected for the current Sprint |
| Increment | Completed working functionality |

### B. Kanban

Kanban is a visual method of managing work using a board.

Example:

**To Do**
- Create login
- Configure server

**In Progress**
- Install Nginx

**Testing**
- Test API

**Done**
- Git setup

### Difference Between Scrum and Kanban

| Scrum | Kanban |
|---|---|
| Fixed-length Sprints | Continuous workflow |
| Sprint planning | Work pulled as capacity allows |
| Defined team roles | No mandatory roles |
| Sprint review | Continuous delivery/review |

## Part 4 – Difference Between Agile and DevOps

| Agile | DevOps |
|---|---|
| Focuses on software development and collaboration | Focuses on development and operations collaboration |
| Delivers software in small iterations | Automates build, test, deployment and operations |
| Uses Scrum and Kanban | Uses Jenkins, Git, Docker, Kubernetes, etc. |
| Focuses on customer feedback | Focuses on reliable and faster delivery |

### Simple Example

- Agile team develops a new login feature in a Sprint.
- DevOps team creates a CI/CD pipeline to build, test and deploy that feature.

### Interview Answer

"Agile is a methodology that helps teams develop software in small iterations with continuous feedback. DevOps brings development and operations together through automation, CI/CD and continuous monitoring. Both complement each other."

## Part 5 – What is SRE?

SRE stands for Site Reliability Engineering.

SRE applies software engineering principles to IT operations to make systems more reliable, scalable and available.

### Example

Imagine an e-commerce website that must remain available 24/7.

An SRE engineer works on:

- Monitoring application health.
- Improving system availability.
- Automating repetitive operational tasks.
- Managing incidents.
- Reducing downtime.
- Improving performance and reliability.

### Important SRE Concepts: SLA, SLI and SLO

**1. SLI – Service Level Indicator**

A measurable metric that tells us how a service is performing.

Examples:
- Application availability.
- API response time.
- Error rate.
- Request success rate.

**2. SLO – Service Level Objective**

The target we want our service to achieve.

Example: Website availability should be 99.9%.

**3. SLA – Service Level Agreement**

A formal agreement between a service provider and customer defining expected service levels and possible consequences if they are not met.

Example: A cloud provider agrees to a specified availability commitment under its SLA terms.

### Easy Way to Remember

| Term | Meaning | Example |
|---|---|---|
| SLI | Actual measurement | 99.95% availability |
| SLO | Target | 99.9% availability |
| SLA | Customer agreement | Contractual availability commitment |

Remember:

- SLI = Measurement
- SLO = Target
- SLA = Agreement

## Part 6 – Practical Exercise

Let's connect these concepts to a real DevOps team.

Imagine your company is maintaining an online shopping application.

Your responsibilities:

1. Developers are building a new payment feature.
2. The team plans to complete it within a two-week Sprint.
3. Tasks are tracked using a Kanban board.
4. Jenkins automatically builds and tests the application.
5. Prometheus and Grafana monitor application performance.
6. The SRE team investigates incidents and improves availability.

### Assignment

Explain how Agile, Scrum, DevOps and SRE work together in this scenario.

## Part 7 – Interview Preparation

Practise answering these questions in your own words:

1. What is Agile methodology?
2. What is a Sprint in Scrum?
3. Difference between Scrum and Kanban?
4. Difference between Agile and DevOps?
5. What is SRE?
6. Explain SLA, SLI and SLO with examples.

---

## Day 3 – Completion Status

- [x] Agile methodology
- [x] Scrum and Kanban
- [x] Agile vs DevOps
- [x] Site Reliability Engineering
- [x] SLA, SLI and SLO
- [x] Practical scenario
- [x] Interview preparation

**Status: Day 3 Completed**
