# 9x Team Setup Skill

## Description
Setup skill for 9x team members using Cowork. Guides users through GitHub authentication and installation of private 9x skills from the go9x/skills marketplace.

## Usage
After adding the `go9x/onboarding` marketplace, run this skill to complete your setup.

## What This Skill Does

Guides you through:
1. GitHub CLI authentication (if needed)
2. Adding the private go9x/skills marketplace
3. Installing 9x team skills
4. Setting up API credentials (handled by private skills)

## Instructions for Claude

When a user invokes this skill, guide them interactively:

### Step 1: Welcome & Context

Greet them warmly:
```
Welcome to 9x! 🎉

You've successfully added the public onboarding marketplace. Now let's get you access to the private 9x team skills.

This will take about 5 minutes. Ready to get started?
```

### Step 2: Create GitHub Personal Access Token

Explain what's needed:
```
To access the private 9x skills, you'll need a GitHub Personal Access Token.

This is a one-time setup that takes about 2 minutes. I'll walk you through it!
```

**Guide them step-by-step:**

1. **Open GitHub settings:**
   "Open this link in your browser: https://github.com/settings/tokens"

2. **Create token:**
   - Click **"Generate new token"** (or "Generate new token (classic)")
   - Give it a name: `Cowork - 9x Skills`
   - Set expiration: **No expiration** (or 1 year if you prefer)
   - Select scopes: Check **`repo`** (this gives access to private repositories)
   - Scroll down and click **"Generate token"**

3. **Copy the token:**
   "⚠️ Important: Copy the token NOW. You won't be able to see it again!"

   The token will look like: `ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx`

4. **Save it temporarily:**
   "Paste the token somewhere safe for the next step (like a note). We'll use it in just a moment."

Ask them: "Do you have the token copied? Reply with 'yes' when ready."

### Step 3: Set GitHub Token

Once they confirm they have the token, guide them:

```
Great! Now we'll save this token so Cowork can access the private skills.

Open your Terminal app and paste this command (replace YOUR_TOKEN with your actual token):

echo 'export GITHUB_TOKEN="YOUR_TOKEN_HERE"' >> ~/.zshrc && source ~/.zshrc

For example:
echo 'export GITHUB_TOKEN="ghp_abc123xyz789"' >> ~/.zshrc && source ~/.zshrc
```

**Wait for them to complete this step.**

Then verify it worked:
```bash
echo $GITHUB_TOKEN
```

They should see their token printed. If they see nothing, the token wasn't set correctly.

Show celebration: "✅ GitHub token configured!"

### Step 4: Verify Token Works

Quick test to ensure the token has access:
```bash
curl -H "Authorization: token $GITHUB_TOKEN" https://api.github.com/user/orgs | grep -i "go9x"
```

**If they see "go9x" in the output:**
"✅ Perfect! Your token has access to the go9x organization."

**If they get an error or don't see go9x:**
```
⚠️ It looks like you're not in the go9x GitHub organization yet, OR your token doesn't have the right permissions.

Two things to check:
1. Make sure you selected the 'repo' scope when creating the token
2. Make sure you're a member of the go9x GitHub organization

To join the organization, contact:
- PYV (pyv@go9x.com)
- Roger
- Alex
- Jan

Once you're added, you may need to create a new token.
```

Stop here if no access.

### Step 5: Verify Organization Access

This is critical. Check if they have access to go9x:
```bash
gh api user/orgs --jq '.[].login' | grep -i "go9x"
```

**If they have access:**
Show: "✅ Confirmed! You're a member of the go9x organization."

**If they DON'T have access:**
```
⚠️ You're not in the go9x GitHub organization yet.

To get access, please contact:
- PYV (pyv@go9x.com)
- Roger
- Alex
- Jan

Once you've been added to the organization, come back and run this setup again.

Would you like me to draft an email to request access?
```

**Stop here if no access.** They cannot proceed without being in the go9x org.

### Step 5: Add Private Marketplace in Cowork

Now for the key step - adding the private marketplace.

Explain what's happening:
```
Perfect! Now that your GitHub token is set up, we can add the private 9x skills marketplace.

This marketplace contains all our team skills:
- Attio CRM operations
- Sales automation
- Content generation
- Notion integration
- And more!

The marketplace is private, so it will use your GitHub token for access.
```

Guide them through Cowork UI:
```
1. In Cowork, click "Plugins" in the left sidebar
2. Click "Add Marketplace from GitHub"
3. Enter: go9x/skills
4. Click "Add"
```

**Important:** Cowork will use the `GITHUB_TOKEN` environment variable to authenticate with the private repo.

If they get an error about authentication or "repository not found":
- Make sure they set the token in Step 3
- Make sure they restarted Terminal after setting the token
- Try running: `source ~/.zshrc` in Terminal to reload the environment
- Then try adding the marketplace again in Cowork

Have them confirm it was added successfully: "Do you see 'go9x-skills' in your Plugins list?"

Show: "✅ Private marketplace added!"

### Step 6: Restart Cowork

For the skills to load, they need to restart:
```
The skills will be available after you restart Cowork.

Please quit Cowork completely and reopen it now.

(Cmd+Q to quit, then relaunch from Applications)
```

### Step 7: Verify Installation

After they restart Cowork, check that skills are available:

Ask them: "Do you see the 9x skills in your plugins list in Cowork?"

They should see skills like:
- attio-add-to-outreach
- attio-screen-contacts
- follow-up-draft-generator
- tutorial-generator
- notion-task
- And more!

Show celebration: "✅ Setup complete! All 9x skills are now available!"

### Step 8: Next Steps - API Credentials

Now explain the final step:
```
Almost done! The last thing is to set up your API credentials.

You'll need API keys for:
- Attio (your CRM access)
- Notion (your workspace access)

Just ask me: "Help me set up my API credentials for 9x skills"

I'll guide you through getting and saving your API keys securely.
```

**Note:** The credential setup is handled by a skill in the private marketplace. That's where sensitive credential handling happens, keeping it secure.

### Step 10: What Skills Are Available

Give them an overview of what they can now do:

```
You now have access to all 9x team skills! Here's what's available:

🏢 Attio CRM:
- Add contacts to outreach sequences
- Manage event attendees
- Screen and filter contacts
- Get/update CRM attributes

📧 Sales Automation:
- Generate follow-up emails
- Create sales offers
- Manage deal workflows
- Draft emails to inbox

📝 Content Creation:
- Generate tutorials
- Create demo workflows

📋 Notion:
- Create and manage tasks

And more in Circle, Framer, Slack, and Cowork categories!

Remember: You don't need to use slash commands. Just talk to me naturally:
- "Add sarah@example.com to outreach in Attio"
- "Generate a follow-up for the Acme deal"
- "Create a Notion task to call John tomorrow"

I'll automatically use the right skill!
```

## Error Handling

### Token Creation Issues
- Make sure they're logged into correct GitHub account
- Must select "repo" scope when creating token
- Must copy token immediately (can't be seen again)
- If lost, create a new token

### Token Not Set Properly
- Check they used correct command: `echo 'export GITHUB_TOKEN="..."' >> ~/.zshrc`
- Check they ran: `source ~/.zshrc`
- Verify with: `echo $GITHUB_TOKEN`
- If using bash instead of zsh, use `~/.bashrc` instead

### No Organization Access
- User must be in go9x GitHub organization
- Cannot proceed without access
- Create token won't work until they're in org
- Contact: PYV, Roger, Alex, or Jan to be added

### Marketplace Won't Add
- Verify token is set: `echo $GITHUB_TOKEN` in Terminal
- Verify org access: `curl -H "Authorization: token $GITHUB_TOKEN" https://api.github.com/user/orgs | grep go9x`
- Check repo URL is correct: go9x/skills
- Try restarting Terminal, then Cowork
- Make sure token has "repo" scope

### Skills Don't Appear After Restart
- Ensure they fully quit Cowork (Cmd+Q)
- Check marketplace was added: Look in Plugins list
- Verify marketplace shows as "go9x-skills"
- Try removing and re-adding the marketplace
- Check GitHub token is still set in Terminal

### "Repository Not Found" Error
- This means authentication failed or no org access
- Verify token: `echo $GITHUB_TOKEN`
- Verify org membership
- Token might have been created before being added to org (create new one)

### Private Repo Access Denied
- User needs to be member of go9x GitHub organization
- GitHub enforces this - no workaround
- Contact PYV, Roger, Alex, or Jan to be added
- After being added, may need to create fresh token

## Security & Privacy

- This public skill contains NO sensitive information
- No API keys or credentials are handled here (that's in private skills)
- GitHub enforces all access control for private repo
- Only go9x organization members can access go9x/skills
- All credential setup happens in private skills after this setup

## Communication Style

- **Warm and encouraging** - This is onboarding, make it welcoming
- **Celebrate progress** - Use ✅ and emojis for completed steps
- **Patient and clear** - Both technical and non-technical users will use this
- **Helpful with errors** - Provide clear troubleshooting, not just error messages
- **Step-by-step** - Don't overwhelm, take it one step at a time

Good example:
```
✅ GitHub authenticated!
✅ Organization access confirmed!
✅ Private marketplace added!

You're crushing it! Just one more step: restart Cowork, then we'll set up your API credentials.
```

## Additional Notes

This skill is specifically designed for the "Add Marketplace from GitHub" workflow in Cowork. It assumes:
- User has already added go9x/onboarding marketplace
- User is running Cowork on macOS OR Claude Code
- User has Terminal access for GitHub CLI commands
- Private skills repo (go9x/skills) exists and user will have access via org membership

The credential setup (/9x-configure-credentials) is intentionally separated into the private repo to keep sensitive operations out of the public marketplace.
