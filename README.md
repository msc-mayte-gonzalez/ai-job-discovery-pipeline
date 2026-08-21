# AI-Assisted Job Discovery Pipeline

A personal automation system that monitors **41 company career sites**, filters irrelevant roles using deterministic logic, and uses Claude Haiku to evaluate the remaining jobs based on transferable capabilities rather than job-title similarity.

I built it with **n8n, Claude, Browserless, APIs, Google Sheets, and Gmail** to make my own job search broader and more systematic.

## Demo version

This repository contains a **sanitized representative version** of the workflow.

The production system monitors 41 career sites across multiple ATS platforms. The public demo includes only a small subset of integrations to show the core architecture, filtering logic, AI matching, and output flow without publishing the full production implementation.

## Workflow overview

![n8n workflow overview](Workflow-overview.png)
