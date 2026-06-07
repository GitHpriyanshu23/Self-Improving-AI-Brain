# Agentic AI Memory

![Hermes-Agent + Obsidian Header](assets/header.png)

![Self-Improving AI Brain Logo](assets/logo.jpg)

A complete system that connects Obsidian (permanent knowledge) with Hermes Agent (execution + automation) to create a self-improving second brain that thinks, remembers, and acts.

## Why this exists

Most knowledge workflows fall into two camps:

- Obsidian alone — stores everything but cannot act on it
- AI agents alone — can act but forget state between sessions

This project combines a permanent knowledge vault (Obsidian) with an execution layer (Hermes Agent) so the system can remember, reason, and act.

## What we built

- Structured Obsidian vault with a clear folder architecture
- Hermes skills that read from and write to the vault
- Automated briefs, inbox processing, project monitoring, and weekly synthesis
- Adapted to use Grok (via X Premium) instead of Claude

### Key adaptation: Grok + X Premium

This repo uses Grok (grok-4.3) via X Premium and `xai-oauth` as the reasoning model. If you don't have an Anthropic/Claude subscription, Grok is the supported alternative here.

## Vault structure

Example Obsidian vault layout:

```
ObsessVault/
├── 00 - INBOX/                    # Raw captures (processed automatically)
├── 01 - NOTES/
│   ├── permanent/                 # Atomic notes
│   ├── daily/                     # Daily notes
│   └── meetings/
├── 02 - PROJECTS/                 # Active projects
├── 03 - RESOURCES/                # Reference material
├── 04 - HERMES-OUTPUTS/           # All auto-generated content
│   ├── briefings/
│   ├── analyses/
│   ├── reviews/
│   └── syntheses/
├── 05 - ARCHIVE/
└── 06 - SYSTEM/
    └── SYSTEM.md                  # Master context file for Hermes
```

## Skills

| Skill               | Status  | Description                            |
|---------------------|---------|----------------------------------------|
| inbox-processor     | Working | Automatically files items from INBOX   |
| project-health      | Working | Weekly project status reports          |
| connection-finder   | Working | Finds hidden connections between notes |
| weekly-synthesis    | Created | Weekly review + priority update        |
| vault-morning-brief | Partial | Morning brief with header image        |

## Installation & setup

1) Install Hermes Agent

Run the official install script:

```bash
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
```

Hermes Agent repo: https://github.com/NousResearch/hermes-agent

2) Verify installation

```bash
hermes --version
hermes doctor
```

3) Select/Configure Grok model (X Premium)

```bash
hermes model
```

Choose `grok-4.3` (or another available Grok model) via the `xai-oauth` provider.

4) Configure the Filesystem MCP

```bash
hermes mcp add filesystem --command 'npx -y @modelcontextprotocol/server-filesystem /path/to/your/vault'
hermes mcp configure filesystem
```

5) Create your vault and `SYSTEM.md`

Follow the vault structure above and create `06 - SYSTEM/SYSTEM.md` with your personal context, priorities, and vault rules.

6) Add skills

Place skill files in `~/.hermes/skills/` following the examples in this repository.

## How it works

1. `SYSTEM.md` acts as the master context file (read by Hermes at skill startup)
2. Filesystem MCP gives Hermes read/write access to your vault
3. Skills follow: Read → Reason → Write back to vault
4. Grok (via X Premium) provides reasoning and model behaviour

## Future improvements

- Automatic image generation for daily briefs
- More skills (Research Converter, Thinking Partner)
- X posting workflow integration
- Daily note templates

## Tech stack

- Obsidian — knowledge base
- Hermes Agent — automation & execution
- Grok-4.3 (via X Premium) — reasoning model
- Filesystem MCP — vault access

## Using the header image

Place the header image file you provided in this repository at `assets/header.png`. If you prefer a different filename, update the image path at the top of this README.

## License

MIT
