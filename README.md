# Roblox Carry System

A professional multiplayer carry/piggyback system for Roblox with real-time animation synchronization.

## Features

- **Multi-Player Carrying**: Carry up to 50 players simultaneously with automatic slot management
- **Animation Sync**: Real-time animation synchronization between players
- **Modern UI**: Clean, responsive interface supporting both desktop and mobile
- **Friend Integration**: Quick add-friend functionality from carry menu
- **Smart Detection**: Click-to-carry with distance validation
- **Rate Limiting**: Built-in anti-spam and request management
- **Auto-Transfer**: Passengers automatically transfer when carrier is carried

## Installation

### 1. Remote Setup (Run First)

Create a **Script** in `ServerScriptService`:
- Name: `0_RemoteSetup`
- Paste the RemoteEvent setup code
- This creates required RemoteEvents: `CarryRemote`, `Sync`, `Unsync`

### 2. Server Scripts

Place in `ServerScriptService`:
- `CarryConfig` (ModuleScript)
- `CarrySystemServer` (Script)
- `AnimationSyncConfig` (ModuleScript)
- `AnimationSyncServer` (Script)

### 3. Client Script

Place in `StarterPlayer` → `StarterPlayerScripts`:
- `CarrySystemClient` (LocalScript)

## Configuration

### CarryConfig.lua

```
Config.PENDING_TIMEOUT = 8        -- Request timeout (seconds)
Config.MAX_DISTANCE = 20          -- Max carry distance (studs)
Config.MAX_CARRY = 50             -- Max players to carry
Config.RATE_LIMIT_COUNT = 3       -- Max requests per window
Config.RATE_LIMIT_WINDOW = 5      -- Rate limit window (seconds)
```

### AnimationSyncConfig.lua

```
-- Ignored animation priorities
Config.IGNORED_ANIMATION_PRIORITIES = {
    Enum.AnimationPriority.Core,
}

-- Ignored animation names
Config.IGNORED_ANIMATION_NAMES = {
    "running", "swimming", "jumping", "walking"
}
```

## Usage

### Carrying Players

1. Click on another player to open carry menu
2. Click "Carry" button
3. Target player accepts/declines request
4. Use navigation arrows to switch between carried players
5. Click "Drop" to release current player

### Animation Sync

1. Open carry menu on target player
2. Click "Sync" button
3. Your animations will mirror theirs in real-time
4. Click "Unsync" to stop synchronization

### Controls

- **Desktop**: Click players to interact
- **Mobile**: Tap players to interact
- **Get Down**: Click button while being carried

## Architecture

### Server Components

**CarrySystemServer**
- State management for carry relationships
- Physics manipulation and weld management
- Distance monitoring and auto-detach
- Passenger transfer system
- Rate limiting and validation

**AnimationSyncServer**
- Heartbeat-based sync for minimal delay
- Animation filtering by priority/name
- Automatic cleanup on death/disconnect

### Client Components

**CarrySystemClient**
- Modern UI with animations and glow effects
- Click/touch detection with raycast
- Friend system integration
- State synchronization on respawn

## Technical Details

### Slot Formation

Players are positioned in vertical stack behind carrier:
- Base offset: 1.6 studs
- Spacing: 1.1 studs per slot
- Progressive elevation for visibility
- Automatic reindexing on add/remove

### Physics Management

- Carried players become massless
- Collision disabled for carried players
- WeldConstraints for stable attachment
- Saved states restored on release

### Performance

- Optimized sync loop using Heartbeat
- Debounced input handling
- Efficient state queries
- Automatic cleanup on player removal

## Animation IDs

Default animations (customizable):
- Sit R15: `86456460001706`
- Sit R6: `92641970583807`
- Carry R15: `103977242672051`
- Carry R6: `127460005242268`

## Troubleshooting

**Players can't carry each other**
- Verify RemoteEvents exist in ReplicatedStorage
- Check server console for errors
- Ensure scripts are in correct locations

**Animations not playing**
- Verify animation IDs are valid
- Check animation ownership/permissions
- Ensure Animator exists in Humanoid

**UI not appearing**
- Check ResetOnSpawn is false on ScreenGui
- Verify client script is in StarterPlayerScripts
- Check for GUI-related errors in client console

## Credits

**Author**: ItoRenz00  
**Version**: 1.0  
**License**: Free to use and modify

## Support

For issues or questions, check:
- Server console for server-side errors
- Client console (F9) for client-side errors
- Ensure all scripts are properly named and located
```
