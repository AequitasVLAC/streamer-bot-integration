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
4. `action-raid-reward.json` - Raid rewards

### Phase 2: Basic Commands
1. `command-eggs.json` - Check balance
2. `command-eggpack.json` - View inventory
3. `command-top.json` - Leaderboard

### Phase 3: Token System
1. `command-buyD20.json` - Buy D20 tokens
2. `command-buyRRT.json` - Buy RRTokens

### Phase 4: Games
1. `command-roll20.json` - Roll20 game
2. `command-roulette.json` - Roulette game

### Phase 5: PvP System (Optional)
1. `command-pvp.json` - PvP challenges (!pvp and !duel)
2. `command-accept.json` - Accept challenges

### Phase 6: Adventure System (Optional)
1. Copy `adventure-stories.json` to `C:\StreamerBot\UserData\adventure-stories.json`
2. `command-adventure.json` - Start adventures
3. `command-save.json` - Make saving throws

### Phase 7: Moderator Tools (Optional)
1. `command-giveggs.json` - Grant eggs
2. `command-takeggs.json` - Remove eggs
3. `command-resetuser.json` - Reset users
4. `command-ecobalance.json` - Economy stats

### Phase 8: Test Everything
- Have a test account chat to earn eggs
- Test commands to verify they work
- Check that `eggs.json` is being updated

## Step 4: Testing Checklist

- [ ] Chat in stream → Check if eggs.json updates with +5 eggs
- [ ] Run `!eggs` → Should display egg count
- [ ] Run `!eggpack` → Should show full inventory
- [ ] Run `!top` → Should display leaderboard
- [ ] Run `!buyD20 1` → Should purchase token if you have 100+ eggs
- [ ] Run `!buyRRT 1` → Should purchase token if you have 50+ eggs
- [ ] Run `!roll20 50` → Should play the game if you have 50+ eggs
- [ ] Run `!roulette 100` → Should play roulette if you have 100+ eggs
- [ ] Run `!pvp @testuser 5` → Should challenge user (if they have 5+ RRTokens)
- [ ] Run `!accept` → Should accept pending PvP challenge
- [ ] Run `!adventure` → Should start adventure (if you have 1+ D20 Token)
- [ ] Run `!save` → Should complete active adventure
- [ ] Check `eggs.json` file → Verify data is being saved
- [ ] Check `adventure-stories.json` → Verify file exists in UserData folder

### Moderator Commands Testing (Requires Mod/Broadcaster)
- [ ] Run `!giveggs @user 100` → Should grant eggs
- [ ] Run `!takeggs @user 50` → Should remove eggs
- [ ] Run `!resetuser @user` → Should reset user data
- [ ] Run `!ecobalance` → Should display economy statistics

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
- For adventures: Verify `adventure-stories.json` is in `C:\StreamerBot\UserData\`

### Commands not responding
- Check triggers are properly configured
- Verify command name matches (case doesn't matter)
- Check permissions allow Everyone
- Look at Streamer.bot logs for errors

### Eggs not saving
- Verify JSON file has write permissions
- Check C# code compiles without errors
- Look at Streamer.bot logs for errors
- Ensure file path is correct and accessible

### Cooldowns not working
- Ensure cooldown is enabled in action settings
- Check cooldown type (User vs Global)
- Verify duration is set correctly

### PvP challenges not working
- Both players must have sufficient RRTokens
- Challenges expire after 60 seconds
- Check that both users have valid egg data

### Adventures not loading
- Verify `adventure-stories.json` exists in `C:\StreamerBot\UserData\`
- Check JSON file is valid (no syntax errors)
- Ensure at least one adventure exists in the file
- Adventures have a 24-hour cooldown per user
- Active adventures expire after 10 minutes

### Leaderboard showing user IDs instead of names
- This is normal if Streamer.bot can't lookup the username
- The system will show usernames when available
- User IDs are used as fallback

### C# Compilation Errors
- Ensure you copied the entire code block
- Check for missing using statements
- Verify Newtonsoft.Json.Linq is available (comes with Streamer.bot)
- Check Streamer.bot logs for specific error messages

## Advanced Setup

### Customizing the Economy

After basic setup works, customize:

1. **Egg Costs**: Modify token costs in buy commands (default: D20=100, RRT=50)
2. **Rewards**: Adjust egg amounts in reward actions
3. **Cooldowns**: Change command cooldown times
4. **File Path**: Update `dataPath` in all C# code if needed
5. **Game Odds**: Modify Roll20 and Roulette payout multipliers
6. **Adventure Stories**: Add more adventures to `adventure-stories.json`

### Adding More Adventure Stories

To expand the adventure system:
1. Open `adventure-stories.json`
2. Add new adventure objects following the same structure
3. Include unique `id`, `title`, `description`, `challenge`, `dc`, outcomes, and rewards
4. Link adventures together using `nextAdventures` array
5. Save and restart Streamer.bot to load new stories

## Getting Help

- Review the [full documentation](../Unified-Eggonomy-System.md)
- Check [Streamer.bot documentation](https://docs.streamer.bot)
- Visit Streamer.bot Discord for community support

## Quick Reference

| File | Command | Cost | Cooldown |
|------|---------|------|----------|
| command-eggs.json | !eggs | Free | 5s |
| command-eggpack.json | !eggpack | Free | 10s |
| command-top.json | !top | Free | 30s global |
| command-buyD20.json | !buyD20 [amount] | 100 eggs/token | 10s |
| command-buyRRT.json | !buyRRT [amount] | 50 eggs/token | 10s |
| command-roll20.json | !roll20 [wager] | 10-500 eggs | 30s |
| command-roulette.json | !roulette [wager] | 25-1000 eggs | 45s |
| command-pvp.json | !pvp @user [wager] | 1-20 RRTokens | 120s |
| command-pvp.json | !duel @user [wager] | 1-20 RRTokens | 120s |
| command-accept.json | !accept | Free | None |
| command-adventure.json | !adventure | 1 D20 Token | 24h |
| command-save.json | !save | Free | None |

### Moderator Commands
| File | Command | Description |
|------|---------|-------------|
| command-giveggs.json | !giveggs @user [amount] | Grant eggs to user |
| command-takeggs.json | !takeggs @user [amount] | Remove eggs from user |
| command-resetuser.json | !resetuser @user | Reset user's data |
| command-ecobalance.json | !ecobalance | View economy stats |

---

**Next Steps**: Once the basics work, explore the full documentation to implement roulette, PvP, and the adventure system!
