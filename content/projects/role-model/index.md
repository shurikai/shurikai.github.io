+++
date = '2026-10-22T09:03:00-04:00'
draft = false
title = 'Role Model'
status = 'active'
github = 'https://github.com/shurikai/role-model'
description = 'A career knowledge base that builds tailored resumes where every bullet traces back to its source.'
summary = 'A career knowledge base that builds tailored resumes where every bullet traces back to its source.'
tags = ['go', 'ai']
weight = 1
+++

**Repo:** [github.com/shurikai/role-model](https://github.com/shurikai/role-model)  
**Stack:** Go, PostgreSQL, Anthropic SDK, React + TypeScript, Python (renderer and onboarding agent)

## Why I built it

I was tailoring my resume for every application with an LLM's help, and each version drifted a little
further from the truth. A "contributed to" became "led" over a few rounds, and a client picked up a
city I'd never worked in. I wrote about that in
[How Your Resume Lies While Telling the Truth](/posts/how_your_resume_lies/).

The fix wasn't a better prompt. It was to stop editing resumes and start generating them from a single,
human-written source of truth.

## What it does

Role Model keeps a career as structured data instead of a document. Work is stored as small
*contribution* records, each more detailed than any resume bullet would be. They attach to positions,
and positions attach to employers. When I apply somewhere, the system queries that data and builds a
resume from the contributions that fit the role.

The pipeline has two stages:

1. **Extract the job description.** One LLM call pulls out structured signals: seniority, required and
   preferred skills, competency asks, culture signals.
2. **Generate the resume.** SQL retrieval selects relevant contributions, and the model writes bullets
   from them under a length budget. A second call writes the summary, and it only sees the bullets the
   first call chose, so it can't claim things the bullets don't support.

Between the two sits a **fit gate**: deterministic scoring in plain Go. The model writes the
explanation, but it doesn't produce the scores.

## Decisions I'd make again

- **Provenance on every bullet.** Each generated bullet carries the IDs of the contributions it came
  from. If something looks off, "where did that come from?" always has an answer.
- **SQL retrieval, not a vector store.** My data is structured, so WHERE clauses, joins, and a
  hand-maintained alias table do the matching. I explain why in
  [Oops! All Ragtime!](/posts/oops-all-ragtime/).
- **Deliberately not agentic.** Each generation stage is one LLM call with a fixed input shape and a
  validated JSON output, and a human reviews the result. The one exception is onboarding, a
  conversational LangGraph agent for entering career history, where exploring is the point.
- **Prompts are versioned like code.** Prompts are compiled into the binary, and each generation records
  the git hash of the prompt that produced it.
- **Self-hosted by design.** One person, one instance, one database, your own API key. Nothing leaves
  your machine.

## Where it's going

End to end works today: paste a job description, get a `.docx`. Next up is making it usable by people
who aren't me, then an MCP server so any MCP client can query the career data directly.
