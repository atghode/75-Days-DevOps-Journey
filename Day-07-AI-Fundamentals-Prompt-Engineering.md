
# Day 7 – AI Fundamentals, Prompt Engineering and AI Coding Assistants

## 1. Introduction

Artificial Intelligence (AI) is becoming an important part of modern DevOps practices. It helps engineers automate tasks, troubleshoot problems, generate scripts, analyse logs, and improve productivity.

## 2. AI Fundamentals

- **Artificial Intelligence (AI):** Technology that enables machines to perform tasks that normally require human intelligence.
- **Machine Learning (ML):** A subset of AI that learns patterns from data.
- **Deep Learning:** A subset of ML that uses multi-layered neural networks.
- **Generative AI:** AI that can generate new content, such as text, code, images, and other outputs.
- **Large Language Model (LLM):** An AI model trained on large amounts of text to understand and generate human-like language.

## 3. AI vs ML vs Deep Learning vs Generative AI

- AI is the broad field.
- ML is a subset of AI.
- Deep Learning is a subset of ML.
- Generative AI focuses on creating new content.

## 4. Generative AI Tools

Some commonly used AI tools:

- ChatGPT
- GitHub Copilot
- Google Gemini

These tools can help with coding, troubleshooting, explanations, and documentation.

## 5. Prompt Engineering

Prompt Engineering means writing clear and structured instructions to get useful responses from AI.

### Five Components of a Good Prompt

1. Role – Define the role of the AI.
2. Context – Provide relevant background information.
3. Task – Explain what you want it to do.
4. Constraints – Mention limitations and requirements.
5. Output Format – Specify how the response should be presented.

### Example

Weak prompt:
Explain Linux.

Better prompt:
Act as a Linux system administrator. Explain the `df -h` command for a beginner using RHEL 9. Include its purpose, sample output, and a real-world DevOps troubleshooting example.

## 6. AI in DevOps

AI can assist with:

- Linux troubleshooting
- Bash scripting
- Python automation
- Dockerfile generation
- Kubernetes troubleshooting
- Terraform code assistance
- Ansible playbook creation
- Jenkins pipeline troubleshooting
- Log analysis and documentation

## 7. AI Coding Assistants

### GitHub Copilot
An AI coding assistant that provides code suggestions and helps developers write code.

### ChatGPT
Can explain commands, generate scripts, troubleshoot errors, and assist with technical documentation.

### Google Gemini
A Generative AI assistant that can help with technical questions, coding, and problem-solving.

## 8. Practical DevOps Scenarios

### Scenario 1: Disk Usage Troubleshooting

If a Linux server's root filesystem reaches 95% usage, AI can help explain investigation commands such as:

```bash
df -h
du -sh /*
```

Always verify commands and investigate before deleting files.

### Scenario 2: Docker Command Not Found

Error:

```text
-bash: docker: command not found
```

AI can help investigate whether Docker is installed, whether the executable is in PATH, or whether the required container runtime is missing.

## 9. Security Risks and Best Practices

- Never share passwords, API keys, tokens, or SSH private keys with AI tools.
- Review AI-generated scripts before executing them.
- Validate commands before using them in production.
- Test scripts in a development environment first.
- Verify AI responses using reliable documentation.
- Do not blindly trust AI-generated answers.

## 10. Important Interview Questions

**Q1. What is Artificial Intelligence?**

AI is a technology that enables machines to perform tasks that normally require human intelligence.

**Q2. What is Generative AI?**

Generative AI creates new content such as text, code, images, and other outputs.

**Q3. What is Prompt Engineering?**

Prompt Engineering is the process of writing clear and structured instructions to get accurate and useful responses from AI.

**Q4. What is an LLM?**

LLM stands for Large Language Model. It is an AI model trained on large amounts of text to understand and generate language.

**Q5. How does AI help in DevOps?**

AI helps DevOps engineers with scripting, troubleshooting, log analysis, automation, and documentation.

**Q6. Can AI replace DevOps engineers?**

No. AI can assist engineers, but technical knowledge, decision-making, security awareness, and practical experience remain important.

## 11. Key Takeaways

- Understand the fundamentals of AI and Generative AI.
- Learn how LLMs work at a basic level.
- Write structured prompts using Prompt Engineering.
- Explore AI coding assistants.
- Use AI for DevOps troubleshooting and automation.
- Always validate AI-generated code and commands.

## 12. Day 7 Status

Topic: AI Fundamentals – Prompt Engineering and AI Coding Assistants

Status: Learning in Progress

Next Topic: Day 8 – Linux Fundamentals, Architecture, Distributions and GCP Introduction.
