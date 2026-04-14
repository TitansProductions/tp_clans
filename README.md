# Commands

- @param [source] : The online Player ID. 

| Command                                    | Ace Permission                | Description                                                                   | Console / TXAdmin Console Support |
|--------------------------------------------|-------------------------------|-------------------------------------------------------------------------------|-----------------------------------|
| createclan [source]                        | tp_clans.createclan           | Perform this command to create a new clan for a target player.                | No |
| transferclan [clanId] [source]             | tp_clans.transfer             | Perform this command to transfer the ownership of a clan to another player.   | Yes |
| disbandclan [clanId]                       | tp_clans.disband              | Perform this command to disband a clan (remove) permanently.                  | Yes |
| resetclandailymissions [clanId]            | tp_clans.resetdailymissions   | Perform this command to transfer the ownership of a clan to another player.   | Yes |
| resetclanweeklymissions [clanId]           | tp_clans.resetweeklymissions  | Adds extra inventory weight capacity on the selected user.                    | Yes |

- The ace permission: `tp_clans.all` grants permissions to all commands.

# Development API

## CLIENT:

### Exports

API Getter Function

```lua
local ClansAPI = exports.tp_clans:getAPI()
```

1. Get player data.

```lua
--- @return table
local PlayerData = ClansAPI.GetPlayerData()

--- @param PlayerData.ClanId return integer
--- @param PlayerData.IsLoaded return boolean
--- @param PlayerData.Clans return table
--- @param PlayerData.Teritories return table
--- @param PlayerData.SourceId return integer
--- @param PlayerData.Identifier return string
--- @param PlayerData.CharIdentifier return integer
--- @param PlayerData.CurrentDay return string
--- @param PlayerData.IsBusy return boolean
```

2. Get player raiding state (If player is raiding)

```lua
--- @return boolean
local isPlayerRaiding = ClansAPI.IsPlayerRaiding()
```

3. Get player raiding clan id.

```lua
--- @return integer
local raidedClanId = ClansAPI.GetRaidingClanId()
```

4. Get player clan leadership state (if the player is the leader of the clan)

```lua
--- @return boolean
local isLeader = ClansAPI.IsPlayerClanLeader()
```

5. Get clan data

```lua
-- @return table
local ClanData = PlayerData.Clans[PlayerData.ClanId]

--- @param ClanData.coords return table
--- @param ClanData.furnitures return table
--- @param ClanData.raids_history return table
--- @param ClanData.members return table
--- @param ClanData.notifications return table
--- @param ClanData.alliances return table
--- @param ClanData.identifier return string
--- @param ClanData.charidentifier return integer
--- @param ClanData.name return string
--- @param ClanData.id return integer
--- @param ClanData.ledger return integer
--- @param ClanData.upgrade return integer
--- @param ClanData.level return integer
--- @param ClanData.level_experience return integer
```

### Events

1. Send an advanced notification to the desired clan.

```lua

-- @param message : requires a string (the notification message)
-- @param notificationType : requires a string (success, info, warning)
-- @param isImportant : requires an integer value (0 = not important, 1 = important )
local data = {
    message = message, 
    type = notificationType, 
    important = isImportant,
}

TriggerServerEvent('tp_clans:server:notifications:send', clanId, data) -- client > server
```

2. Use any desired code when a mission has been successfully finished (weekly missions only). This event is triggered for all the clan members who are online.

```lua
RegisterNetEvent("tp_clans:client:missions:mission_success")
AddEventHandler("tp_clans:client:missions:mission_success", function(missionType)
    -- todo anything
end)
```

## SERVER:

### Exports

API Getter Function

```lua
local ClansAPI = exports.tp_clans:getAPI()
```

1. Get all clans

```lua
--- @return table.
local Clans = ClansAPI.GetClans()
```

3. Get clan data by clan id.
   
```lua
-- @param clanId : requires an integer.
local ClanData = ClansAPI.GetClanData(clanId)

--- @param ClanData.coords return table
--- @param ClanData.furnitures return table
--- @param ClanData.raids_history return table
--- @param ClanData.members return table
--- @param ClanData.notifications return table
--- @param ClanData.alliances return table
--- @param ClanData.identifier return string
--- @param ClanData.charidentifier return integer
--- @param ClanData.name return string
--- @param ClanData.id return integer
--- @param ClanData.ledger return integer
--- @param ClanData.upgrade return integer
--- @param ClanData.level return integer
--- @param ClanData.level_experience return integer

```

3. Get player clan id (By Source)

```lua
-- @param source : requires an integer (player online id)
local ClanId = ClansAPI.GetPlayerClanId(source)

--- @param ClanId return 0 if there is no clan
```

4. Get player clan id (By Identifiers)

```lua
-- @param identifier : requires a string (the player steam hex)
-- @param charIdentifier : requires an integer (the player character id)
local ClanId = ClansAPI.GetPlayerClanIdOffline(identifier, charIdentifier)

--- @param ClanId return 0 if there is no clan
```

5. Kick a player from a clan (Online - By Source)

```lua
-- @param clanId : requires an integer.
-- @param source : requires an integer (player online id)
ClansAPI.KickPlayerClanMember(clanId, source)
```

6. Kick a player from a clan (Offline - By Identifiers)

```lua
-- @param clanId : requires an integer.
-- @param identifier : requires a string (the player steam hex)
-- @param charIdentifier : requires an integer (the player character id)
ClansAPI.KickPlayerClanMemberOffline(clanId, identifier, charIdentifier)
```

7. Add a new clan member(s).

```lua
-- @param clanId : requires an integer.
-- @param source : requires an integer (player online id)
ClansAPI.AddPlayerClanMember(clanId, source)
```

8. Disband a clan by its id.

```lua
-- @param clanId : requires an integer.
ClansAPI.DisbandClanById(clanId)
```

9. Delete a clan by its id.

```lua
-- @param clanId : requires an integer.
ClansAPI.DeleteClanById(clanId)
```

10. Add clan level

```lua
-- @param clanId : requires an integer.
-- @param level : requires an integer
ClansAPI.AddLevel(clanId, level)
```

11. Add clan level experience

```lua
-- @param clanId : requires an integer.
-- @param experienece : requires an integer (max is 10000 to get a level)
ClansAPI.AddLevelExperience(clanId, experienece)
```

12. Check if a clan mission is active.

```lua
-- @param clanId : requires an integer.
-- @param missionName : requires a string (a mission name, either a custom one or existing one, ex: 'CRAYFISH')
local hasActiveMission, missionData = ClansAPI.HasClanMissionActiveByName(clanId, missionName)
```

13. Decrease the required value if a clan mission is active **(THIS IS ONLY FOR DAILY MISSIONS)**

```lua
local ClansAPI = exports.tp_clans:getAPI() -- example
local clanId   = ClansAPI.GetPlayerClanId(source) -- example

if clanId ~= 0 then -- if clanId equals to 0, it means the player does not belong to any clan.
    -- @param clanId : requires an integer.
    -- @param missionName : requires a string (a mission name, either a custom one or existing one, ex: 'CRAYFISH')
    local hasActiveMission, missionData = ClansAPI.HasClanMissionActiveByName(clanId, missionName)

    -- @param decreaseAmount : requires an integer (decreaseAmount is the input value that you want to decrease from a daily mission, for example, if a player must catch (5) crayfishes, you can set the value to `1` so 4 crayfish catches will remain to do).
    if hasActiveMission then 
        ClansAPI.DecreaseClanMissionRequiredValueByName(clanId, missionName, decreaseAmount)
    end
end

```

### Events

1. Send an advanced notification to the desired clan.

```lua

-- @param message : requires a string (the notification message)
-- @param notificationType : requires a string (success, info, warning)
-- @param isImportant : requires an integer value (0 = not important, 1 = important )
local data = {
    message = message, 
    type = notificationType, 
    important = isImportant,
}

TriggerEvent('tp_clans:server:notifications:send', clanId, data) -- server > server
```
