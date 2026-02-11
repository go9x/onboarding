# 9x Team Setup Skill

## Description
Setup skill for 9x team members using Cowork. Guides users through connecting GitHub and installing private 9x skills from the go9x/skills marketplace.

## Usage
After adding the `go9x/onboarding` marketplace in Cowork, ask Claude to help set up 9x skills.

## What This Skill Does

Guides you through:
1. Connecting GitHub in Cowork (if not already connected)
2. Manually adding the private go9x/skills marketplace to your settings file
3. Restarting Cowork to load the skills
4. Next steps for API credential setup (handled by private skills)

## Instructions for Claude

When a user invokes this skill, guide them interactively through these steps. This is a **Cowork-only workflow** - no terminal commands allowed.

### Step 1: Welcome & Context

Greet them warmly:
```
Welcome to 9x! 🎉

You've successfully added the public onboarding marketplace in Cowork. Now let's get you access to the private 9x team skills.

This will take about 2-3 minutes and involves:
✓ Connecting your GitHub account (if not already)
✓ Manually editing one settings file
✓ Restarting Cowork

Ready to get started?
```

### Step 2: Check GitHub Connection

First, check if they have GitHub connected in Cowork.

Ask them: "Is GitHub connected in your Cowork? You can check by clicking your **profile icon (bottom left) → Settings → Integrations**. Do you see GitHub listed as connected?"

**If GitHub is NOT connected:**

Guide them to connect:
```
Let's connect your GitHub account to Cowork. This will give you access to private 9x repositories.

Follow these steps in Cowork:
1. Click your **profile icon** (bottom left corner)
2. Select **Settings**
3. Click **Integrations** in the left sidebar
4. Find **GitHub** and click **Connect**
5. Your browser will open GitHub's authorization page
6. **Important:** When prompted, make sure to grant access to the **go9x** organization
7. After authorizing, return to Cowork

Let me know when you've completed this!
```

**Wait for them to complete GitHub connection.**

**If GitHub IS connected:**

Verify they have access to the go9x organization:
```
Perfect! GitHub is connected.

Quick check: When you connected GitHub, did you grant Cowork access to the **go9x** organization?

You can verify this at: https://github.com/settings/installations
Look for "Claude" or "Anthropic" in your installed apps and check that go9x organization is selected.
```

**If they don't have go9x organization access:**
```
You'll need to be added to the go9x GitHub organization first. Please contact:
- PYV (pyv@go9x.com)
- Roger
- Alex
- Jan

Once you're added to the organization, you may need to reconnect GitHub in Cowork (Settings → Integrations → GitHub → Disconnect, then reconnect).
```

Show celebration when confirmed: "✅ GitHub connected with go9x organization access!"

### Step 3: Manually Add Private Marketplace to Settings File

Now guide them to manually edit their Cowork settings file:

```
Perfect! Now we'll add the private 9x skills marketplace by editing one file.

Since you already added the public go9x/onboarding marketplace, you have a settings file. We just need to add the private marketplace to it!

Since you're connected to GitHub with go9x organization access, Cowork will automatically authenticate when loading the private repository.
```

**Guide them step-by-step through Finder and TextEdit:**

**Step 3.1: Open Finder and Navigate to Settings File**

```
First, let's open the folder containing your Cowork settings:

1. Click on **Finder** (the blue smiley face icon in your Dock)
2. Press **Cmd+Shift+G** (this opens "Go to Folder")
3. Type exactly: ~/.claude
4. Press **Enter**

You should now see a folder with a file called **settings.json**
```

**Step 3.2: Open the File in TextEdit**

```
Now let's open the file:

1. Find the file named **settings.json**
2. **Right-click** on it (or Control+Click)
3. Select **"Open With"**
4. Choose **"TextEdit"**
   (You can also use VS Code, Cursor, or any text editor you prefer)

The file will open and show JSON text.
```

**Step 3.3: Show Them What the File Currently Looks Like**

```
Your settings.json file currently looks something like this:

{
  "extraKnownMarketplaces": {
    "go9x-onboarding": {
      "source": {
        "source": "github",
        "repo": "go9x/onboarding"
      }
    }
  },
  "enabledPlugins": {
    "9x-onboarding@go9x-onboarding": true
  }
}

Now we need to add the private marketplace to this file.
```

**Step 3.4: Guide the Exact Edits**

```
Here's what to do:

1. Find the line with the closing brace after "go9x/onboarding" }
2. Add a COMMA after that closing brace
3. Add the private marketplace entry

Your file should end up looking like this:

{
  "extraKnownMarketplaces": {
    "go9x-onboarding": {
      "source": {
        "source": "github",
        "repo": "go9x/onboarding"
      }
    },
    "go9x-skills": {
      "source": {
        "source": "github",
        "repo": "go9x/skills"
      }
    }
  },
  "enabledPlugins": {
    "9x-onboarding@go9x-onboarding": true,
    "go9x-skills@go9x-skills": true
  }
}

Key changes you made:
✓ Added a comma after the go9x-onboarding closing brace
✓ Added the entire "go9x-skills" block
✓ Added a comma after "9x-onboarding@go9x-onboarding": true
✓ Added the "go9x-skills@go9x-skills": true line
```

**Step 3.5: Save the File**

```
Now save your changes:

1. Press **Cmd+S** to save
2. Close TextEdit

Great! Your settings file is now updated.
```

**Step 3.6: Verify (Optional)**

If they want to double-check, tell them:
```
Want to make sure everything looks good?

You can paste your entire settings.json file here and I'll verify it's correct. Just select all the text in TextEdit (Cmd+A), copy it (Cmd+C), and paste it in this chat.
```

Show celebration: "✅ Settings file updated! You've added the private marketplace."

### Step 4: Restart Cowork

For the skills to load, they need to completely restart Cowork:

```
Excellent! The private marketplace has been added to your configuration.

Now we need to restart Cowork so it can load the private skills:

1. **Quit Cowork completely:** Press **Cmd+Q** (or click Cowork → Quit Cowork)
2. Wait a few seconds
3. **Reopen Cowork** from your Applications folder or Dock

When Cowork restarts, it will automatically:
- Read your updated settings file
- Use your GitHub connection to access the private go9x/skills repository
- Load all the 9x team skills

Let me know when Cowork has restarted!
```

### Step 5: Verify Installation

After they restart Cowork, verify the skills loaded successfully:

```
Perfect! Now let's check that everything worked.

In Cowork, look at the **Plugins sidebar** (left side).

Do you see **go9x-skills** listed in your marketplaces?

If you do, that means the private 9x skills have been loaded successfully!
```

**If they see the skills:**

Show celebration:
```
✅ Setup complete! All 9x team skills are now available in Cowork!

You can now use any of these skills just by talking to me naturally. No need to memorize commands!
```

**If they don't see the skills:**

Troubleshoot step-by-step:
```
Let's troubleshoot together:

1. **Check the Plugins list:** In Cowork → Plugins sidebar, do you see "go9x-skills" marketplace listed? (Even if the skills themselves aren't showing)

2. **Check GitHub is still connected:** Go to Settings → Integrations. Is GitHub showing as "Connected"?

3. **Verify your settings file:** Let's make sure the file was saved correctly. Can you:
   - Open Finder, press Cmd+Shift+G, type ~/.claude
   - Open settings.json
   - Copy all the text and paste it here so I can check?

4. **Check organization access:** Go to https://github.com/settings/installations
   - Find "Claude" or "Anthropic"
   - Click "Configure"
   - Make sure **go9x** organization is selected

5. **Try a fresh restart:** Quit Cowork completely (Cmd+Q), wait 10 seconds, reopen

Let's go through these one by one to figure out what's happening!
```

### Step 6: Next Steps - API Credentials

Once skills are loaded successfully, explain the final step:

```
🎉 Amazing! You now have access to all 9x team skills in Cowork!

There's one more thing to set up: your **API credentials**.

The private marketplace includes a credential setup skill. Just ask me:

"Help me configure my 9x credentials"

This will guide you through setting up the necessary API access for the 9x skills.

Want to do that now, or would you like to explore the available skills first?
```

**Note for Claude:** The credential setup skill is in the private go9x/skills marketplace, not in this public onboarding marketplace. That's where all sensitive operations happen.

### Step 7: Next Steps

```
You're all set! The 9x skills are now available in Cowork.

To see what skills are available, you can:
- Browse the Plugins sidebar in Cowork
- Just start talking to me naturally about what you want to do
- Ask me "What 9x skills are available?"

The skills will work automatically based on what you ask for - no need to memorize commands!

Once you configure your credentials, you'll be able to use all the 9x team tools directly through Cowork.
```

## Error Handling

### GitHub Not Connected in Cowork
- User needs to connect GitHub: Cowork → Settings → Integrations → GitHub → Connect
- Must authorize and grant access to **go9x** organization during OAuth flow
- Check authorization at: https://github.com/settings/installations

### No Access to go9x Organization
- User must be a member of go9x GitHub organization
- Cannot access private skills without membership
- Contact to be added: PYV (pyv@go9x.com), Roger, Alex, or Jan
- After being added, may need to disconnect and reconnect GitHub in Cowork

### Settings File Editing Issues
- **File doesn't open:** Try different text editor (VS Code, Sublime, etc.)
- **Can't find .claude folder:** The folder is hidden. Use Finder → Cmd+Shift+G → ~/.claude
- **JSON syntax error:** Check for missing commas, unmatched brackets/braces, or extra commas
- **File won't save:** Check file isn't open in another program

### Skills Don't Appear After Restart
- Check **Plugins sidebar** in Cowork - is "go9x-skills" listed?
- Verify **GitHub still connected**: Settings → Integrations → GitHub status
- Check **settings.json was saved**: Open file again and verify changes are there
- Verify **organization access**: https://github.com/settings/installations → Configure Claude app → Ensure go9x is selected
- Try **complete restart**: Cmd+Q to quit, wait 10 seconds, reopen from Applications

### "Repository Not Found" or Access Errors
- GitHub connection may not include go9x organization
- Go to: https://github.com/settings/installations
- Find "Claude" or "Anthropic"
- Click **"Configure"**
- Under "Repository access" or "Organization access", make sure **go9x** is selected
- If not selected, add it
- Disconnect and reconnect GitHub in Cowork to refresh

### Marketplace Added But Skills Won't Load
- Confirm they're actually in go9x organization: https://github.com/orgs/go9x/people
- Try visiting https://github.com/go9x/skills in their browser - can they see it?
- If they get "404 Not Found", they don't have access yet
- Full restart: Quit Cowork (Cmd+Q), wait 10 seconds, reopen

### Invalid JSON in Settings File
Common mistakes:
- Missing comma between marketplace entries
- Extra comma after last item
- Unmatched quotes or brackets
- Using single quotes instead of double quotes

If the file is broken, they can paste it here and you'll help fix it.

## Security & Privacy

- This skill only modifies the local Cowork settings file (`~/.claude/settings.json`)
- No API keys or credentials are handled here (that's in the private skills)
- Authentication to private repository is handled automatically by Cowork's GitHub integration
- Only go9x organization members with proper GitHub access can load the private skills
- GitHub enforces all access control - there's no way to bypass it

## Communication Style

- **Warm and encouraging** - This is onboarding, make it welcoming and celebratory
- **Clear and visual** - Use ✅ emojis for completed steps, show examples
- **Patient** - Repeat instructions if needed, break down complex steps
- **Supportive with errors** - Don't just say "it failed", help them fix it step by step
- **Check understanding** - After each major step, ask "How did that go?" or "Are you seeing what I described?"
- **Celebrate progress** - Every completed step deserves acknowledgment

Good example flow:
```
✅ GitHub connected to Cowork!
✅ Settings file edited successfully!
✅ Cowork restarted!
✅ Skills loaded!

You're doing great! Let's do a quick test - try asking me to "add a contact to Attio" and see if it recognizes the skill.
```

Bad example (too terse, no guidance):
```
Done. Restart Cowork. Check if it works.
```

## Additional Notes

**This skill is specifically designed for:**
- **Cowork** (Claude Desktop app) on macOS
- **Manual file editing** workflow (no terminal commands)
- **GitHub-based authentication** (using Cowork's built-in GitHub integration)
- **Non-technical users** who are comfortable with Finder and TextEdit

**Not suitable for:**
- Users who don't have Cowork (Claude Desktop)
- Windows or Linux users (different file paths and workflows)
- Users without GitHub access
- Claude.ai web interface (different setup entirely)

**The credential setup** (`/9x-configure-credentials`) is intentionally in the private marketplace to keep all sensitive operations (API keys, tokens) separate from this public onboarding process.

## Key Benefits of This Approach

✅ **Zero terminal commands** - Everything done in Cowork UI and Finder/TextEdit
✅ **No GITHUB_TOKEN needed** - Cowork handles authentication automatically
✅ **No GitHub CLI required** - Just browser-based GitHub OAuth
✅ **No command-line tools** - Completely GUI-based workflow
✅ **Simple for non-technical users** - Uses familiar macOS tools
✅ **Secure** - GitHub enforces all access control

The private marketplace is accessed using the same GitHub permissions that Cowork already has through the user's connected GitHub account. Once their GitHub account is in the go9x organization and connected to Cowork, everything works automatically.
