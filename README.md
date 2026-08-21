# AI-Assisted Job Discovery Pipeline

A personal automation system that monitors **41 company career sites**, filters irrelevant roles using deterministic logic, and uses Claude Haiku to evaluate the remaining jobs based on transferable capabilities rather than job-title similarity.

I built it with **n8n, Claude, Browserless, APIs, Google Sheets, and Gmail** to make my own job search broader and more systematic.

## Demo version

This repository contains a **sanitized representative version** of the workflow.

The production system monitors 41 career sites across multiple ATS platforms. The public demo includes only a small subset of integrations to show the core architecture, filtering logic, AI matching, and output flow without publishing the full production implementation.

## Why I built it

My background spans scientific research, UX research, product work, and customer-facing work, so relevant opportunities don't always share the same job title.

I built this system to search by **underlying capability rather than title alone**, while reducing the manual work of repeatedly checking dozens of company career pages.

## How it works

1. Fetches job postings from multiple career platforms
2. Normalizes them into a common format
3. Applies deterministic title and location filters
4. Removes jobs already seen
5. Sends only the remaining roles to Claude Haiku
6. Parses the response into structured fit data
7. Writes matches to Google Sheets and sends an email digest

Keeping deterministic logic before the AI step reduces unnecessary API calls and keeps normal operating cost around **$1.50–3 CAD/month**.

## Key design decisions

### Deterministic before AI

Title filtering, location filtering, and deduplication happen before Claude is called. These decisions don't require an LLM, so handling them with rules makes the workflow cheaper and more predictable.

### Two-layer deduplication

Jobs are checked by both **URL** and **company + title**, which catches reposted roles even when their URLs change.

### AI for interpretation

Claude is used only where judgment is useful: evaluating whether my past experience demonstrates the underlying capabilities a role requires, even when the job title is unfamiliar.

### Structured outputs

Each evaluated role returns a consistent set of fields such as match score, recommendation, transferable strengths, genuine gaps, risk factors, and a short fit narrative.

## Built with AI

I built this system using **Claude as a coding and debugging collaborator**.

I defined the problem, workflow architecture, filtering rules, edge cases, and product decisions, while using Claude to help write and troubleshoot JavaScript, API requests, and n8n logic.

The project became a practical way to use AI to extend my technical capabilities and turn an idea into a working system.

## Limitations and next improvements

This is a working personal system, not a production job-search product.

Current limitations include:

* Career sites can change their APIs or page structure, which can break individual sources.
* Some sites expose incomplete job descriptions or block automated access entirely.
* Deterministic filters can occasionally remove a role that might have been worth reviewing.
* AI fit assessments are useful for prioritization, but they are not treated as final decisions.

If I continued developing it, I would add better source-health monitoring, clearer confidence indicators for incomplete job data, and automated tests for the filtering and parsing logic.

## Explore the demo

[`workflow-demo.json`](workflow-demo.json) is a sanitized, representative n8n workflow showing the core architecture without the full production implementation.

To inspect it, download the JSON and import it into n8n. Credentials and personal configuration have been replaced with placeholders.


## Workflow overview

![n8n workflow overview](Workflow-overview.png)

## Sample output

The workflow writes structured match assessments to Google Sheets for quick review.

![Sample job match output](sample-output.png)
