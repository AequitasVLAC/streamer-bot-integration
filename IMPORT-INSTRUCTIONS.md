# Streamer.bot Import Instructions for Unified Eggonomy System

This document explains how to import and use the Unified Eggonomy System with Streamer.bot.

## Understanding Streamer.bot Import/Export

Streamer.bot uses **encoded text strings** (base64/gzip compressed JSON) for importing and exporting actions and commands. These are typically shared as:
- `.sb` files
- `.txt` files with encoded strings
- Raw encoded strings in documentation

## What's Included

This repository provides **JSON template files** in the `streamerbot-imports/` directory. These are **not** encoded import strings, but rather structured templates that show you exactly what each action does.

### Why JSON Templates Instead of Encoded Strings?

1. **Transparency**: You can see exactly what code will run
2. **Customization**: Easy to modify before implementing
3. **Learning**: Understand how each component works
4. **Security**: No hidden code execution
5. **Version Control**: Clear diffs when changes are made

## How to Use These Files

You have two options:

### Option A: Manual Setup (Recommended for Learning)

Follow the step-by-step guide in `streamerbot-imports/QUICK-START.md` to manually create each action in Streamer.bot using the JSON templates as reference.

**Pros:**
- Full understanding of each component
- Easy to customize as you go
- Learn Streamer.bot interface

**Cons:**
- Takes more time
- More steps involved

### Option B: Create Your Own Export Strings

1. Set up actions manually using Option A
2. Export each action from Streamer.bot (right-click → Export)
3. Save the encoded strings for future use
4. Share them with others who trust your setup

**Pros:**
- One-click import after initial setup
- Easy to share with your community
- Quick deployment to new instances

**Cons:**
- Initial setup still required
- Encoded strings are harder to review

## Getting Started

1. **Read the Documentation**
   - Start with [Unified-Eggonomy-System.md](../Unified-Eggonomy-System.md) for full system overview
   - Review [QUICK-START.md](./QUICK-START.md) for step-by-step setup

2. **Set Up User Data**
   - Create `C:\StreamerBot\UserData\eggs.json`
   - Initialize with `{"users": {}}`

3. **Import Core Actions**
   - Start with reward actions (chat, bits, subs)
   - Add basic commands (eggs, eggpack)
   - Test before proceeding

4. **Add Games and Features**
   - Token purchase commands
   - Roll20 game
   - Roulette (optional)
   - PvP system (optional)
   - Adventure system (optional)

5. **Customize and Balance**
   - Adjust egg rewards
   - Modify token costs
   - Tune game odds
   - Set appropriate cooldowns

## File Structure

```
streamerbot-imports/
├── README.md                          # Overview (this file)
├── QUICK-START.md                     # Step-by-step setup guide
├── action-chat-egg-reward.json        # Chat message rewards
├── action-cheer-reward.json           # Bit cheer rewards
├── action-subscription-reward.json    # Subscription rewards
├── command-eggs.json                  # !eggs command
├── command-eggpack.json               # !eggpack command
├── command-buyD20.json                # !buyD20 command
├── command-buyRRT.json                # !buyRRT command
└── command-roll20.json                # !roll20 game
```

## Additional Files to Create

The following actions are described in the main documentation but not yet provided as JSON templates. You can create them following the same patterns:

### Commands
- `!top` - Leaderboard
- `!roulette` - Roulette game
- `!pvp` - PvP battles
- `!accept` - Accept PvP
- `!duel` - PvP alias
- `!adventure` - Start adventure
- `!save` - Make saving throw

### Moderator Commands
- `!giveggs` - Grant eggs
- `!takeggs` - Remove eggs
- `!resetuser` - Reset user data
- `!ecobalance` - Economy stats

### Additional Reward Actions
- Watch time / loyalty rewards
- Raid rewards

## Technical Details

### User Data Structure

All actions read/write to `eggs.json` with this structure:

```json
{
  "users": {
    "userId123": {
      "eggs": 500,
      "d20Tokens": 3,
      "rrTokens": 10,
      "adventureState": "...",
      "lastAdventure": "2025-12-31T00:00:00Z",
      "totalAdventures": 5,
      "modifiers": {
        "STR": 1, "DEX": 2, "CON": 1,
        "INT": 2, "WIS": 1, "CHA": 1
      }
    }
  }
}
```

### C# Dependencies

All C# code uses:
- `System.IO` - File operations
- `Newtonsoft.Json.Linq` - JSON parsing (included with Streamer.bot)

### Customization Points

Common modifications:
- `dataPath` - Change file location
- Token costs (100 for D20, 50 for RR)
- Egg rewards (5 for chat, varies for events)
- Game odds and payouts
- Cooldown durations

## Support and Resources

### Official Streamer.bot Resources
- [Streamer.bot Documentation](https://docs.streamer.bot)
- [Import/Export Guide](https://docs.streamer.bot/guide/import-export)
- [Streamer.bot Discord](https://discord.gg/streamerbot)

### This Repository
- [Full System Documentation](../Unified-Eggonomy-System.md)
- [Quick Start Guide](./QUICK-START.md)
- [GitHub Issues](https://github.com/AequitasVLAC/streamer-bot-integration/issues)

### Community Examples
- [welshman/Streamer.bot-Exports](https://github.com/welshman/Streamer.bot-Exports)
- [nuttylmao/Streamer.bot-Actions](https://github.com/nuttylmao/Streamer.bot-Actions)

## Creating Export Strings from JSON Templates

If you want to create actual Streamer.bot export strings from these templates:

1. Set up the action manually in Streamer.bot
2. Right-click the action → **Export**
3. Choose format (String or File)
4. Save the output
5. Share or backup the encoded string

The encoded string can then be imported with:
1. Right-click in Actions → **Import**
2. Paste the string
3. Click **Import**

## Security Note

When using import strings from others:
- Always review the source
- Check C# code before compiling
- Test in a safe environment first
- Understand what file operations occur
- Be cautious with external API calls

This repository provides readable JSON templates specifically to make code review easy.

## Contributing

Want to add more actions or improve existing ones?

1. Fork the repository
2. Add or modify JSON template files
3. Test in your Streamer.bot instance
4. Create a pull request with description
5. Include any new dependencies or requirements

## Feedback

Have questions or suggestions? Open an issue on GitHub!

---

**Ready to get started?** → Check out [QUICK-START.md](./QUICK-START.md)!
