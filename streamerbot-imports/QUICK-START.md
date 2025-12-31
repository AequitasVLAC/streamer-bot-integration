# Quick Start Guide - Importing Eggonomy System into Streamer.bot

This guide will walk you through setting up the Unified Eggonomy System in Streamer.bot using the provided JSON action templates.

## Prerequisites

1. **Streamer.bot** v0.2.0 or higher installed
2. **Twitch account** connected to Streamer.bot
3. **Windows** operating system (for file paths)
4. **Basic familiarity** with Streamer.bot interface

## Step 1: Create User Data File

1. Create the directory: `C:\StreamerBot\UserData\`
2. Create a new file: `eggs.json`
3. Add this initial content:
```json
{
  "users": {}
}
```

**Note**: You can change this path, but you'll need to update it in all C# code files.

## Step 2: Import Actions into Streamer.bot

Since Streamer.bot doesn't directly import JSON files, you'll need to manually create each action:

### For Each JSON File:

1. Open Streamer.bot
2. Go to the **Actions** tab
3. Right-click in the actions list → **Add Action**
4. Configure the action using the JSON file as reference:
   - **Name**: Copy from `name` field
   - **Group**: Copy from `group` field
   - **Enabled**: Check the box
   
### Adding Triggers

For **Commands** (e.g., `command-eggs.json`):
1. In the action, click **Triggers** tab
2. Click **Add** → **Command**
3. Enter the command (e.g., `!eggs`)
4. Set **Case Sensitive**: No

For **Events** (e.g., `action-chat-egg-reward.json`):
1. Click **Triggers** tab
2. Click **Add** → **Event**
3. Select the appropriate Twitch event (e.g., "Chat Message")

### Adding C# Code Sub-Action

1. In the action, go to **Sub-Actions** tab
2. Click **Add Action** → **Code** → **Execute C# Code**
3. Copy the entire `code` field from the JSON file
4. Paste it into the C# code editor
5. Click **Compile** to verify no errors
6. Click **Save**

### Setting Cooldowns

1. In the action settings, find **Cooldown** section
2. Enable cooldown if specified in JSON
3. Set type (User/Global) and duration in seconds

### Setting Permissions

1. In **Permissions** section
2. Check appropriate boxes (Everyone, Subscriber, VIP, Moderator)

## Step 3: Import Order

We recommend importing in this order:

### Phase 1: Core Rewards (Foundation)
1. `action-chat-egg-reward.json` - Chat message rewards
2. `action-cheer-reward.json` - Bit rewards
3. `action-subscription-reward.json` - Subscription rewards

### Phase 2: Basic Commands
1. `command-eggs.json` - Check balance
2. `command-eggpack.json` - View inventory

### Phase 3: Token System
1. `command-buyD20.json` - Buy D20 tokens
2. `command-buyRRT.json` - Buy RRTokens

### Phase 4: Games
1. `command-roll20.json` - Roll20 game

### Phase 5: Test Everything
- Have a test account chat to earn eggs
- Test commands to verify they work
- Check that `eggs.json` is being updated

## Step 4: Testing Checklist

- [ ] Chat in stream → Check if eggs.json updates with +5 eggs
- [ ] Run `!eggs` → Should display egg count
- [ ] Run `!eggpack` → Should show full inventory
- [ ] Run `!buyD20 1` → Should purchase token if you have 100+ eggs
- [ ] Run `!roll20 50` → Should play the game if you have 50+ eggs
- [ ] Check `eggs.json` file → Verify data is being saved

## Step 5: Customize

After basic setup works, customize:

1. **Egg Costs**: Modify token costs in buy commands
2. **Rewards**: Adjust egg amounts in reward actions
3. **Cooldowns**: Change command cooldown times
4. **File Path**: Update `dataPath` in all C# code if needed

## Troubleshooting

### "File not found" error
- Verify `C:\StreamerBot\UserData\eggs.json` exists
- Check file path in C# code matches your actual path

### Commands not responding
- Check triggers are properly configured
- Verify command name matches (case doesn't matter)
- Check permissions allow Everyone

### Eggs not saving
- Verify JSON file has write permissions
- Check C# code compiles without errors
- Look at Streamer.bot logs for errors

### Cooldowns not working
- Ensure cooldown is enabled in action settings
- Check cooldown type (User vs Global)
- Verify duration is set correctly

## Advanced Setup

### Adding More Commands

Want to add the remaining commands? Follow the same pattern:

- `command-roulette.json` - Roulette game
- `command-pvp.json` - PvP battles
- `command-adventure.json` - Adventure system
- Moderator commands (`command-giveggs.json`, etc.)

### Creating Export Strings

Once you've set up actions manually:

1. Right-click the action in Streamer.bot
2. Select **Export**
3. Copy the generated string
4. Save to a `.sb` or `.txt` file
5. Share with others!

## Getting Help

- Review the [full documentation](../Unified-Eggonomy-System.md)
- Check [Streamer.bot documentation](https://docs.streamer.bot)
- Visit Streamer.bot Discord for community support

## Quick Reference

| File | Command | Cost | Cooldown |
|------|---------|------|----------|
| command-eggs.json | !eggs | Free | 5s |
| command-eggpack.json | !eggpack | Free | 10s |
| command-buyD20.json | !buyD20 [amount] | 100 eggs/token | 10s |
| command-buyRRT.json | !buyRRT [amount] | 50 eggs/token | 10s |
| command-roll20.json | !roll20 [wager] | 10-500 eggs | 30s |

---

**Next Steps**: Once the basics work, explore the full documentation to implement roulette, PvP, and the adventure system!
