# 🎉 PartyModule
- PartyModule is a way to simplify the creation of a party system in your roblox game.
- You can add/remove players, teleport them to another place (with optional teleport data) and other essentials function you can use!

# 📘 Basic Documentation
## Party.new(name: string, players: {[number]: Player}, information: {[any]: any}?) -> Party
- Creates a new party object with a name, players (optional) and information (also optional)
- information will be used to store teleport data when Party:Teleport() is called, leave it empty if you do not want to store teleport data.

## Party:AddPlayer(player: Player)
- Adds a player to the party object.

## Party:RemovePlayer(player: Player)
- Removes a player to the party object. (wow)

## Party:Teleport(placeId: number)
- Teleports all the players inside of the party to a place with its place id.
- Uses SafeTeleport to ensure everyone is teleported regardless of poor network conditions or other errors
- The party is destroyed after this function is called.

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
