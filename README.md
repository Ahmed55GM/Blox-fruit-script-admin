print("Hi")
local adminCommands = {}
local admins = {"ninjaman32352"} 
adminCommands.commands = {
  ["fly"] = function(player)
    player.Character.Humanoid.Fly = not player.Character.Humanoid.Fly
  end,
  ["god"] = function(player)
    player.Character.Humanoid.MaxHealth = math.huge
    player.Character.Humanoid.Health = math.huge
  end,
  ["maxlevel"] = function(player)
    player.leaderstats.Level.Value = 2600
  end,
  ["inflevel"] = function(player)
    player.leaderstats.Level.Value = 99999999
    player.leaderstats.XP.Value = 9999999999999
    end
    ["maxfruit"] = function(player)
    for _, fruit in pairs(game.ReplicatedStorage.Fruits:GetChildren()) do
      local fruitInstance = Instance.new("Tool")
      fruitInstance.Name = fruit.Name
      fruitInstance.Parent = player.Backpack
      local fruitInstance2 = fruit:Clone()
      fruitInstance2.Parent = player.Character
    end
  end,
  ["roll"] = function(player)
    local exclusiveFruits = {
      "Dragon Fruit (East)",
      "Dragon Fruit (West)",
      "Yeti Fruit",
      "Kitsune Fruit"
    }
    local randomFruitName = exclusiveFruits[math.random(1, #exclusiveFruits)]
    local fruitInstance = game.ReplicatedStorage.Fruits:FindFirstChild(randomFruitName)
    local fruitTool = Instance.new("Tool")
    fruitTool.Name = randomFruitName
    fruitTool:Clone().Parent = player.Backpack
    game.Studio.Chat:Chat(player.Name .. " rolled a " .. randomFruitName)
  end,
["tp"] = function(player, msg)
    local target = game.Players:FindFirstChild(msg:split(" ")[2])
    if target then
      player.Character.HumanoidRootPart.CFrame = target.Character.HumanoidRootPart.CFrame
    end
  end,
  ["bring"] = function(player, msg)
    local target = game.Players:FindFirstChild(msg:split(" ")[2])
    if target then
      target.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
    end
  end,
  ["kill"] = function(player, msg)
    local target = game.Players:FindFirstChild(msg:split(" ")[2])
    if target then
      target.Character.Humanoid.Health = 0
    end
  end,
 
game:GetService("Players").PlayerAdded:Connect(function(player)
  player.Chatted:Connect(function(msg)
    if admins[player.Name:lower()] then
      local cmd = msg:lower():split(" ")[1]:sub(1,1) == "/" and msg:lower():split(" ")[1]:sub(2)

  if adminCommands.commands[cmd] then
        if cmd == "tp" or cmd == "bring" or cmd == "kill" then
          adminCommands.commands[cmd](player, msg)
        else
          adminCommands.commands[cmd](player)
        end
      end
    end
  end)
end)
``
