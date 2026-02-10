# 9x Team Onboarding for Cowork

Public marketplace for onboarding 9x team members to use private 9x skills in Claude Cowork.

## What This Is

This is a **public** onboarding marketplace that helps 9x team members install **private** 9x skills in Cowork. It contains a setup skill that guides users through:

1. GitHub CLI authentication
2. Adding the private `go9x/skills` marketplace
3. Installing all 9x team skills
4. Next steps for API credential setup

## For 9x Team Members

### Getting Started

1. **Open Cowork** (Claude Desktop on Mac)
2. **Click "Plugins"** in the left sidebar
3. **Click "Add Marketplace from GitHub"**
4. **Enter:** `go9x/onboarding`
5. **Click "Add"**
6. **Ask Claude:** "Help me set up 9x skills"

Claude will guide you through the rest!

### Prerequisites

- **Mac with Cowork** (Claude Desktop)
- **GitHub account** with access to the go9x organization
- **Homebrew** (for installing GitHub CLI if needed)
- **Terminal access** (for one-time GitHub authentication)

### What You'll Get

After setup, you'll have access to these 9x skills in Cowork:

- **Attio CRM:** Contact management, outreach sequences, event attendees
- **Sales:** Follow-up generators, offer creators, deal management
- **Content:** Tutorial and demo generators
- **Notion:** Task management and workspace integration
- **And more:** Circle, Framer, Slack utilities

Just talk to Claude naturally, and it will use the right skill automatically:
- "Add sarah@example.com to Attio outreach"
- "Generate a follow-up email for the Acme deal"
- "Create a Notion task to call John tomorrow"

## Security

### Public vs Private

- **This repo (go9x/onboarding):** PUBLIC
  - Contains only the setup skill
  - No sensitive information
  - No API keys or credentials
  - Just guides users through adding the private marketplace

- **The skills repo (go9x/skills):** PRIVATE
  - Contains all actual team skills
  - Handles API credentials
  - Only accessible to go9x organization members
  - GitHub enforces access control

### Access Control

Only members of the go9x GitHub organization can access the private skills repo. This is enforced by GitHub and cannot be bypassed.

If you're not in the organization, the setup will guide you to request access from:
- PYV (pyv@go9x.com)
- Roger
- Alex
- Jan

## Repository Structure

```
go9x-onboarding/
├── .claude-plugin/
│   ├── marketplace.json       # Marketplace metadata
│   └── plugin.json           # Plugin configuration
├── skills/
│   └── 9x-setup/             # Setup skill for Cowork
│       ├── SKILL.md          # Main skill definition
│       └── references/
│           └── setup-instructions.md  # Command reference
└── README.md                 # This file
```

## For Admins

### Updating the Setup Skill

1. Edit `skills/9x-setup/SKILL.md`
2. Commit and push to GitHub
3. Cowork will automatically use the latest version from the marketplace

### Adding to Onboarding

Include this in new team member onboarding:
1. Ensure they have Mac with Cowork installed
2. Ensure they're added to go9x GitHub organization
3. Share link to this README or Notion onboarding doc
4. They follow "Getting Started" steps above

### Monitoring Usage

Users who complete setup will:
1. Be authenticated with GitHub
2. Be members of go9x organization
3. Have the private marketplace added in Cowork
4. Have access to all private skills

Track by monitoring private repo access in GitHub.

## Troubleshooting

### Common Issues

**"GitHub CLI not found"**
- The setup skill will guide installation: `brew install gh`
- One-time setup, then it's available forever

**"Not authenticated with GitHub"**
- The setup skill will guide: `gh auth login`
- Use browser authentication (easiest)
- Grant requested permissions

**"No access to go9x organization"**
- User needs invitation to go9x GitHub org
- Contact PYV, Roger, Alex, or Jan
- Cannot proceed without org membership

**"Private marketplace won't add"**
- Verify GitHub authentication in Terminal: `gh auth status`
- Verify org access: `gh api user/orgs --jq '.[].login' | grep go9x`
- Restart Cowork after adding marketplace

**"Skills don't appear"**
- Quit and reopen Cowork completely
- Check Plugins sidebar shows go9x-skills marketplace
- Verify you're signed into correct GitHub account

## Support

For help with setup:
- **Technical issues:** Contact Roger, Alex, or Jan
- **Access requests:** Contact PYV (pyv@go9x.com)
- **General questions:** #tech channel on Slack

## License

Internal use only - 9x team members.

---

**Maintained by:** 9x Technical Team
**Last updated:** February 2026
