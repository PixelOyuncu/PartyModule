# <img width="32" height="32" alt="PartyModule" src="https://github.com/user-attachments/assets/47ffaf63-a475-43ae-9f41-671257b27840"/> PartyModule

- PartyModule is a way to simplify the creation of a party system for your roblox ~~game~~ ✨ **EXPERIENCE**.
- You can add/remove players, teleport them to another place (with optional teleport data) and more!

# ❓ Installation / Usage
- **1.** Install the latest version in releases tab.
- **2.** Drag the `.rbxm` file to Roblox Studio
- **3.** Place it under ServerScriptService or under a script
- [⚠️] **Do not put this module on ReplicatedStorage or on a place the players can access!**

# 📘 Basic Documentation
## Party.new(name: string, players: {[number]: Player}?, information: {[any]: any}?, owner: Player?, playerLimit: number?, password: string?, visible: boolean?) -> Party
- Creates a new party object with a name, players (optional) and information. (also optional)
- information can be used to store extra data on your party. (for you to compare, do operations...)
- players, playerLimit and owner are essential but not required, while password and visible is completely optional.
- The party object's structure will be like this:

```lua
    Name: string,
	  Players: {[number]: Player},
	  Information: {[any]: any},
	  Owner: Player,
	  PartyId: string,
	  Password: string?,
	  PlayerLimit: number?,
	  Visible: boolean,
```
## Party.getParties(showHidden: boolean?) -> {[number]: Party}
- Returns the parties that are available.
- Use the 'showHidden' to show non-visible parties.

## Party.isPlayerInParty(player: Player, party: Party) -> boolean
- Checks if the provided player is in a party.
- When 'party' is provided, it will only check that party.

## Party.getPartyFromPlayer(player: Player) -> Party?
- Returns the party that the player is in.
- It will return **nil** if the player isn't in a party

## Party.findParty(partyId: string) -> Party?
- Returns the party via the provided partyId.
- Returns **nil** if it was not found.

## Party:AddPlayer(player: Player, bypassLimit: boolean?)
- Adds a player to the party object.
- You can use the optional 'bypassLimit' to bypass the player limit when adding players.

## Party:RemovePlayer(player: Player)
- Removes a player to the party object.
- If the player is the owner, the ownership will be given to a random person in the party.
- If the party contains 0 player after the player leaves, it will automatically be removed.

## Party:Teleport(placeId: number)
- Teleports all the players inside of the party to a place with its place id.
- Uses SafeTeleport to ensure everyone is teleported regardless of poor network conditions or other errors.
- The party is destroyed after this function is called.

## Party:Edit(contents: {})
- Edits the party contents.
- [⚠️] **Try not to edit essential data unless you really need to. (partyId and functions)**

## Party:EligibleToJoin(player: Player, password: string?) -> boolean
- Checks if the player is able to join the party by checking the password, the playerLimit and if the player is in a party.
- 'password' is optional (will be required if the party has a password)

## Party:Destroy()
- Destroys the party object, making it unusable.

# 📄 Example Usage
```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local PartyModule = require(script.PartyModule) -- the path of the module

ReplicatedStorage.Functions.CreateParty.OnServerInvoke = function(player)
	local playerInParty = PartyModule.isPlayerInParty(player) -- check if player is already in a party
	if playerInParty then return end
	
	local newParty = PartyModule.new(`{player.DisplayName}'s party`, {player}, nil, player)
end

ReplicatedStorage.Functions.JoinParty.OnServerInvoke = function(player, partyId)
	local party = PartyModule.findParty(partyId)
	if party then
		party:AddPlayer(player)
	end
end

ReplicatedStorage.Functions.LeaveParty.OnServerInvoke = function(player)
	local party = PartyModule.getPartyFromPlayer(player)
	if party then
		party:RemovePlayer(player)
	end
end

ReplicatedStorage.Functions.GetParties.OnServerInvoke = function(player)
	return PartyModule.getParties(false) -- hide the non-visible parties from the player
end
```

# ➕ Extra
- This is my first time using OOP and there may be better modules out there, I am just trying my best! :D
- If you have anything to suggest or report, you can open an issue for it!
