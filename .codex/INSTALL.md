# Installing SwapBox Skills for Codex

Enable SwapBox skills in Codex via native skill discovery. Just clone and symlink.

## Prerequisites

- Git

## Installation

1. **Clone the repository:**

   ```bash
   git clone https://github.com/AboPlus/swapbox-skills ~/.codex/swapbox-skills
   ```

2. **Create the skills symlink:**

   ```bash
   mkdir -p ~/.agents/skills
   ln -s ~/.codex/swapbox-skills/skills ~/.agents/skills/swapbox-skills
   ```

   **Windows (PowerShell):**

   ```powershell
   New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.agents\skills"
   cmd /c mklink /J "$env:USERPROFILE\.agents\skills\swapbox-skills" "$env:USERPROFILE\.codex\swapbox-skills\skills"
   ```

3. **Restart Codex** (quit and relaunch the CLI) to discover the skills.

## Verify

```bash
ls -la ~/.agents/skills/swapbox-skills
```

You should see the three skill directories: `swapbox-price`, `swapbox-swap`, `swapbox-bridge`.

## Available Skills

| Skill | When to Use |
|-------|-------------|
| `swapbox-price` | Token price queries against USDT across 30+ chains |
| `swapbox-swap` | On-chain DEX swap execution (Coming Soon) |
| `swapbox-bridge` | Cross-chain bridge transfers (Coming Soon) |

## Updating

```bash
cd ~/.codex/swapbox-skills && git pull
```

Skills update instantly through the symlink.

## Uninstalling

```bash
rm ~/.agents/skills/swapbox-skills
```

Optionally delete the clone: `rm -rf ~/.codex/swapbox-skills`.
