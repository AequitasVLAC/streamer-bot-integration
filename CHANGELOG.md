# Changelog

All notable changes to the Unified Eggonomy System will be documented in this file.

## [1.1.0] - 2025-12-31

### Added

#### Complete Command Set
- **!top** - Display leaderboard of top 10 egg holders
- **!roulette** - Weighted random gambling game (25-1000 eggs)
- **!pvp / !duel** - Challenge players to D&D-style PvP battles (RRTokens)
- **!accept** - Accept pending PvP challenges
- **!adventure** - Start personalized D&D-style adventures (24h cooldown)
- **!save** - Make saving throws to resolve adventure challenges

#### Moderator Commands
- **!giveggs** - Grant eggs to users (moderator only)
- **!takeggs** - Remove eggs from users (moderator only)
- **!resetuser** - Reset user's economy data (moderator only)
- **!ecobalance** - View comprehensive economy statistics (moderator only)

#### New Reward Actions
- **Raid Rewards** - Award 10 eggs per raider to raiding streamer

#### Adventure System
- 8 unique adventure story templates with branching narratives
- D&D 5e-style saving throw mechanics (STR, DEX, CON, INT, WIS, CHA)
- Difficulty Classes (DC) ranging from 10-22
- Progressive modifier system (+1 per 10 adventures completed)
- Critical success (natural 20) and critical failure (natural 1) outcomes
- Adventure state persistence and story continuity
- 24-hour cooldown per user
- 10-minute expiration for active adventures

#### PvP System
- Challenge system with 60-second acceptance window
- D&D-style combat simulation with initiative rolls
- 3 rounds of combat with attack vs defense rolls
- Narrative combat descriptions with random weapons and actions
- Token wagering (1-20 RRTokens)
- Winner rewards: opponent's tokens + 50 bonus eggs
- Loser consolation: 10 eggs
- Draw scenario: both keep tokens, receive 25 eggs each
- Automatic challenge expiration and cleanup

#### Documentation
- Comprehensive **TESTING-GUIDE.md** with detailed test scenarios
- Updated **IMPORT-INSTRUCTIONS.md** with complete file structure
- Expanded **QUICK-START.md** with all commands and troubleshooting
- Added adventure system setup instructions
- Included moderator command documentation

### Changed
- Updated file structure documentation to reflect 20 total JSON files
- Enhanced QUICK-START.md with expanded testing checklist
- Improved troubleshooting section with PvP and adventure-specific issues
- Updated quick reference tables with all commands

### Fixed
- Improved error handling in all commands
- Added missing null checks in user data access
- Enhanced validation for command parameters
- Better handling of edge cases (0 eggs, missing users, etc.)

## [1.0.0] - 2025-12-30

### Added - Initial Release

#### Core Economy
- **!eggs** - Check egg balance (5s cooldown)
- **!eggpack** - View complete inventory (eggs and tokens)
- **!buyD20** - Purchase D20 Tokens for adventures (100 eggs each)
- **!buyRRT** - Purchase RRTokens for games (50 eggs each)

#### Games
- **!roll20** - D20 gambling game with varied outcomes (10-500 eggs)

#### Reward Actions
- **Chat Message Rewards** - 5 eggs per message (60s cooldown)
- **Cheer Rewards** - 1 egg per bit
- **Subscription Rewards** - 500/1000/2000 eggs for T1/T2/T3

#### Documentation
- Complete **Unified-Eggonomy-System.md** specification
- **README.md** with overview and quick start
- **IMPORT-INSTRUCTIONS.md** for Streamer.bot setup
- **QUICK-START.md** for step-by-step configuration

#### File Structure
- JSON template format for transparency and customization
- Organized action groups (Rewards, Commands, Games)
- User data persistence system using JSON files

---

## File Count Summary

### Version 1.1.0
- **20 JSON files total**
  - 4 Reward Actions
  - 3 Basic Commands  
  - 2 Token Commands
  - 2 Game Commands
  - 2 PvP Commands
  - 3 Adventure Commands (including story template)
  - 4 Moderator Commands

### Version 1.0.0
- **8 JSON files**

---

## Upgrade Path

### From 1.0.0 to 1.1.0

1. **Download New Files:**
   - All new command JSON files from `streamerbot-imports/`
   - `adventure-stories.json` template

2. **Copy Adventure Stories:**
   ```
   Copy adventure-stories.json to C:\StreamerBot\UserData\adventure-stories.json
   ```

3. **Import New Actions:**
   - Follow QUICK-START.md for each new command
   - Test each command individually before proceeding

4. **Update Data Structure:**
   - Existing `eggs.json` is compatible
   - New fields added automatically as needed:
     - `pvpChallenges` - For PvP challenge state
     - `activeAdventures` - For adventure state
     - Per-user: `adventureState`, `lastAdventure`, `totalAdventures`

5. **No Breaking Changes:**
   - All existing commands continue to work
   - User data is preserved and extended
   - New commands are independent additions

---

## Known Issues

### Version 1.1.0
- Leaderboard may show user IDs if username lookup fails (fallback behavior)
- PvP challenges don't persist across Streamer.bot restarts
- Adventure stories must be manually updated (no auto-reload)

### Version 1.0.0
- Limited command set (only basics implemented)

---

## Future Roadmap

### Planned for Version 1.2.0
- Boss battle system (community PvE events)
- Guild/team system for cooperative play
- Achievement system with unlockable titles
- Egg shop for cosmetic items
- Enhanced adventure editor tool

### Under Consideration
- Discord bot integration
- Web dashboard for leaderboards
- Mobile app for inventory checking
- Twitch extension for visual inventory
- Trading system between users
- Seasonal events and limited-time adventures

---

## Credits

**Created by:** AequitasVLAC
**License:** MIT
**Repository:** https://github.com/AequitasVLAC/streamer-bot-integration

Special thanks to:
- Streamer.bot community for feedback and testing
- D&D 5e for inspiration on adventure mechanics
- All contributors and testers

---

**For detailed information about each command, see:**
- [Unified-Eggonomy-System.md](./Unified-Eggonomy-System.md) - Complete system specification
- [TESTING-GUIDE.md](./TESTING-GUIDE.md) - Comprehensive testing scenarios
- [QUICK-START.md](./streamerbot-imports/QUICK-START.md) - Setup instructions
