    Self-Improving AI Brain
    
    A complete system that connects Obsidian (permanent knowledge) with Hermes Agent (execution + automation) to create a self-improving second brain that thinks, remembers, and acts.
    
    Why This Exists
    
    Most productivity systems have a fundamental problem:
    
    - Obsidian alone → Stores everything but cannot act on it
    - AI agents alone → Can act but forget everything when the session ends
    
    This project solves that by making Obsidian the permanent knowledge layer and Hermes the intelligence + execution layer.
    
    What We Built
    
    A full system with:
    
    - Structured Obsidian vault with clear folder architecture
    - Multiple Hermes skills that read from and write to the vault
    - Automatic morning briefs, inbox processing, project health monitoring, and weekly synthesis
    - All adapted to work with Grok (via X Premium) instead of Claude
    
    Key Adaptation: Grok + X Premium (No Claude)
    
    The original guide was built around Claude. We adapted everything to work with Grok because:
    
    - User has X Premium (gives access to Grok)
    - No direct Anthropic API key / Claude subscription
    - Grok-4.3 via xai-oauth provider works well for this use case
    
    We used the same model that powers this conversation (grok-4.3 via xai-oauth).
    
    Vault Structure
    
    
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
    
    
    Skills Created
    
    | Skill               | Status  | Description                            |
    |---------------------|---------|----------------------------------------|
    | inbox-processor     | Working | Automatically files items from INBOX   |
    | project-health      | Working | Weekly project status reports          |
    | connection-finder   | Working | Finds hidden connections between notes |
    | weekly-synthesis    | Created | Weekly review + priority update        |
    | vault-morning-brief | Partial | Morning brief with header image        |
    
    How to Install Hermes Agent (Step by Step)
    
    1. Install Hermes
    
    bash
    curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
    
    
    2. Verify Installation
    
    bash
    hermes --version
    hermes doctor
    
    
    3. Set Up Grok (X Premium)
    
    Since we're using Grok via X Premium instead of Claude:
    
    bash
    hermes model
    
    
    Select grok-4.3 or the available Grok model via xai-oauth.
    
    4. Configure Filesystem MCP
    
    bash
    hermes mcp add filesystem --command 'npx -y @modelcontextprotocol/server-filesystem /path/to/your/vault'
    
    
    Then enable it:
    
    bash
    hermes mcp configure filesystem
    
    
    5. Create Your Vault Structure
    
    Follow the folder structure shown above.
    
    6. Create SYSTEM.md
    
    Create 06 - SYSTEM/SYSTEM.md with your personal context (who you are, priorities, vault rules, etc.).
    
    7. Create Skills
    
    Place skill files in ~/.hermes/skills/ following the format used in this repo.
    
    How It Works
    
    1. SYSTEM.md acts as the master context file (read by Hermes at the start of every skill)
    2. Filesystem MCP gives Hermes direct read/write access to the vault
    3. Skills follow a structured process: Read → Reason → Write back to vault
    4. Grok handles all reasoning (via X Premium / xai-oauth)
    
    Future Improvements
    
    - Enable automatic image generation for daily briefs
    - Add more skills (Research Converter, Thinking Partner)
    - Connect X posting workflow
    - Add daily note template
    
    Tech Stack
    
    - Obsidian – Knowledge base
    - Hermes Agent – Automation + execution
    - Grok-4.3 (via X Premium) – Reasoning model
    - Filesystem MCP – Vault access
    
    License
    
    MIT
