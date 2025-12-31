# Streamer.bot Import Files for Unified Eggonomy System

This directory contains importable Streamer.bot action and command configurations for the Unified Eggonomy System.

## How to Import

### Method 1: Manual Setup (Recommended)
Since these are JSON templates, you'll need to manually create the actions in Streamer.bot using the configurations provided:

1. Open Streamer.bot
2. Navigate to the **Actions** tab
3. Right-click and select **Add Action**
4. Configure the action using the details from each JSON file
5. Add sub-actions as specified in the configuration

### Method 2: Create Import Strings
If you want to create actual import strings:

1. Set up the actions manually in Streamer.bot (using the JSON templates)
2. Right-click the action and select **Export**
3. Copy the generated encoded string
4. Save it to a `.sb` or `.txt` file for sharing

## Available Actions

### Core Economy Actions

1. **`action-chat-egg-reward.json`** - Awards eggs for chat messages
2. **`action-watch-time-reward.json`** - Awards eggs for watch time (loyalty)
3. **`action-cheer-reward.json`** - Awards eggs for cheering bits
4. **`action-subscription-reward.json`** - Awards eggs for subscriptions
5. **`action-raid-reward.json`** - Awards eggs for raids

### Command Actions

1. **`command-eggs.json`** - Check egg balance (!eggs)
2. **`command-eggpack.json`** - View full inventory (!eggpack)
3. **`command-top.json`** - View leaderboard (!top)
4. **`command-buyD20.json`** - Purchase D20 Tokens (!buyD20)
5. **`command-buyRRT.json`** - Purchase RRTokens (!buyRRT)
6. **`command-roll20.json`** - Play Roll20 game (!roll20)
7. **`command-roulette.json`** - Play Roulette (!roulette)
8. **`command-pvp.json`** - Challenge to PvP battle (!pvp)
9. **`command-accept.json`** - Accept PvP challenge (!accept)
10. **`command-adventure.json`** - Start/continue adventure (!adventure)
11. **`command-save.json`** - Make saving throw (!save)

### Moderator Commands

1. **`command-giveggs.json`** - Grant eggs to user (!giveggs)
2. **`command-takeggs.json`** - Remove eggs from user (!takeggs)
3. **`command-resetuser.json`** - Reset user data (!resetuser)
4. **`command-ecobalance.json`** - Display economy stats (!ecobalance)

## Setup Requirements

### Prerequisites
1. **Streamer.bot** installed and connected to Twitch
2. **User Data Storage**: Set up JSON file for user data at `C:\StreamerBot\UserData\eggs.json`
3. **C# Methods**: Some actions require custom C# code (provided in each JSON file)

### User Data Structure

Create a file at `C:\StreamerBot\UserData\eggs.json` with this initial structure:

```json
{
  "users": {}
}
```

User entries will be automatically created when users interact with the system.

## Configuration Notes

- **Cooldowns**: Adjust cooldown times in each command based on your preferences
- **Costs**: Modify egg costs and token prices in the JSON configurations
- **Permissions**: Set appropriate permission levels for each command
- **File Paths**: Update the `dataPath` variable in C# code to match your system

## Testing

After importing:

1. Test each command individually
2. Verify user data is being saved correctly
3. Check that cooldowns work as expected
4. Validate game logic and outcomes

## Support

For detailed documentation on the entire Eggonomy System, see:
- [Unified Eggonomy System Documentation](../Unified-Eggonomy-System.md)

For Streamer.bot import/export documentation:
- [Official Streamer.bot Import/Export Guide](https://docs.streamer.bot/guide/import-export)
