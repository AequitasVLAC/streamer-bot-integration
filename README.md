# Streamer.bot Integration

Welcome to the **Streamer.bot Integration** repository! This repository contains comprehensive guides and configurations for integrating advanced features into your Twitch streams using Streamer.bot.

## 🥚 Unified Eggonomy System

The flagship feature of this repository is the **Unified Eggonomy System** - a complete, engaging, egg-based currency and game loop for Twitch communities.

### Features
- 🥚 Egg-based economy with multiple earning methods
- 🎲 D20 Token system for D&D-style adventures
- 🎰 RRToken system for competitive games
- 🎮 Multiple game modes (Roll20, Roulette, PvP)
- 📖 Personal Adventure system with persistent narratives
- 🏆 Leaderboards and community engagement tools
- ⚖️ Balanced economy with egg sinks and periodic events

### Documentation

For complete implementation instructions, configuration details, and command reference, see:

**[📚 Unified Eggonomy System Documentation](./Unified-Eggonomy-System.md)**

This comprehensive guide includes:
- Core economy mechanics and egg acquisition methods
- Token system (D20 Tokens & RRTokens)
- Game configurations (Roll20, Roulette, PvP battles)
- Personal Adventure system with D&D mechanics
- Complete Streamer.bot setup instructions
- C# code examples and templates
- Balance guidelines and economy management
- Command reference and troubleshooting

### Quick Start

#### Option 1: Import Ready-to-Use Actions (Fastest)

1. Install Streamer.bot and connect to your Twitch channel
2. Check out the **[Import Instructions](./IMPORT-INSTRUCTIONS.md)** for importing pre-configured actions
3. Follow the **[Quick Start Guide](./streamerbot-imports/QUICK-START.md)** for step-by-step setup
4. Import actions from the `streamerbot-imports/` directory
5. Test and customize to fit your community

#### Option 2: Manual Configuration (Most Flexible)

1. Install Streamer.bot and connect to your Twitch channel
2. Set up user data storage (JSON file)
3. Follow the [Streamer.bot Configuration](./Unified-Eggonomy-System.md#streamerbot-configuration) section
4. Configure Twitch event actions for egg rewards
5. Set up chat commands for user interaction
6. Test and adjust economy balance to fit your community

### Importable Actions

The `streamerbot-imports/` directory contains ready-to-use JSON templates for:
- 💬 Chat egg rewards
- 🎁 Bit and subscription rewards
- 💰 Commands: `!eggs`, `!eggpack`, `!buyD20`, `!buyRRT`
- 🎲 Games: `!roll20` and more

See **[IMPORT-INSTRUCTIONS.md](./IMPORT-INSTRUCTIONS.md)** for details on importing these into Streamer.bot.

### Support

For questions, issues, or suggestions, please open an issue in this repository.

---

**Version**: 1.0  
**Last Updated**: 2025-12-31
