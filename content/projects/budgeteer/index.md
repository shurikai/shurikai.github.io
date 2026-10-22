+++
date = '2026-10-22T09:02:00-04:00'
draft = false
title = 'Budgeteer'
status = 'active'
github = 'https://github.com/shurikai/budgeteer'
description = 'A shared envelope-budgeting app for two people who just want to know where the money goes.'
summary = 'A shared envelope-budgeting app for two people who just want to know where the money goes.'
weight = 2
+++

**Repo:** [github.com/shurikai/budgeteer](https://github.com/shurikai/budgeteer)  
**Stack:** Python, FastAPI, PostgreSQL, Redis, ARQ, Anthropic SDK, React + TypeScript (in progress)

## Why I built it

My wife and I wanted a simple way to see where our money was going. Every budgeting app we tried was too
expensive, too complicated, or both. So I'm building the one we actually want.

## What it is

An envelope-style budgeting app: money gets assigned to categories, and spending draws them down. It's
built around a *household* that more than one person can share, rather than a single user, because
budgeting is a shared activity in our house.

It is deliberately not an accounting system. No double-entry ledgers, no investment tracking, just
something that works without getting in the way.

## How it's put together

- **FastAPI and PostgreSQL** for the API, with SQLAlchemy models and Alembic migrations covering
  households, members, accounts, budgets, categories, and transactions
- **Token auth with refresh tokens**, since two people on different devices need to stay signed in
- **Redis and ARQ** for background jobs, so slow work like categorization stays out of the request path
- **Anthropic SDK** for transaction categorization and plain-language spending insights

## Status

The data model, API routes, auth, and core domain logic are in place. The AI features and the React
frontend are in progress.
