# Testing Guide for Unified Eggonomy System

This guide provides comprehensive testing scenarios for all components of the Unified Eggonomy System.

## Prerequisites

Before testing:
1. Streamer.bot is installed and running
2. Connected to Twitch channel
3. `eggs.json` file created at `C:\StreamerBot\UserData\eggs.json` with `{"users": {}}`
4. `adventure-stories.json` copied to `C:\StreamerBot\UserData\adventure-stories.json`
5. All actions imported and enabled
6. Test with at least 2 Twitch accounts (one for challenger/opponent testing)

## Test Categories

### 1. Reward Actions Testing

#### Chat Rewards
**Action:** `action-chat-egg-reward.json`
- [ ] Send a chat message from test account
- [ ] Wait 5 seconds for processing
- [ ] Check `eggs.json` - user should have 5 eggs
- [ ] Send another message immediately - should NOT trigger (60s cooldown)
- [ ] Wait 60 seconds and send another message - should add 5 more eggs

**Expected Result:** User gains 5 eggs per message with 60s cooldown

#### Cheer Rewards
**Action:** `action-cheer-reward.json`
- [ ] Simulate a cheer event with 100 bits
- [ ] Check `eggs.json` - user should have gained 100 eggs
- [ ] Chat should display reward message

**Expected Result:** 1 egg per bit cheered

#### Subscription Rewards
**Action:** `action-subscription-reward.json`
- [ ] Simulate Tier 1 subscription - should grant 500 eggs
- [ ] Simulate Tier 2 subscription - should grant 1000 eggs
- [ ] Simulate Tier 3 subscription - should grant 2000 eggs
- [ ] Check `eggs.json` for correct amounts

**Expected Result:** Eggs granted based on tier level

#### Raid Rewards
**Action:** `action-raid-reward.json`
- [ ] Simulate raid with 50 viewers
- [ ] Check `eggs.json` - raider should have 500 eggs (50 × 10)
- [ ] Chat should display reward message

**Expected Result:** 10 eggs per raider

---

### 2. Basic Commands Testing

#### !eggs Command
**File:** `command-eggs.json`

Test Scenarios:
- [ ] User with 0 eggs: `!eggs` → "you have 0 eggs"
- [ ] User with eggs: `!eggs` → "you have X eggs"
- [ ] Rapid fire: Send `!eggs` twice in 3 seconds → Second should be blocked (5s cooldown)

**Expected Result:** Displays current egg balance with 5s cooldown

#### !eggpack Command
**File:** `command-eggpack.json`

Test Scenarios:
- [ ] New user: `!eggpack` → Shows 0 eggs, 0 tokens
- [ ] User with inventory: `!eggpack` → Shows eggs and tokens correctly
- [ ] Rapid fire: Send twice in 8 seconds → Second blocked (10s cooldown)

**Expected Result:** Displays full inventory (eggs, D20 tokens, RRTokens) with 10s cooldown

#### !top Command
**File:** `command-top.json`

Test Scenarios:
- [ ] Empty database: `!top` → "No egg data yet"
- [ ] With users: `!top` → Shows top 10 users sorted by eggs
- [ ] Rapid fire (different users): Send twice in 20s → Second blocked (30s global cooldown)

**Expected Result:** Leaderboard of top 10 egg holders with 30s global cooldown

---

### 3. Token System Testing

#### !buyD20 Command
**File:** `command-buyD20.json`

Test Scenarios:
- [ ] User with 0 eggs: `!buyD20 1` → "you don't have enough eggs"
- [ ] User with 50 eggs: `!buyD20 1` → "you don't have enough eggs" (need 100)
- [ ] User with 100 eggs: `!buyD20 1` → Success, gains 1 D20 token, loses 100 eggs
- [ ] User with 500 eggs: `!buyD20 5` → Success, gains 5 D20 tokens, loses 500 eggs
- [ ] Invalid input: `!buyD20 abc` → Error message
- [ ] No input: `!buyD20` → Usage message

**Expected Result:** Purchases D20 tokens at 100 eggs each with 10s cooldown

#### !buyRRT Command
**File:** `command-buyRRT.json`

Test Scenarios:
- [ ] User with 0 eggs: `!buyRRT 1` → Error
- [ ] User with 25 eggs: `!buyRRT 1` → Error (need 50)
- [ ] User with 50 eggs: `!buyRRT 1` → Success, gains 1 RRToken, loses 50 eggs
- [ ] User with 500 eggs: `!buyRRT 10` → Success, gains 10 RRTokens, loses 500 eggs

**Expected Result:** Purchases RRTokens at 50 eggs each with 10s cooldown

---

### 4. Games Testing

#### !roll20 Command
**File:** `command-roll20.json`

Test Scenarios:
- [ ] No wager: `!roll20` → Usage message
- [ ] Wager too low: `!roll20 5` → Error (min 10)
- [ ] Wager too high: `!roll20 600` → Error (max 500)
- [ ] Insufficient eggs: User with 30 eggs, `!roll20 50` → Error
- [ ] Valid wager: User with 100 eggs, `!roll20 50` → Game plays

Test Multiple Rolls (to verify odds):
- [ ] Roll at least 10 times and verify various outcomes occur
- [ ] Verify roll 1 (crit fail) loses wager + 50%
- [ ] Verify roll 20 (crit success) wins wager × 4 + 100

**Expected Result:** D20 roll game with varied outcomes based on roll (1-20)

#### !roulette Command
**File:** `command-roulette.json`

Test Scenarios:
- [ ] No wager: `!roulette` → Usage message
- [ ] Wager too low: `!roulette 20` → Error (min 25)
- [ ] Wager too high: `!roulette 1500` → Error (max 1000)
- [ ] Insufficient eggs: User with 50 eggs, `!roulette 100` → Error
- [ ] Valid wager: User with 200 eggs, `!roulette 100` → Game plays

Test Multiple Spins:
- [ ] Play 20+ times to see different outcomes
- [ ] Verify jackpot (5% chance) occurs
- [ ] Verify catastrophe (2% chance) occurs
- [ ] Verify big loss can remove RRToken if available

**Expected Result:** Weighted random outcomes with various win/loss scenarios

---

### 5. PvP System Testing

#### !pvp Command
**File:** `command-pvp.json`

Test Scenarios:
- [ ] No parameters: `!pvp` → Usage message
- [ ] Invalid wager: `!pvp @user 0` → Error
- [ ] Wager too high: `!pvp @user 25` → Error (max 20)
- [ ] Challenge self: `!pvp @self 5` → Error
- [ ] User doesn't exist: `!pvp @fakeuserxyz123 5` → Error
- [ ] Insufficient tokens (challenger): User with 2 RRTokens, `!pvp @user 5` → Error
- [ ] Insufficient tokens (opponent): Opponent with 2 RRTokens, `!pvp @opponent 5` → Error
- [ ] Valid challenge: Both users with 10+ RRTokens, `!pvp @user 5` → Challenge created

**!duel Alias:**
- [ ] Test `!duel @user 5` → Should work same as !pvp

**Expected Result:** Creates PvP challenge with 60s acceptance window

#### !accept Command
**File:** `command-accept.json`

Test Scenarios:
- [ ] No pending challenge: `!accept` → Error message
- [ ] Expired challenge (>60s): Create challenge, wait 65s, `!accept` → Error
- [ ] Valid acceptance: Create challenge, immediate `!accept` → Battle executes

Battle Verification:
- [ ] Verify initiative rolls displayed
- [ ] Verify 3 rounds of combat with rolls
- [ ] Verify winner announced
- [ ] Verify tokens transferred correctly
- [ ] Verify bonus eggs awarded (winner +50, loser +10)
- [ ] Verify draw scenario (both keep tokens, +25 eggs each)

**Expected Result:** Accepts challenge and executes D&D-style combat simulation

---

### 6. Adventure System Testing

#### !adventure Command
**File:** `command-adventure.json`

Test Scenarios:
- [ ] User with 0 D20 tokens: `!adventure` → Error
- [ ] User with 1 D20 token: `!adventure` → Success, adventure starts
- [ ] Verify D20 token deducted
- [ ] Verify adventure story displayed with title, description, challenge
- [ ] Use `!adventure` again immediately → Error (24h cooldown)

Adventure Persistence:
- [ ] Start adventure, check `eggs.json` → Verify activeAdventures entry created
- [ ] Complete adventure, start new one → Should be different or linked story

**Expected Result:** Starts personalized adventure, costs 1 D20 token, 24h cooldown

#### !save Command
**File:** `command-save.json`

Test Scenarios:
- [ ] No active adventure: `!save` → Error
- [ ] Active adventure: `!save` → Rolls D20, resolves challenge
- [ ] Expired adventure (>10 min): Start adventure, wait 11 min, `!save` → Error

Roll Outcomes:
- [ ] Success: Total roll ≥ DC → Success outcome + reward
- [ ] Failure: Total roll < DC → Failure outcome + consolation
- [ ] Critical success (nat 20): → Maximum reward + bonus token
- [ ] Critical failure (nat 1): → Lose eggs

Verify After !save:
- [ ] Adventure state updated in `eggs.json`
- [ ] lastAdventure timestamp set
- [ ] totalAdventures incremented
- [ ] Eggs awarded/deducted correctly
- [ ] Active adventure cleared

**Expected Result:** Resolves adventure with D20 roll + modifiers vs DC

---

### 7. Moderator Commands Testing

**Prerequisites:** Must test with moderator or broadcaster account

#### !giveggs Command
**File:** `command-giveggs.json`

Test Scenarios:
- [ ] Non-mod user: `!giveggs @user 100` → Permission error
- [ ] No parameters: `!giveggs` → Usage message
- [ ] Invalid amount: `!giveggs @user abc` → Error
- [ ] User doesn't exist: `!giveggs @fakeuserxyz 100` → Error
- [ ] Valid grant: `!giveggs @user 500` → User receives 500 eggs

**Expected Result:** Moderator grants eggs to specified user

#### !takeggs Command
**File:** `command-takeggs.json`

Test Scenarios:
- [ ] Non-mod user: `!takeggs @user 50` → Permission error
- [ ] No parameters: `!takeggs` → Usage message
- [ ] User doesn't exist: `!takeggs @fakeuser 50` → Error
- [ ] Valid removal: User with 200 eggs, `!takeggs @user 100` → User has 100 eggs left
- [ ] Remove more than user has: User with 50 eggs, `!takeggs @user 100` → User has 0 eggs (floor at 0)

**Expected Result:** Moderator removes eggs from user (min 0)

#### !resetuser Command
**File:** `command-resetuser.json`

Test Scenarios:
- [ ] Non-mod user: `!resetuser @user` → Permission error
- [ ] No parameter: `!resetuser` → Usage message
- [ ] User doesn't exist: `!resetuser @fakeuser` → Error
- [ ] Valid reset: User with data, `!resetuser @user` → All data reset to 0

**Expected Result:** Resets user's eggs, tokens, and adventure data to 0

#### !ecobalance Command
**File:** `command-ecobalance.json`

Test Scenarios:
- [ ] Non-mod user: `!ecobalance` → Permission error
- [ ] Empty database: `!ecobalance` → Error or "no data"
- [ ] With user data: `!ecobalance` → Displays statistics

Verify Stats Displayed:
- [ ] Total users count
- [ ] Total eggs in circulation
- [ ] Total D20 tokens
- [ ] Total RRTokens
- [ ] Average eggs per user
- [ ] Max and min egg counts
- [ ] Total egg value equivalent

**Expected Result:** Displays comprehensive economy statistics

---

## Edge Cases and Error Handling

### File System Issues
- [ ] Delete `eggs.json` → Commands should recreate file
- [ ] Corrupt `eggs.json` (invalid JSON) → Should show error
- [ ] Delete `adventure-stories.json` → Adventure commands should error gracefully
- [ ] No write permissions on `eggs.json` → Should show error

### Concurrent Operations
- [ ] Two users using !buyD20 simultaneously
- [ ] User in PvP while also trying !adventure
- [ ] Multiple users triggering chat rewards at once

### Boundary Values
- [ ] User with exactly 0 eggs
- [ ] User with max integer eggs (999999999)
- [ ] Negative number inputs (should be rejected)
- [ ] Very long username inputs

### Race Conditions
- [ ] Accept PvP challenge at exactly 60 seconds
- [ ] Use !save at exactly 10 minutes after !adventure
- [ ] Multiple !top commands from different users at 30s mark

---

## Performance Testing

### Large Dataset
1. Create `eggs.json` with 1000+ users
2. Test !top command → Should complete quickly
3. Test !ecobalance → Should calculate correctly
4. Test individual user commands → Should not slow down

### Rapid Command Testing
1. Send same command 10 times in rapid succession → Cooldowns should work
2. Send different commands rapidly → All should process
3. Multiple users sending commands → All should process correctly

---

## Validation Checklist

After completing all tests:
- [ ] All JSON files are syntactically valid
- [ ] All commands have appropriate cooldowns
- [ ] All commands have proper error messages
- [ ] File operations are safe (no data loss)
- [ ] User data persists correctly
- [ ] Economy balance is maintained
- [ ] No infinite egg exploits exist
- [ ] Moderator commands require proper permissions
- [ ] All numeric calculations are correct
- [ ] All random outcomes are weighted properly

---

## Bug Reporting

If you find bugs during testing:
1. Document the exact steps to reproduce
2. Include the command used and any parameters
3. Include relevant sections from `eggs.json`
4. Check Streamer.bot logs for errors
5. Open an issue on GitHub with details

---

## Test Results Template

Use this template to document your test results:

```
## Test Session: [Date]
**Tester:** [Name]
**Streamer.bot Version:** [Version]

### Reward Actions: ✅ / ❌
- Chat Rewards: ✅
- Cheer Rewards: ✅
- Subscription Rewards: ✅
- Raid Rewards: ✅

### Basic Commands: ✅ / ❌
- !eggs: ✅
- !eggpack: ✅
- !top: ✅

### Token System: ✅ / ❌
- !buyD20: ✅
- !buyRRT: ✅

### Games: ✅ / ❌
- !roll20: ✅
- !roulette: ✅

### PvP System: ✅ / ❌
- !pvp / !duel: ✅
- !accept: ✅

### Adventure System: ✅ / ❌
- !adventure: ✅
- !save: ✅

### Moderator Tools: ✅ / ❌
- !giveggs: ✅
- !takeggs: ✅
- !resetuser: ✅
- !ecobalance: ✅

### Issues Found:
1. [Description]
2. [Description]

### Notes:
[Any additional observations]
```

---

**Version:** 1.0
**Last Updated:** 2025-12-31
