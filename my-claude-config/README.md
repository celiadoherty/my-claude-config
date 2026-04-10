# my-claude-config

Custom Claude Cowork skills built by Celia Doherty for tem Energy.

## What's in here

This repo contains my custom skills — instruction sets that tell Claude how to handle specific recurring tasks. Each skill lives in its own folder under `skills/` and contains a `SKILL.md` file (the core instructions) plus any reference files it needs.

## Skills

| Skill | What it does |
|-------|-------------|
| `tem-battlecard` | Generates competitor battlecards for the sales team |
| `tem-battlecard-update` | Updates existing battlecards with new competitive intel |
| `tem-voice` | Applies tem's brand voice to any written content |
| `tem-tone-of-voice` | Reviews and enforces tem's tone of voice guidelines |
| `tem-product-context` | Loads tem's full product and market context for any task |
| `tem-project-builder` | Guides creation of TEM Heartbeat project documents |
| `one-on-one-prep` | Prepares agendas and talking points for 1:1 meetings |
| `bio-feedback` | Structures feedback using the BIO format (Behaviour, Impact, Options) |
| `log` | End-of-session learning logger that writes to Notion |

## How to use

These skills are used in Claude Cowork. To install them, copy the `skills/` folder into your `.claude/skills/` directory.

## Updating

When you create or update a skill in Cowork, copy the updated files here and push to keep this repo in sync.
