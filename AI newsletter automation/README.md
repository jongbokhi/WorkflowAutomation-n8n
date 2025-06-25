# 📰 AI Newsletter Automation with n8n

This repository contains a modular, AI-powered newsletter automation system built with [n8n](https://n8n.io). It enables dynamic content curation using live news, academic research, and GPT-based agents — fully automated from input to email delivery.

---

## 📦 Included Workflows

### 1. `AI_agent_News_Automation` – Main Automation

The primary workflow that:
- Accepts user input via form (topic + target audience)
- Plans a newsletter structure using OpenAI agent
- Invokes sub-workflows to gather latest news and papers
- Aggregates, refines, and formats the newsletter as HTML
- Sends the result via Gmail

**Core Components:**
- `Form Trigger`: Collects user input (`Topic`, `Target Audience`)
- `OpenAI Agent (Newsletter Expert)`: Crafts table of contents based on topic
- `Project Planner`: Splits the content into sections
- `News & Paper Splitters`: Processes and labels content types
- `News Research Team` / `Paper Research Team`: Summarizes and edits
- `Editor`: Formats final newsletter into email-ready HTML
- `Send Newsletter`: Dispatches via Gmail

---

### 2. `Tavily_Search_Tool` – Real-time News Fetcher

A lightweight workflow used to fetch up-to-date internet news related to the topic using the **Tavily API**.

**Steps:**
- Accepts a dynamic query
- Sends a POST request to `https://api.tavily.com/search`
- Retrieves top 3 news sources with full content
- Formats them into a unified response

**Used By:** The main workflow (`AI_agent_News_Automation`) through a `Tool Workflow` node.

---

### 3. `Arxiv_Search_Tool` – Academic Paper Fetcher

Fetches recent papers related to the topic using Arxiv’s public API.

**Steps:**
- Calls `http://export.arxiv.org/api/query` with search term
- Parses XML using a `Code` node (JavaScript)
- Extracts title, summary, date, authors, and link for each paper
- Returns a structured JSON list of results

**Used By:** The main workflow via `Tool Workflow` call.

---

## ⚙️ How It Works (End-to-End Flow)

1. **User Submission**  
   → Enters newsletter topic & target audience through form

2. **Newsletter Planning**  
   → OpenAI agent analyzes input and creates a Table of Contents  
   → Sub-workflows (`Tavily` & `Arxiv`) are triggered to fetch actual content

3. **Content Processing**  
   → Content is split by type (news vs papers)  
   → Specialized agents summarize each section based on audience profile

4. **Formatting**  
   → News and paper sections are merged and edited into professional HTML

5. **Delivery**  
   → Final newsletter is emailed to a specified address

---

## ✨ Features

- ✅ Low-code automation with modular n8n workflows
- 🔍 Live news retrieval via Tavily
- 📚 Paper extraction and summarization from Arxiv
- 🤖 AI agents for newsletter design and editing
- 📧 Automated email sending via Gmail
- 🧩 Fully customizable and scalable

---

## 🔐 API & Credential Setup

To run this system, set up the following:

| Service | Use | Notes |
|--------|-----|-------|
| Tavily | News search | Requires `api_key` |
| Arxiv | Paper search | No API key needed |
| OpenAI | Content planning & editing | Needs OpenAI API credentials |
| Gmail | Email delivery | OAuth2 setup in n8n |

