# 🎉 PartyModule
- PartyModule is a way to simplify the creation of a party system in your roblox game.
- You can add/remove players, teleport them to another place (with optional teleport data) and more!

# 📘 Basic Documentation
## Party.new(name: string, players: {[number]: Player}?, information: {[any]: any}?, owner: Player?, playerLimit: number?, password: string?, visible: boolean?) -> Party
- Creates a new party object with a name, players (optional) and information. (also optional)
- information can be used to store extra data on your party. (for you to compare, do operations...)
- players, playerLimit and owner are essential but not required, while password and visible is completely optional.
- The party object's structure will be like this:

```
    Name: string,
	  Players: {[number]: Player},
	  Information: {[any]: any},
	  Owner: Player,
	  PartyId: string,
	  Password: string?,
	  PlayerLimit: number?,
	  Visible: boolean,
```

## Party.isPlayerInParty(player: Player, party: Party) -> boolean
- Checks if the provided player is in a party.
- When 'party' is provided, it will only check that party.

## Party.getPartyFromPlayer(player: Player) -> Party?
- Returns the party that the player is in.
- It will return **nil** if the player isn't in a party

## Party.findParty(partyId: string) -> Party?
- Returns the party via the provided partyId.
- Returns **nil** if it was not found.

## Party:AddPlayer(player: Player)
- Adds a player to the party object.

## Party:RemovePlayer(player: Player)
- Removes a player to the party object. (wow)

## Party:Teleport(placeId: number)
- Teleports all the players inside of the party to a place with its place id.
- Uses SafeTeleport to ensure everyone is teleported regardless of poor network conditions or other errors.
- The party is destroyed after this function is called.

## Party:Edit(contents: {})
- Edits the party contents.
[⚠️] **Try not to edit essential data unless you really need to. (partyId and functions)**

## Party:EligibleToJoin(player: Player, password: string?) -> boolean
- Checks if the player is able to join the party by checking the password, the playerLimit and if the player is in a party.
- 'password' is optional (will be required if the party has a password)

## Party:Destroy()
- Destroys the party object, making it unusable.

# 📄 Example Usage
```
local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local PartyModule = require(script.PartyModule) -- this path may be different for you

Players.PlayerAdded:Connect(function(player: Player)
  local newParty = PartyModule.new(`{player.DisplayName}'s party`, {player), {Mode = "Easy"})
end)
```

# ➕ Extra
- This is my first time using OOP and there may be better modules out there, I am just trying my best! :D
- If you have anything to suggest or report, you can open an issue for it!
