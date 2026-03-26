# quantxiv — Project Goal

## What
A public, moderated discussion platform for quantum computing research papers — think arxiv + Reddit + Stocktwits, purpose-built for the quantum computing research community.

## Problem
Thousands of quantum computing papers are published on arxiv annually. No dedicated community exists to discuss them. Researchers fall back on LinkedIn/Twitter where discussions rarely form or die quickly.

## Solution: quantxiv.com
A web platform where:
- arxiv papers (quantum computing) are surfaced/imported as discussion threads
- Users can comment, reply, react to papers and comments
- Content is moderated to maintain research-grade quality
- A global community of researchers, engineers, and enthusiasts can engage

## Core Features (MVP)
1. **Paper feed** — auto-ingested quantum computing papers from arxiv API, sorted by recency/activity
2. **Paper page** — abstract, metadata, link to full paper, threaded comments
3. **Comments & reactions** — nested threading, upvotes/reactions
4. **User accounts** — sign up, profiles, posting history
5. **Moderation** — flag/remove low-quality content, mod roles

## Users
- Quantum computing researchers and academics
- Engineers working in quantum (industry/startups)
- Students and enthusiasts following the field

## Stack Decisions (TBD)
- Frontend: web-first, fast, clean UI
- Backend: API-driven
- Data source: arxiv API (`export.arxiv.org/api/query`)
- Auth: email or OAuth
- Hosting: TBD

## Success Metric
quantxiv.com becomes the default place where quantum computing researchers discuss new papers.
