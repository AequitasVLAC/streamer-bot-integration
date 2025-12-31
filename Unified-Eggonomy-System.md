# Unified Eggonomy System for Streamer.bot

## Table of Contents
1. [Overview](#overview)
2. [Core Economy](#core-economy)
3. [Games (Spending Eggs)](#games-spending-eggs)
4. [PvP System](#pvp-system)
5. [Personal Adventure System](#personal-adventure-system)
6. [Backend Economy Management](#backend-economy-management)
7. [Streamer.bot Configuration](#streamerbot-configuration)
8. [Command Reference](#command-reference)
9. [Balance Guidelines](#balance-guidelines)

---

## Overview

The **Unified Eggonomy System** is a fun, engaging, and interactive egg-based currency and game loop designed for Twitch stream communities. This system uses **eggs** as the primary currency, which viewers can earn from various Twitch activities and spend on tokens for games, PvP battles, and personalized D&D-style adventures.

### Key Features
- 🥚 **Eggs**: Primary currency earned from watching, chatting, cheering, subscriptions, and raids
- 🎲 **D20 Tokens**: Used for Personal Adventure system (D&D-style gameplay)
- 🎰 **RRTokens** (Roulette Tokens): Used for Roulette games and PvP battles
- 🎮 **Multiple Game Modes**: Roll20, Roulette, PvP, and Personal Adventures
- 📊 **Balanced Economy**: Egg sinks and reward mechanisms to prevent hoarding
- 🏆 **Community Engagement**: Leaderboards, competitive play, and narrative experiences

---

## Core Economy

### Egg Acquisition

Viewers earn eggs through multiple channels:

#### 1. **Watch Time (Loyalty System)**
- Reward: **10-20 eggs per 10 minutes** of watch time
- Streamer.bot Configuration: Use Twitch loyalty point integration
- Notes: Encourages consistent viewership

#### 2. **Chat Messages**
- Reward: **5 eggs per message** (with cooldown)
- Cooldown: **60 seconds** per user
- Command: Automatic on chat message
- Notes: Prevents spam, encourages engagement

#### 3. **Cheering Bits**
- Reward: **1 egg per bit**
- Example: 100 bits = 100 eggs
- Command: Automatic on cheer event
- Notes: Monetary support directly converts to currency

#### 4. **Subscriptions**
- **Tier 1 Sub**: 500 eggs
- **Tier 2 Sub**: 1000 eggs
- **Tier 3 Sub**: 2000 eggs
- **Gift Sub**: 500 eggs (per recipient)
- Command: Automatic on subscription event
- Notes: Substantial reward for supporter commitment

#### 5. **Raids**
- Reward: **10 eggs per raider**
- Example: 50-person raid = 500 eggs (to raiding streamer)
- Command: Automatic on raid event
- Notes: Encourages community building

### Token System

Eggs can be converted into specialized tokens for specific game modes:

#### 🎲 D20 Tokens
- **Cost**: 100 eggs = 1 D20 Token
- **Purpose**: Personal Adventure system
- **Command**: `!buyD20 [amount]`
- **Example**: `!buyD20 5` (costs 500 eggs, gives 5 D20 Tokens)

#### 🎰 RRTokens (Roulette Tokens)
- **Cost**: 50 eggs = 1 RRToken
- **Purpose**: Roulette games and PvP battles
- **Command**: `!buyRRT [amount]`
- **Example**: `!buyRRT 10` (costs 500 eggs, gives 10 RRTokens)

### Inventory Commands

#### `!eggs`
- **Description**: Check your current egg balance
- **Response**: "🥚 @{user}, you have **{eggCount}** eggs!"
- **Cooldown**: 5 seconds per user

#### `!eggpack`
- **Description**: View your complete inventory (eggs and tokens)
- **Response**: 
  ```
  🎒 @{user}'s Eggpack:
  🥚 Eggs: {eggCount}
  🎲 D20 Tokens: {d20Tokens}
  🎰 RRTokens: {rrTokens}
  ```
- **Cooldown**: 10 seconds per user

#### `!top`
- **Description**: View the egg leaderboard (top 10 users)
- **Response**: 
  ```
  🏆 Top Egg Holders:
  1. @User1 - 5000 eggs
  2. @User2 - 4500 eggs
  3. @User3 - 4200 eggs
  ...
  ```
- **Cooldown**: 30 seconds globally

---

## Games (Spending Eggs)

### Roll20 (Egg Game)

A D20 rolling game where users spend eggs to roll a 20-sided die and win eggs based on the outcome.

#### Command: `!roll20 [wager]`

**Usage**: `!roll20 50` (wagers 50 eggs)

**Mechanics**:
1. User wagers a specific number of eggs (minimum 10, maximum 500)
2. System rolls a D20 (1-20)
3. Outcome determines egg winnings:
   - **Roll 1 (Critical Fail)**: Lose wager + 50% penalty
   - **Roll 2-5**: Lose wager
   - **Roll 6-10**: Lose 50% of wager
   - **Roll 11-14**: Get wager back (no profit)
   - **Roll 15-18**: Win 1.5x wager
   - **Roll 19**: Win 2x wager
   - **Roll 20 (Critical Success)**: Win 5x wager + bonus 100 eggs

**Response Examples**:
```
🎲 @{user} rolled a **{rollResult}**!
- Critical Success! You won {winAmount} eggs! 🎉
- Total Eggs: {newEggCount}
```

**Configuration Notes**:
- Cooldown: 30 seconds per user
- Maximum wager: 500 eggs (prevents excessive loss)
- Minimum wager: 10 eggs

### Roulette

A random outcome game where users wager eggs and can win or lose based on a weighted random result.

#### Command: `!roulette [wager]`

**Usage**: `!roulette 100` (wagers 100 eggs)

**Mechanics**:
1. User wagers eggs (minimum 25, maximum 1000)
2. System generates a random outcome based on weighted probabilities
3. Possible outcomes:
   - **Jackpot (5% chance)**: Win 5x wager + 200 eggs
   - **Big Win (10% chance)**: Win 3x wager
   - **Win (20% chance)**: Win 2x wager
   - **Small Win (25% chance)**: Win 1.5x wager
   - **Push (15% chance)**: Get wager back
   - **Small Loss (15% chance)**: Lose wager
   - **Big Loss (8% chance)**: Lose wager + 1 RRToken (if available)
   - **Catastrophe (2% chance)**: Lose wager + 50% of current eggs (capped at 500 egg loss)

**Response Examples**:
```
🎰 @{user} spins the roulette...
Result: 🌟 JACKPOT! 🌟
You won {winAmount} eggs!
Total Eggs: {newEggCount}
```

**Configuration Notes**:
- Cooldown: 45 seconds per user
- Maximum wager: 1000 eggs
- Minimum wager: 25 eggs
- High-risk, high-reward gameplay

---

## PvP System

Token-based player-vs-player battles with D&D-style combat narration. Players wager RRTokens, and outcomes are determined by random rolls with narrative flavor.

### Command: `!pvp @[opponent] [wager]`

**Usage**: `!pvp @User2 5` (challenges User2, wagering 5 RRTokens each)

**Mechanics**:
1. Challenger initiates with `!pvp @opponent [wager]`
2. Opponent has 60 seconds to accept with `!accept`
3. Both players must have the wagered RRTokens
4. System simulates a D&D-style combat encounter:
   - Each player rolls initiative (D20)
   - Higher roll attacks first
   - Attack rolls vs. Defense rolls (D20 + modifiers)
   - 3 rounds of combat
5. Winner determined by best of 3 rounds or total damage
6. Rewards:
   - **Winner**: Gets opponent's wagered tokens + bonus 50 eggs
   - **Loser**: Loses wagered tokens, gets consolation 10 eggs
   - **Draw**: Both players keep tokens, get 25 eggs each

**Combat Narration Examples**:
```
⚔️ PvP Battle: @User1 vs @User2 (5 RRTokens wagered)

🎲 Initiative!
@User1 rolls 18, @User2 rolls 12
@User1 strikes first!

Round 1:
@User1 swings a mighty axe! (Rolled 16) 💥
@User2 attempts to dodge! (Rolled 8)
Hit! @User1 deals 8 damage!

Round 2:
@User2 casts a fireball! (Rolled 19) 🔥
@User1 tries to resist! (Rolled 14)
Critical Hit! @User2 deals 12 damage!

Round 3:
@User1 charges with their shield! (Rolled 11)
@User2 parries! (Rolled 15)
Miss! @User2 counters for 5 damage!

⚔️ Final Result: @User2 WINS! 🏆
- @User2 gains 5 RRTokens + 50 eggs
- @User1 receives 10 consolation eggs
```

**Configuration Notes**:
- Accept timeout: 60 seconds
- Cooldown: 120 seconds per user
- Minimum wager: 1 RRToken
- Maximum wager: 20 RRTokens
- Requires both players to be present and have sufficient tokens

**Alternative Command**: `!duel @[opponent] [wager]` (alias for !pvp)

---

## Personal Adventure System

A narrative-driven D&D-style game where users embark on daily story scenarios. Each user has their own persistent adventure that evolves based on their choices and dice rolls.

### Command: `!adventure`

**Usage**: `!adventure` (costs 1 D20 Token per use)

**Mechanics**:
1. User spends 1 D20 Token to trigger their daily adventure
2. System generates or continues a personalized narrative scenario
3. Player faces a challenge requiring a saving throw
4. Six saving throw types (D&D 5e style):
   - **STR** (Strength): Physical power, athletics
   - **DEX** (Dexterity): Agility, reflexes, stealth
   - **CON** (Constitution): Endurance, resilience
   - **INT** (Intelligence): Knowledge, logic, investigation
   - **WIS** (Wisdom): Perception, insight, survival
   - **CHA** (Charisma): Persuasion, deception, performance
5. Player rolls D20 + modifier against a Difficulty Class (DC)
6. Success/failure determines story outcome and rewards

**Saving Throw DCs**:
- **Easy**: DC 10 (70% success rate)
- **Medium**: DC 15 (50% success rate)
- **Hard**: DC 18 (30% success rate)
- **Very Hard**: DC 22 (15% success rate)

**Story Persistence**:
- Each user has a unique adventure state stored per-user
- Adventures evolve over multiple sessions
- Choices and outcomes carry forward
- Story can branch based on previous results

**Rewards**:
- **Success**: 50-200 eggs (scales with DC difficulty)
- **Failure**: 10-25 eggs (consolation)
- **Critical Success (Natural 20)**: 300 eggs + 1 bonus D20 Token
- **Critical Failure (Natural 1)**: Lose 50 eggs (story consequence)

**Example Adventure**:
```
🗡️ @{user}'s Adventure Continues...

📖 Story:
You stand at the entrance of an ancient temple. Vines cover 
crumbling stone pillars, and an eerie silence fills the air. 
As you step inside, the floor begins to collapse beneath you!

🎲 Challenge: Make a DEX saving throw! (DC 15)
Type !save to attempt!

[User types: !save]

🎲 @{user} rolls DEX saving throw: 17 (rolled 15 + 2 modifier)
✅ Success!

📖 Outcome:
With lightning reflexes, you leap to safety as the floor 
crumbles away! You spot a glowing artifact on a pedestal ahead.

🎁 Reward: +100 eggs!
🥚 Total Eggs: {newEggCount}

📚 Your adventure will continue next time you use !adventure...
```

**Configuration Notes**:
- Cooldown: 1 use per day per user (24-hour cooldown)
- Cost: 1 D20 Token per adventure
- Story templates: 50+ unique scenarios
- User data persistence required
- Modifier system: Users gain +1 to +3 modifiers based on total adventures completed

### Saving Throw Command: `!save`

**Usage**: `!save` (used within an active adventure)

**Mechanics**:
- Only usable when user has an active adventure challenge
- Rolls D20 + user's modifier for the required stat
- Resolves the current story challenge
- Provides narrative outcome and rewards

---

## Backend Economy Management

### Egg Sinks (Spending Mechanisms)

To maintain a balanced economy and prevent infinite egg accumulation, the system includes multiple egg sinks:

1. **Token Purchases**: Primary sink (D20 Tokens, RRTokens)
2. **Roll20 Game**: Risk-based gambling sink
3. **Roulette**: High-risk gambling sink
4. **Failed Adventures**: Potential egg loss on critical failures
5. **Special Events**: Limited-time items or cosmetics (future expansion)

### Economy Balancing Guidelines

#### Egg Income vs. Spending Ratios
- **Target**: Users should spend approximately 60-70% of earned eggs
- **Watch Time Income**: ~120 eggs/hour (base rate)
- **Expected Spending**: ~80-100 eggs/hour on games and tokens
- **Net Gain**: ~20-40 eggs/hour (allows slow accumulation)

#### Token Economy
- **D20 Token**: High value (100 eggs), limited daily use (adventure cooldown)
- **RRToken**: Medium value (50 eggs), used for competitive play
- **Conversion Rate**: Designed to encourage token purchases for special content

#### Adjustment Levers
1. **Egg Rewards**: Adjust watch time, chat, and event multipliers
2. **Token Costs**: Modify egg-to-token conversion rates
3. **Game Payouts**: Tweak Roll20 and Roulette multipliers
4. **Cooldowns**: Adjust command cooldowns to control spending rate
5. **Special Events**: Introduce temporary sinks or income boosts

### Periodic Events

#### Double Egg Weekend
- **Frequency**: Once per month
- **Effect**: 2x egg rewards from all sources
- **Duration**: 48 hours
- **Goal**: Drive engagement and reward loyal viewers

#### Token Sale
- **Frequency**: Quarterly
- **Effect**: 25% discount on token purchases (e.g., 75 eggs for 1 D20 Token)
- **Duration**: 24 hours
- **Goal**: Encourage token acquisition and game participation

#### Adventure Marathon
- **Frequency**: Bi-monthly
- **Effect**: Remove daily cooldown on !adventure
- **Duration**: Stream duration (4-8 hours)
- **Goal**: Provide intense narrative gameplay session

---

## Streamer.bot Configuration

### Prerequisites
- Streamer.bot installed and connected to Twitch
- Database or persistent storage for user data (JSON file or SQLite recommended)
- Basic C# scripting knowledge for custom actions

### Step 1: User Data Structure

Create a user data storage system to track:
- Username (Twitch ID)
- Egg count (integer)
- D20 Token count (integer)
- RRToken count (integer)
- Adventure state (string/JSON)
- Last adventure timestamp (datetime)
- Total adventures completed (integer)
- Saving throw modifiers (STR, DEX, CON, INT, WIS, CHA)

**Example JSON Structure**:
```json
{
  "users": {
    "user123": {
      "username": "CoolViewer",
      "eggs": 1250,
      "d20Tokens": 5,
      "rrTokens": 10,
      "adventureState": "temple_entrance",
      "lastAdventure": "2025-12-30T15:30:00Z",
      "totalAdventures": 15,
      "modifiers": {
        "STR": 2,
        "DEX": 1,
        "CON": 1,
        "INT": 3,
        "WIS": 2,
        "CHA": 1
      }
    }
  }
}
```

### Step 2: Twitch Event Actions

Configure Streamer.bot actions for automatic egg rewards:

#### Watch Time Rewards (Loyalty Integration)
1. Create Action: "Loyalty Egg Reward"
2. Trigger: Twitch Loyalty Point Award (every 10 minutes)
3. Sub-Actions:
   - C# Code: Add 15 eggs to user data
   - Send Chat Message: "🥚 @{user} earned 15 eggs for watching!"

#### Chat Message Rewards
1. Create Action: "Chat Egg Reward"
2. Trigger: Chat Message (with 60-second cooldown per user)
3. Sub-Actions:
   - C# Code: Add 5 eggs to user data
   - (Optional) Send whisper: "🥚 +5 eggs!"

#### Cheer Rewards
1. Create Action: "Cheer Egg Reward"
2. Trigger: Cheer Event
3. Sub-Actions:
   - C# Code: Add eggs equal to bits amount
   - Send Chat Message: "🥚 @{user} earned {bits} eggs from cheering! Thank you!"

#### Subscription Rewards
1. Create Action: "Sub Egg Reward"
2. Trigger: Subscription Event
3. Sub-Actions:
   - C# Code: 
     - Tier 1: Add 500 eggs
     - Tier 2: Add 1000 eggs
     - Tier 3: Add 2000 eggs
   - Send Chat Message: "🥚 @{user} earned {eggAmount} eggs for subscribing! Welcome to the nest!"

#### Raid Rewards
1. Create Action: "Raid Egg Reward"
2. Trigger: Raid Event
3. Sub-Actions:
   - C# Code: Add (raider count × 10) eggs to raiding streamer
   - Send Chat Message: "🥚 Thanks for the raid @{raider}! You earned {eggAmount} eggs!"

### Step 3: Command Configuration

Configure chat commands for user interaction:

#### !eggs Command
- **Command**: !eggs
- **Permission**: Everyone
- **Cooldown**: 5 seconds per user
- **Action**: Display user's egg count from database
- **Response**: "🥚 @{user}, you have **{eggCount}** eggs!"

#### !eggpack Command
- **Command**: !eggpack
- **Permission**: Everyone
- **Cooldown**: 10 seconds per user
- **Action**: Display full inventory (eggs, tokens)
- **Response**: Multi-line inventory display

#### !top Command
- **Command**: !top
- **Permission**: Everyone
- **Cooldown**: 30 seconds global
- **Action**: Query database for top 10 egg holders
- **Response**: Leaderboard display

#### !buyD20 Command
- **Command**: !buyD20 [amount]
- **Permission**: Everyone
- **Cooldown**: 10 seconds per user
- **Action**: 
  1. Check if user has sufficient eggs (amount × 100)
  2. Deduct eggs, add D20 Tokens
  3. Update database
- **Response**: "🎲 @{user} purchased {amount} D20 Token(s) for {cost} eggs!"

#### !buyRRT Command
- **Command**: !buyRRT [amount]
- **Permission**: Everyone
- **Cooldown**: 10 seconds per user
- **Action**: 
  1. Check if user has sufficient eggs (amount × 50)
  2. Deduct eggs, add RRTokens
  3. Update database
- **Response**: "🎰 @{user} purchased {amount} RRToken(s) for {cost} eggs!"

#### !roll20 Command
- **Command**: !roll20 [wager]
- **Permission**: Everyone
- **Cooldown**: 30 seconds per user
- **Action**:
  1. Validate wager (10-500 eggs)
  2. Check user has sufficient eggs
  3. Roll D20
  4. Calculate outcome
  5. Update user eggs
  6. Send narrative response
- **C# Pseudocode**:
```csharp
int wager = int.Parse(args[0]);
int roll = random.Next(1, 21);
int result = 0;

switch(roll) {
    case 1: result = -wager - (wager / 2); break; // Crit fail
    case 2: case 3: case 4: case 5: result = -wager; break;
    case 6: case 7: case 8: case 9: case 10: result = -(wager / 2); break;
    case 11: case 12: case 13: case 14: result = 0; break;
    case 15: case 16: case 17: case 18: result = wager / 2; break;
    case 19: result = wager; break;
    case 20: result = (wager * 4) + 100; break; // Crit success
}

UpdateUserEggs(userId, result);
SendMessage($"🎲 @{user} rolled a {roll}! {GetRollFlavor(roll)} Result: {result:+#;-#;0} eggs!");
```

#### !roulette Command
- **Command**: !roulette [wager]
- **Permission**: Everyone
- **Cooldown**: 45 seconds per user
- **Action**:
  1. Validate wager (25-1000 eggs)
  2. Check user has sufficient eggs
  3. Generate weighted random outcome
  4. Calculate result
  5. Update user eggs/tokens
  6. Send narrative response

#### !pvp Command
- **Command**: !pvp @[opponent] [wager]
- **Permission**: Everyone
- **Cooldown**: 120 seconds per user
- **Action**:
  1. Validate both users have sufficient RRTokens
  2. Create PvP challenge (60-second acceptance window)
  3. Wait for !accept from opponent
  4. Simulate D&D combat (3 rounds)
  5. Determine winner
  6. Update tokens and eggs
  7. Send combat narration

#### !accept Command
- **Command**: !accept
- **Permission**: Everyone
- **Cooldown**: None
- **Action**: Accept pending PvP challenge

#### !adventure Command
- **Command**: !adventure
- **Permission**: Everyone
- **Cooldown**: 24 hours per user
- **Action**:
  1. Check user has at least 1 D20 Token
  2. Check 24-hour cooldown
  3. Deduct 1 D20 Token
  4. Generate/continue adventure scenario
  5. Present challenge
  6. Wait for !save command
  7. Store adventure state

#### !save Command
- **Command**: !save
- **Permission**: Everyone
- **Cooldown**: None (requires active adventure)
- **Action**:
  1. Check for active adventure
  2. Roll D20 + modifier
  3. Compare to DC
  4. Resolve outcome
  5. Award eggs
  6. Update adventure state
  7. Send narrative result

### Step 4: C# Scripting Examples

**Note**: These are example functions to demonstrate the core logic. You'll need to adapt them to your specific Streamer.bot setup. The `GetUserEggs()` and `UpdateUserEggs()` helper functions referenced in later examples should be implemented based on the Egg Update Function pattern shown below.

#### Egg Update Function
```csharp
using System;
using System.IO;
using Newtonsoft.Json.Linq;

public class CPHInline
{
    public bool Execute()
    {
        string userId = args["userId"].ToString();
        int eggChange = int.Parse(args["eggChange"].ToString());
        
        // Load user data
        string dataPath = @"C:\StreamerBot\UserData\eggs.json";
        string jsonData = File.ReadAllText(dataPath);
        JObject data = JObject.Parse(jsonData);
        
        // Update eggs
        if (data["users"][userId] == null) {
            // Initialize new user
            data["users"][userId] = new JObject();
            data["users"][userId]["eggs"] = 0;
            data["users"][userId]["d20Tokens"] = 0;
            data["users"][userId]["rrTokens"] = 0;
        }
        
        int currentEggs = (int)data["users"][userId]["eggs"];
        int newEggs = Math.Max(0, currentEggs + eggChange);
        data["users"][userId]["eggs"] = newEggs;
        
        // Save data
        File.WriteAllText(dataPath, data.ToString());
        
        CPH.SetArgument("newEggCount", newEggs);
        return true;
    }
}
```

#### Roll20 Function
```csharp
using System;

public class CPHInline
{
    public bool Execute()
    {
        string userId = args["userId"].ToString();
        string userName = args["userName"].ToString();
        int wager = int.Parse(args["wager"].ToString());
        
        // Validate wager
        if (wager < 10 || wager > 500) {
            CPH.SendMessage($"@{userName}, wager must be between 10 and 500 eggs!");
            return false;
        }
        
        // Check balance (GetUserEggs is a helper function - see Egg Update Function above)
        int currentEggs = GetUserEggs(userId);
        if (currentEggs < wager) {
            CPH.SendMessage($"@{userName}, you don't have enough eggs! You have {currentEggs} eggs.");
            return false;
        }
        
        // Roll D20
        Random rnd = new Random();
        int roll = rnd.Next(1, 21);
        
        // Calculate result
        int result = 0;
        string flavor = "";
        
        if (roll == 1) {
            result = -(wager + wager / 2);
            flavor = "💀 CRITICAL FAIL!";
        } else if (roll >= 2 && roll <= 5) {
            result = -wager;
            flavor = "❌ Miss!";
        } else if (roll >= 6 && roll <= 10) {
            result = -(wager / 2);
            flavor = "😬 Partial Loss";
        } else if (roll >= 11 && roll <= 14) {
            result = 0;
            flavor = "😐 Push";
        } else if (roll >= 15 && roll <= 18) {
            result = wager / 2;
            flavor = "✅ Hit!";
        } else if (roll == 19) {
            result = wager;
            flavor = "🌟 Great Roll!";
        } else if (roll == 20) {
            result = wager * 4 + 100;
            flavor = "💎 CRITICAL SUCCESS!";
        }
        
        // Update eggs (UpdateUserEggs is a helper function - see Egg Update Function above)
        UpdateUserEggs(userId, result);
        int newEggs = currentEggs + result;
        
        // Send message
        string resultStr = result > 0 ? $"+{result}" : result.ToString();
        CPH.SendMessage($"🎲 @{userName} rolled a {roll}! {flavor} Result: {resultStr} eggs! Total: {newEggs} 🥚");
        
        return true;
    }
}
```

### Step 5: Adventure Story Templates

Create a story template system with 50+ scenarios. Store in separate JSON file:

```json
{
  "adventures": [
    {
      "id": "temple_001",
      "title": "The Crumbling Temple",
      "description": "You stand at the entrance of an ancient temple...",
      "challenge": "DEX",
      "dc": 15,
      "successOutcome": "You leap to safety and find a glowing artifact!",
      "failureOutcome": "You fall into a pit, but manage to grab the edge.",
      "successReward": 100,
      "failureReward": 25,
      "nextAdventures": ["temple_002", "temple_003"]
    },
    {
      "id": "forest_001",
      "title": "Whispering Woods",
      "description": "Strange noises echo through the dark forest...",
      "challenge": "WIS",
      "dc": 12,
      "successOutcome": "You identify the sounds as friendly forest spirits.",
      "failureOutcome": "You get turned around and lose your way.",
      "successReward": 75,
      "failureReward": 20,
      "nextAdventures": ["forest_002", "village_001"]
    }
  ]
}
```

### Step 6: Testing and Validation

1. **Test Egg Acquisition**:
   - Verify watch time rewards
   - Test chat message rewards with cooldown
   - Simulate cheer, sub, and raid events

2. **Test Commands**:
   - Execute all commands with various parameters
   - Test edge cases (negative numbers, insufficient balance)
   - Verify cooldowns work correctly

3. **Test Games**:
   - Run Roll20 multiple times, verify odds
   - Test Roulette weighted outcomes
   - Simulate PvP battles

4. **Test Adventures**:
   - Complete full adventure cycle
   - Verify story persistence
   - Test 24-hour cooldown

5. **Test Economy Balance**:
   - Monitor egg accumulation rates
   - Adjust multipliers if needed
   - Verify egg sinks are effective

---

## Command Reference

### User Commands

| Command | Parameters | Cost | Cooldown | Description |
|---------|-----------|------|----------|-------------|
| `!eggs` | None | Free | 5s/user | Check egg balance |
| `!eggpack` | None | Free | 10s/user | View full inventory |
| `!top` | None | Free | 30s/global | View egg leaderboard |
| `!buyD20` | [amount] | 100 eggs/token | 10s/user | Purchase D20 Tokens |
| `!buyRRT` | [amount] | 50 eggs/token | 10s/user | Purchase RRTokens |
| `!roll20` | [wager] | 10-500 eggs | 30s/user | Play Roll20 game |
| `!roulette` | [wager] | 25-1000 eggs | 45s/user | Play Roulette |
| `!pvp` | @opponent [wager] | 1-20 RRTokens | 120s/user | Challenge to PvP |
| `!accept` | None | None | None | Accept PvP challenge |
| `!duel` | @opponent [wager] | 1-20 RRTokens | 120s/user | Alias for !pvp |
| `!adventure` | None | 1 D20 Token | 24h/user | Start/continue adventure |
| `!save` | None | None | None | Make saving throw in adventure |

### Moderator Commands (Optional)

| Command | Parameters | Description |
|---------|-----------|-------------|
| `!giveggs` | @user [amount] | Grant eggs to user |
| `!takeggs` | @user [amount] | Remove eggs from user |
| `!resetuser` | @user | Reset user's economy data |
| `!ecobalance` | None | Display economy statistics |

---

## Balance Guidelines

### Initial Setup Recommendations

1. **Starting Eggs**: 100 eggs (welcome bonus)
2. **Watch Time**: 15 eggs per 10 minutes
3. **Chat Reward**: 5 eggs per message (60s cooldown)
4. **Token Costs**: D20 = 100 eggs, RRToken = 50 eggs

### Monitoring Metrics

Track these metrics to maintain balance:

1. **Average Eggs Per User**: Target 500-2000 range
2. **Daily Egg Generation**: Watch time + events + bonuses
3. **Daily Egg Sinks**: Token purchases + game losses
4. **Net Daily Change**: Should be small positive (20-50 eggs/user/day)
5. **Token Velocity**: Tokens should be used, not hoarded

### Adjustment Strategies

#### If Eggs Accumulate Too Quickly:
- Reduce watch time rewards (10-12 eggs per 10 min)
- Increase token costs (D20 = 125 eggs, RRToken = 60 eggs)
- Add new egg sinks (cosmetics, channel point multipliers)
- Reduce Roll20 payout multipliers

#### If Eggs Are Too Scarce:
- Increase watch time rewards (18-20 eggs per 10 min)
- Reduce token costs (D20 = 75 eggs, RRToken = 40 eggs)
- Improve Roll20 odds (better payouts on 15-18 range)
- Run more frequent double egg events

#### If Tokens Accumulate:
- Add more token-exclusive rewards
- Create token-only games or mini-events
- Increase token costs for PvP (minimum 2-3 tokens)
- Add prestige items purchasable with tokens

#### If Users Don't Engage:
- Reduce command cooldowns
- Increase game payout excitement (bigger jackpots)
- Add community goals (unlock bonuses at milestones)
- Create limited-time events or seasonal adventures

### Long-Term Economy Health

- **Week 1**: Monitor closely, expect high engagement
- **Week 2-4**: Fine-tune multipliers based on data
- **Month 2+**: Establish baseline, plan periodic events
- **Quarterly**: Major balance review and feature additions

---

## Advanced Features (Future Expansion)

### Possible Enhancements

1. **Egg Shop**: Cosmetic items, channel emotes, or special roles
2. **Guild System**: Team-based egg pooling and competitions
3. **Egg Battles**: Strategy game where users command egg armies
4. **Seasonal Events**: Holiday-themed adventures and rewards
5. **Prestige System**: Reset eggs for permanent modifiers
6. **Achievement System**: Unlock titles and badges
7. **Trading System**: Allow users to trade tokens/eggs
8. **Boss Fights**: Community PvE events with shared rewards

### Integration Ideas

- **Discord Bot**: Mirror economy across platforms
- **Website Dashboard**: Live leaderboards and stats
- **Mobile App**: Check inventory and participate remotely
- **Twitch Extensions**: Visual inventory and quick commands

---

## Troubleshooting

### Common Issues

**Issue**: Commands not responding
- **Solution**: Check Streamer.bot connection to Twitch, verify command triggers are enabled

**Issue**: Egg counts not saving
- **Solution**: Verify file permissions for JSON storage, check C# code for errors

**Issue**: Users losing eggs unexpectedly
- **Solution**: Review game logic for negative values, ensure Math.Max(0, value) is used

**Issue**: PvP not starting
- **Solution**: Check both users have sufficient tokens, verify 60-second timer is active

**Issue**: Adventure cooldown not working
- **Solution**: Ensure timestamp comparison uses UTC time, verify database updates

### Support Resources

- Streamer.bot Documentation: https://wiki.streamer.bot
- Community Discord: [Your community server]
- GitHub Repository: [Your repo link]
- Video Tutorial: [Tutorial link if available]

---

## Conclusion

The **Unified Eggonomy System** provides a comprehensive, engaging, and balanced economy for your Twitch community. By combining passive rewards, active gameplay, competitive PvP, and narrative adventures, you create multiple engagement vectors that appeal to different viewer preferences.

Key to success:
- **Monitor** your economy metrics regularly
- **Adjust** multipliers based on community behavior
- **Listen** to viewer feedback about balance
- **Iterate** with new features and events
- **Have fun** with your community!

This system is designed to grow with your stream. Start with core features, monitor engagement, and expand based on what resonates with your viewers.

Good luck, and may your nest be full of eggs! 🥚🎮✨

---

## Version History

- **v1.0** (2025-12-31): Initial unified documentation
  - Core economy system
  - Roll20 and Roulette games
  - PvP battle system
  - Personal Adventure system
  - Balance guidelines and configuration instructions

---

*For questions, support, or contributions, please contact the stream moderators or visit the GitHub repository.*
