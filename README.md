# Forgejo-with-Woodpecker-CI-Stack
Local forgejo + woodpecker CI Docker compose stack file. With this compose, you can have Forgejo and Woodpecker instances instantly.


# 🐳 Forgejo + Woodpecker CI – Docker Compose Setup

## This repository contains a full Docker Compose setup for running:

- Forgejo – a self-hosted Git service (lightweight GitHub/Gitea alternative)
- Woodpecker CI – a modern, lightweight continuous integration system

## The stack includes:

- Forgejo Git server
- Woodpecker server
- Woodpecker agent
- PostgreSQL connection support
- Shared Docker networks & persistent volumes

# 🧱 Components
## Forgejo

A lightweight, community-driven Git hosting platform compatible with Gitea.
This service exposes:

- Web UI on port 3000
- SSH Git access on port 222

Forgejo is configured to use an external PostgreSQL database and supports Actions.

## Woodpecker Server

The CI server responsible for:

- Receiving Forgejo webhooks
- Managing builds & pipelines
- Providing UI on port 8001

It integrates directly with Forgejo using OAuth credentials.

## Woodpecker Agent

Executes CI pipelines sent by the server.
It supports Docker builds using the mounted Docker socket.

## 📦 Volumes

The compose file defines persistent volumes for:

- forgejo_data → Forgejo repositories, configs, users
- woodpecker-server-data → Woodpecker pipelines & metadata
- woodpecker-agent-config → Agent configuration

These ensure data survives container restarts and updates.

## 🌐 Networking

All services communicate over a dedicated internal Docker network:

    forgejo_net


This isolates traffic and keeps internal communication secure and stable.

## 🔧 Configuration Notes

Before running the stack:

- Replace placeholder values such as:
    - < postgresql ip or url >
    - < forgejo ip or url >
    - < woodpecker ip or url >
    - OAuth client & secret keys
    - Database credentials
- Ensure your PostgreSQL instance is reachable.
- Generate OAuth credentials inside Forgejo for Woodpecker.

## ▶️ Usage

Start the stack:

    docker compose up -d


Stop:

    docker compose down


View logs:

    docker compose logs -f
