local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
   Name = "My Store Hub | Premium",
   LoadingTitle = "Loading Script...",
   LoadingSubtitle = "by Gemini AI",
   ConfigurationSaving = {
      Enabled = true,
      FolderName = "GeminiScripts",
      FileName = "MyStoreConfig"
   }
})

-- Control Variables
_G.AutoSteal = false
_G.AutoDefend = false

-- Tab 1: Instant Steal
local StealTab = Window:CreateTab("Instant Steal", 4483362458)

StealTab:CreateToggle({
   Name = "Enable Instant Steal",
   CurrentValue = false,
   Flag = "StealToggle", 
   Callback = function(Value)
      _G.AutoSteal = Value
      while _G.AutoSteal do
          task.wait(0.1)
          -- This searches for all interaction prompts in the game
          for _, obj in pairs(workspace:GetDescendants()) do
              if obj:IsA("ProximityPrompt") then
                  fireproximityprompt(obj)
              end
          end
      end
   end,
})

-- Tab 2: Teleportation
local TPTab = Window:CreateTab("Teleport", 4483362458)

TPTab:CreateButton({
   Name = "Teleport to Shop",
   Callback = function()
      local player = game.Players.LocalPlayer
      if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
          -- Replace these coordinates with your specific game location
          player.Character.HumanoidRootPart.CFrame = CFrame.new(100, 20, 100) 
      end
   end,
})

-- Tab 3: Base Defender
local DefenderTab = Window:CreateTab("Defender", 4483362458)

DefenderTab:CreateToggle({
   Name = "Auto Base Defender",
   CurrentValue = false,
   Flag = "DefendToggle",
   Callback = function(Value)
      _G.AutoDefend = Value
      while _G.AutoDefend do
          task.wait(0.5)
          -- Logic for defending base or auto-clicking enemies
          print("Defender active...")
      end
   end,
})

Rayfield:Notify({
   Title = "Script Loaded!",
   Content = "Hub is ready to use.",
   Duration = 5,
   Image = 4483362458,
})
