# AI Customer Support Ticket System

> An AI-powered customer support automation system built with n8n, OpenAI, Google Sheets, Gmail, Webhooks, and intelligent priority routing.

## 🚀 Overview

Customer support teams often receive large numbers of support requests that must be reviewed, classified, prioritized, documented, and routed to the appropriate response process.

This project automates that workflow from end to end.

The **AI Customer Support Ticket System** receives customer support tickets through a webhook, processes each ticket individually, uses AI to analyze the customer's request, determines its priority and category, stores the structured result in Google Sheets, and automatically routes the ticket to the appropriate email notification based on its priority.

The result is a faster, more organized, and more consistent support workflow with significantly less manual handling.

---

## 🎯 The Problem

A traditional customer support workflow can require an employee to manually:

- Read every incoming ticket.
- Understand the customer's issue.
- Determine the urgency of the request.
- Identify the support category.
- Summarize the issue.
- Decide what action should be taken.
- Record the ticket in a tracking system.
- Notify the appropriate person or team.

When ticket volume increases, this process becomes time-consuming and increases the risk of inconsistent prioritization or delayed responses.

---

## 💡 The Solution

This workflow transforms incoming support requests into a structured and automated support process.

Instead of manually processing every ticket, the system:

**Receives → Splits → Analyzes → Stores → Routes → Alerts**

Each ticket passes through an automated pipeline where AI extracts meaningful support information and n8n controls the business logic and routing.

---

## 🏢 Role Within a Business Environment

This automation can act as an **AI-powered first layer of a customer support operation**.

It can be positioned between the company's customer-facing systems and its internal support team.

### Business Flow

Customer  
↓  
Support Request  
↓  
Webhook  
↓  
n8n Automation  
↓  
AI Ticket Analysis  
↓  
Priority & Category Detection  
↓  
Google Sheets Record  
↓  
Priority-Based Routing  
↓  
Email Notification  
↓  
Support Team Action

This allows the support team to receive structured and prioritized information instead of manually reviewing every incoming request.

---

## ⚙️ How It Works

### 1. Receive Support Tickets

The workflow starts with a **Webhook** that receives customer support requests.

The incoming data contains information such as:

- Customer name
- Customer email
- Customer message

The webhook provides the entry point for external applications or systems to send support requests into the automation.

---

### 2. Split Tickets

The **Split Tickets** node processes incoming ticket data individually.

This allows the workflow to handle each customer request as a separate item and process it independently.

---

### 3. AI Ticket Analysis

The **AI Ticket Analyzer** uses an OpenAI-powered model to analyze the customer request.

The system transforms an unstructured customer message into structured support information, including:

- Priority
- Category
- Sentiment
- Summary
- Recommended action

This converts raw customer communication into information that can be immediately used by the business.

---

### 4. Store Structured Ticket Data

After analysis, the ticket is stored in **Google Sheets**.

The structured record contains information such as:

| Field | Purpose |
|---|---|
| Customer Name | Identifies the customer |
| Email | Contact information |
| Message | Original support request |
| Priority | Determines urgency |
| Category | Identifies the type of issue |
| Sentiment | Indicates customer sentiment |
| Summary | Condensed description of the issue |
| Recommended Action | Suggested next step |

Google Sheets provides a simple and accessible support tracking layer for the workflow.

---

### 5. Intelligent Priority Routing

The **Route by Priority** Switch node applies business logic to the AI-generated priority.

Tickets are routed according to their priority level.

The workflow contains dedicated paths for:

- Urgent
- High
- Normal
- Fallback

This ensures that different levels of customer issues can trigger different notification processes.

---

### 6. Automated Email Alerts

After routing, Gmail automatically sends the appropriate notification.

This allows support teams to immediately identify tickets requiring attention without manually checking the entire ticket list.

For example:

**Urgent Ticket**

🚨 Immediate attention required.

**High Priority Ticket**

⚠️ Requires prompt investigation.

**Normal Ticket**

📩 Can be handled through the normal support process.

**Fallback**

🔄 Handles unexpected or unsupported priority values safely.

---

## 🧠 AI + Automation Architecture

The project combines two important capabilities:

### Artificial Intelligence

AI is responsible for understanding the customer's message and producing structured support intelligence.

### Workflow Automation

n8n is responsible for executing the business process:

- Receiving data
- Processing tickets
- Connecting services
- Storing information
- Applying routing rules
- Triggering notifications

This separation creates a practical architecture where AI handles **understanding**, while automation handles **execution**.

---

## 🛠️ Technology Stack

- **n8n** — Workflow automation and orchestration
- **OpenAI** — AI-powered ticket analysis
- **Webhooks** — Incoming support ticket endpoint
- **Google Sheets** — Ticket storage and tracking
- **Gmail** — Automated support notifications
- **Postman** — API and webhook testing
- **JSON** — Workflow configuration and data exchange

---

## 🔄 Workflow Architecture

```text
┌──────────────────────────┐
│   Customer Support       │
│        Request           │
└────────────┬─────────────┘
             │
             ▼
┌──────────────────────────┐
│        Webhook            │
│     Receive Ticket        │
└────────────┬─────────────┘
             │
             ▼
┌──────────────────────────┐
│      Split Tickets        │
│   Process Individually    │
└────────────┬─────────────┘
             │
             ▼
┌──────────────────────────┐
│     AI Ticket Analyzer    │
│                          │
│ Priority                 │
│ Category                 │
│ Sentiment                │
│ Summary                  │
│ Recommended Action       │
└────────────┬─────────────┘
             │
       ┌─────┴─────┐
       │           │
       ▼           ▼
┌─────────────┐  ┌──────────────────┐
│   Google    │  │ Route by Priority│
│   Sheets    │  │     Switch       │
└─────────────┘  └────────┬─────────┘
                          │
          ┌───────────────┼───────────────┐
          ▼               ▼               ▼
       Urgent            High           Normal
          │               │               │
          ▼               ▼               ▼
       Gmail             Gmail           Gmail
       Alert             Alert           Alert
