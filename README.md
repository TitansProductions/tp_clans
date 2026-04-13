## Commands

- @param [source] : The online Player ID. 

| Command                                    | Ace Permission                | Description                                                                   | Console / TXAdmin Console Support |
|--------------------------------------------|-------------------------------|-------------------------------------------------------------------------------|-----------------------------------|
| createclan [source]                        | tp_clans.createclan           | Perform this command to create a new clan for a target player.                | No |
| transferclan [clanId] [source]             | tp_clans.transfer             | Perform this command to transfer the ownership of a clan to another player.   | Yes |
| disbandclan [clanId]                       | tp_clans.disband              | Perform this command to disband a clan (remove) permanently.                  | Yes |
| resetclandailymissions [clanId]            | tp_clans.resetdailymissions   | Perform this command to transfer the ownership of a clan to another player.   | Yes |
| resetclanweeklymissions [clanId]           | tp_clans.resetweeklymissions  | Adds extra inventory weight capacity on the selected user.                    | Yes |

- The ace permission: `tp_clans.all` grants permissions to all commands.

## Development API

### CLIENT:

API Getter Function

```lua
local ClansAPI = exports.tp_clans:getAPI()
```


1. Get Player Data

```lua
--- @return table
local PlayerData = ClansAPI.GetPlayerData()

--- @param PlayerData.ClanId return integer
--- @param PlayerData.IsLoaded return boolean
--- @param PlayerData.Clans return table

-- In case you want to retrive a Clan Data:

-- @return table
local ClanData = PlayerData.Clans[PlayerData.ClanId]

--- @param ClanData.coords return table
--- @param ClanData.furnitures return table
--- @param ClanData.raids_history return table
--- @param ClanData.members return table
--- @param ClanData.identifier return string
--- @param ClanData.charidentifier return integer
```

2. Get Player Raiding State (If player is raiding)

```lua
--- @return boolean
local isPlayerRaiding = ClansAPI.IsPlayerRaiding()
```

3. Get Player Raiding Clan Id

```lua
--- @return integer
local raidedClanId = ClansAPI.GetRaidingClanId()
```

4. Get Player Clan Leadership State (if the player is the leader of the clan)

```lua
--- @return boolean
local isLeader = ClansAPI.IsPlayerClanLeader()
```


