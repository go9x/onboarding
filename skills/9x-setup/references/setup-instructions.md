# Quick Reference: 9x Setup Commands

## GitHub CLI Installation
```bash
# Mac
brew install gh

# Windows: Download from https://cli.github.com/
# Linux: Use package manager (apt, yum, etc.)
```

## GitHub Authentication
```bash
gh auth login
# Select: GitHub.com → HTTPS → Browser login → Grant all permissions

# Verify
gh auth status
```

## Check Organization Access
```bash
gh api user/orgs --jq '.[].login' | grep -i "go9x"
```

## Add Private Marketplace (Claude Code)
```bash
mkdir -p ~/.claude && (cat ~/.claude/settings.json 2>/dev/null || echo '{}') | python3 -c "
import json, sys
s = json.load(sys.stdin)
s.setdefault('extraKnownMarketplaces', {})['go9x-skills'] = {
    'source': {'source': 'github', 'repo': 'go9x/skills'}
}
s.setdefault('enabledPlugins', {})['go9x-skills@go9x-skills'] = True
json.dump(s, sys.stdout, indent=2)
" > ~/.claude/settings.json.tmp && mv ~/.claude/settings.json.tmp ~/.claude/settings.json
```

## Add Private Marketplace (Cowork UI)
1. Open Cowork
2. Click "Plugins" in left sidebar
3. Click "Add Marketplace from GitHub"
4. Enter: `go9x/skills`
5. Click "Add"

## Verify Installation
```bash
# Claude Code
/skills list

# Cowork
Check Plugins sidebar for 9x skills
```

## Troubleshooting

### gh command not found
```bash
# Mac
brew install gh

# Verify
which gh
```

### Not authenticated
```bash
gh auth logout
gh auth login
```

### No org access
Contact PYV, Roger, Alex, or Jan to be added to go9x GitHub organization.

### Marketplace won't add
- Verify GitHub authentication: `gh auth status`
- Verify org access: `gh api user/orgs --jq '.[].login'`
- Check correct repo: `go9x/skills`
- Restart Cowork/Claude Code after adding
