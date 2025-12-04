# IT Operations Automation

This directory contains workflow automation templates for IT operations.

## Overview

Store your IT operations-related automation workflows here, including:

- Infrastructure provisioning
- Monitoring and alerting workflows
- Incident response automation
- Backup and recovery processes
- System maintenance automation

## Getting Started

Add your automation templates to this directory and document them accordingly.

### Scam detector

This workflow is ideal for anyone who needs to quickly and reliably assess the trustworthiness of a website. Whether you're a consumer double-checking a store before making a purchase, a small business owner validating supplier sites, a cybersecurity analyst conducting threat assessments, or a developer building fraud detection into your platform — this tool offers fast, AI-powered insights without the need for manual research or technical expertise. It's designed for both individuals and teams who value accurate, scalable scam detection.

How It Works
The process begins with a simple form submission where the user enters the URL of the website they want to investigate. Once submitted, the workflow activates four specialized AI agents—each powered by GPT-4o and connected to SerpAPI—to independently analyze the site from different angles:

Agent 1 examines domain age, SSL certificates, and TLD trustworthiness.

Agent 2 reviews search engine results, forum mentions, and public scam reports.

Agent 3 analyzes product pricing patterns and brand authenticity.

Agent 4 assesses on-site content quality, grammar, legitimacy of claims, and presence of business info.

Each agent returns its findings, which are then aggregated and passed to a fifth AI agent—the Analyzer. This final agent, powered by GPT-4o mini, evaluates all the input, assigns a scam likelihood score from 1 to 10, and compiles a neatly formatted summary with organized insights and a disclaimer for context.

Set UP
You will need to obtain an Open AI API key from platform.openai.com/api-keys
After you obtain this Open AI API key you will need to connect it to the Open AI Chat Model for all of the Tools agents (Analyzer, Domain & Technical Details, Search Engine Signals, Product & Pricing Patterns, and Content Analysis Tools Agents).
You will now need to fund your Open AI account. GPT 4o costs ~$0.01 to run the workflow.
Next you will need to create a SerpAPI account at https://serpapi.com/users/sign_up
After you create an account you will need to obtain a SerpAPI key.
You will then need to use this key to connect to the SerpAPI tool for each of the tools agents (Domain & Technical Details, Search Engine Signals, Product & Pricing Patterns, and Content Analysis Tools Agents)
Tip: SerpAPI will allow you to run 100 free searches each month. This workflow uses ~5-15 SerpAPI searches per run. If you would like to utilize the workflow more than that each month, create multiple SerpAPI accounts and have an API key for each account. When you utilize all 100 free searches for an account, switch to the API key for another account within the workflow

### Analyze Email Headers for IP Reputation and Spoofing Detection - Gmail

Analyze Emails for Security Insights
Who is this for?
This workflow is ideal for IT professionals, security analysts, and organizations looking to enhance their email security practices. It is particularly useful for those who need to analyze Gmail email headers for IP tracking, spoofing detection, and sender reputation assessment.

What problem is this workflow solving?
Email spoofing and phishing attacks are significant cybersecurity threats. By analyzing email headers, this workflow provides detailed insights into the email's origin, authentication status, and the reputation of the sending IP address. It helps detect potential spoofing attempts and assess the trustworthiness of incoming emails.

What this workflow does
This n8n workflow automates the process of analyzing email headers received in Gmail. It performs the following key functions:

Triggering and Email Header Extraction: It monitors Gmail inboxes for new emails and extracts their headers for analysis.
Authentication Analysis: It validates SPF, DKIM, and DMARC authentication results to ensure the email adheres to industry-standard security protocols.
IP Analysis: The workflow extracts the originating IP address and evaluates its reputation and geographic details using external APIs.
Reputation Scoring: It integrates with IP Quality Score to detect spam activity and assess the sender's reputation.
Consolidation and Webhook Response: All results are aggregated into a single JSON response, making it easy to integrate with third-party platforms or tools for further automation.
Setup
Authenticate Gmail: Configure the Gmail Trigger node with your Gmail account credentials.
API Keys (Optional):
Obtain an API key for IP Quality Score (https://ipqualityscore.com).
Ensure the IP-API endpoint is accessible.
This step is optional as ipqualityscore.com will provide a limited number of free lookups each month. See more details here.
Activate the Workflow: Ensure the workflow is active to process incoming emails in real-time.
How to customize this workflow to your needs
Add Alerts: Use the Gmail - Respond to Webhook node to trigger notifications in Slack, email, or any other communication channel.
Integrate with SIEM: Forward the workflow output to SIEM tools like Splunk or ELK Stack for further analysis.
Modify Validation Rules: Update SPF, DKIM, or DMARC logic in the Set nodes to align with your organization’s security policies.
Expand IP Analysis: Add more APIs or services to enrich IP reputation data, such as VirusTotal or AbuseIPDB.

# Ai-orchestrator

This workflow is designed to intelligently route user queries to the most suitable large language model (LLM) based on the type of request received in a chat environment. It uses structured classification and model selection to optimize both performance and cost-efficiency in AI-driven conversations.

It dynamically routes requests to specialized AI models based on content type, optimizing response quality and efficiency.

Benefits
Smart Model Routing: Reduces costs by using lighter models for general tasks and reserving heavier models for complex needs.
Scalability: Easily expandable by adding more request types or LLMs.
Maintainability: Clear logic separation between classification, model routing, and execution.
Personalization: Can be integrated with session IDs for per-user memory, enabling personalized conversations.
Speed Optimization: Fast models like GPT-4.1 mini or Gemini Flash are chosen for tasks where speed is a priority.
How It Works
Input Handling:

The workflow starts with the "When chat message received" node, which triggers the process when a chat message is received. The input includes the chat message (chatInput) and a session ID (sessionId).
Request Classification:

The "Request Type" node uses an OpenAI model (gpt-4.1-mini) to classify the incoming request into one of four categories:
general: For general queries.
reasoning: For reasoning-based questions.
coding: For code-related requests.
search: For queries requiring search tools.
The classification is structured using the "Structured Output Parser" node, which enforces a consistent output format.
Model Selection:

The "Model Selector" node routes the request to one of four AI models based on the classification:
Opus 4 (Claude 4 Sonnet): Used for coding requests.
Gemini Thinking Pro: Used for reasoning requests.
GPT 4.1 mini: Used for general requests.
Perplexity: Used for search (Google-related) requests.
AI Processing:

The selected model processes the request via the "AI Agent" node, which includes intermediate steps for complex tasks.
The "Simple Memory" node retains session context using the provided sessionId, enabling multi-turn conversations.
Output:

The final response is generated by the chosen model and returned to the user.
Set Up Steps
Configure Trigger:

Ensure the "When chat message received" node is set up with the correct webhook ID to receive chat inputs.
Define Classification Logic:

Adjust the prompt in the "Request Type" node to refine classification accuracy.
Verify the output schema in the "Structured Output Parser" node matches expected categories (general, reasoning, coding, search).
Connect AI Models:

Link each model node (Opus 4, Gemini Thinking Pro, GPT 4.1 mini, Perplexity) to the "Model Selector" node.
Ensure credentials (API keys) for each model are correctly configured in their respective nodes.
Set Up Memory:

Configure the "Simple Memory" node to use the sessionId from the input for context retention.
Test Workflow:

Send test inputs to verify classification and model routing.
Check intermediate outputs (e.g., request_type) to ensure correct model selection.
Activate Workflow:

Toggle the workflow to "Active" in n8n after testing.
