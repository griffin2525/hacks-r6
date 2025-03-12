local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

-- Services
local Players = game:GetService("Players")
local Lighting = game:GetService("Lighting")

local Window = Rayfield:CreateWindow({
	Name = "Operations: Siege",
	LoadingTitle = "Operations: Siege | Free Script",
	LoadingSubtitle = "By SirSammy",
	ConfigurationSaving = {
		Enabled = true,
		FolderName = nil, -- Create a custom folder for your hub/game
		FileName = "Operations: Siege"
	},
	Discord = {
		Enabled = false,
		Invite = "", -- The Discord invite code, do not include discord.gg/. E.g. discord.gg/ABCD would be ABCD
		RememberJoins = true -- Set this to false to make them join the discord every time they load it up
	},
	KeySystem = false, -- Set this to true to use our key system
	KeySettings = {
		Title = "",
		Subtitle = "",
		Note = "",
		FileName = "", -- It is recommended to use something unique as other scripts using Rayfield may overwrite your key file
		SaveKey = true, -- The user's key will be saved, but if you change the key, they will be unable to use your script
		GrabKeyFromSite = false, -- If this is true, set Key below to the RAW site you would like Rayfield to get the key from
		Key = {""} -- List of keys that will be accepted by the system, can be RAW file links (pastebin, github etc) or simple strings ("hello","key22")
	}
})

-- Main Tab

local Main_Tab = Window:CreateTab("Main", 4483362458)

local Main_ObjectivesAlwaysVisible = false
local Main_NoClipDelay = 0.2
local Main_NoClipBarricades = false
local Main_NoClipWalls = false

-- Main | Main Section

local Section = Main_Tab:CreateSection("Main")

local Toggle = Main_Tab:CreateToggle({Name = "Objectives Always Visible", CurrentValue = false, Flag = "ObjectivesAlwaysVisible_Main", Callback = function(Value) Main_ObjectivesAlwaysVisible = Value ObjectivesAlwaysVisible_Main() local Text = "" if Value == true then Text = "On" else Text = "Off" end Rayfield:Notify({Title = "Objectives Always Visible | Turned "..tostring(Text), Content = "Updated Script Settings", Duration = 3, Image = 4483362458})end})

-- Main | Blatant Section

local Section = Main_Tab:CreateSection("Blatant")

local Slider = Main_Tab:CreateSlider({Name = "No-Clip Delay", Range = {0.1, 2}, Increment = 0.1, Suffix = "Seconds", CurrentValue = 0.2, Flag = "NoClipDelay_Main", Callback = function(Value) Main_NoClipDelay = Value end})

local Toggle = Main_Tab:CreateToggle({Name = "No-Clip Barricades", CurrentValue = false, Flag = "NoClipBarricades_Main", Callback = function(Value) Main_NoClipBarricades = Value NoClipBarricades_Main() local Text = "" if Value == true then Text = "On" else Text = "Off" end Rayfield:Notify({Title = "No-Clip Barricades | Turned "..tostring(Text), Content = "Updated Script Settings", Duration = 3, Image = 4483362458})end})

local Toggle = Main_Tab:CreateToggle({Name = "No-Clip Walls", CurrentValue = false, Flag = "NoClipWalls_Main", Callback = function(Value) Main_NoClipWalls = Value NoClipWalls_Main() local Text = "" if Value == true then Text = "On" else Text = "Off" end Rayfield:Notify({Title = "No-Clip Walls | Turned "..tostring(Text), Content = "Updated Script Settings", Duration = 3, Image = 4483362458})end})

-- Esp Tab

local Esp_Tab = Window:CreateTab("Esp", 4483362458)

local Esp_Delay = 0.5
local Esp_Player = false local Esp_Player_Delay = 0.5 local Esp_Player_TeamCheck = false local Esp_Player_Color = Color3.fromRGB(255,0,0) local Esp_Player_Transparency = 0.5 local Esp_Player_Outline = false local Esp_Player_Outline_Color = Color3.fromRGB(255,255,255) local Esp_Player_Outline_Transparency = 0 local Player_Storage = Instance.new("Folder") Player_Storage.Parent = game.Workspace Player_Storage.Name = "Player_Storage"
local Esp_Drone = false local Esp_Drone_Color = Color3.fromRGB(255,0,0) local Esp_Drone_Transparency = 0.5 local Esp_Drone_Outline = false local Esp_Drone_Outline_Color = Color3.fromRGB(255,255,255) local Esp_Drone_Outline_Transparency = 0 local Drone_Storage = Instance.new("Folder") Drone_Storage.Parent = game.Workspace Drone_Storage.Name = "Drone_Storage"
local Esp_Camera = false local Esp_Camera_Color = Color3.fromRGB(0, 0, 55) local Esp_Camera_Transparency = 0.5 local Esp_Camera_Outline = false local Esp_Camera_Outline_Color = Color3.fromRGB(255,255,255) local Esp_Camera_Outline_Transparency = 0 local Camera_Storage = Instance.new("Folder") Camera_Storage.Parent = game.Workspace Camera_Storage.Name = "Camera_Storage"
local Esp_Gadget = false local Esp_Gadget_Color = Color3.fromRGB(255, 0, 0) local Esp_Gadget_Transparency = 0.5 local Esp_Gadget_Outline = false local Esp_Gadget_Outline_Color = Color3.fromRGB(255,255,255) local Esp_Gadget_Outline_Transparency = 0 local Gadget_Storage = Instance.new("Folder") Gadget_Storage.Parent = game.Workspace Gadget_Storage.Name = "Gadget_Storage"
local Esp_Doors = false local Doors_Storage = Instance.new("Folder") Doors_Storage.Parent = game.Workspace Doors_Storage.Name = "Doors_Storage"
local Esp_Walls = false local Walls_Storage = Instance.new("Folder") Walls_Storage.Parent = game.Workspace Walls_Storage.Name = "Walls_Storage"

-- Esp | Settings Section

local Section = Esp_Tab:CreateSection("Settings")

local Button = Esp_Tab:CreateButton({Name = "Esp Script Not Working?", Callback = function() Reminder_Esp() end})

local Slider = Esp_Tab:CreateSlider({Name = "Esp Delay", Range = {0.1, 3}, Increment = 0.1, Suffix = "Seconds", CurrentValue = 0.5, Flag = "Delay_Esp", Callback = function(Value) Esp_Delay = Value end})

-- Esp | Game Section

local Section = Esp_Tab:CreateSection("Game")

function Player_Esp() spawn(function() while Esp_Player == true do wait(Esp_Player_Delay) for i, v in pairs(Player_Storage:GetChildren()) do v:Destroy() end for i, Player in pairs(Players:GetChildren()) do if Player.Character and Player.Character:FindFirstChild("Humanoid") and Player.Character:FindFirstChild("Humanoid").Health ~= 0 then if Esp_Player_TeamCheck == true then if Player.TeamColor ~= Players.LocalPlayer.TeamColor then local Highlight = Instance.new("Highlight") Highlight.FillColor = Esp_Player_Color Highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop Highlight.FillTransparency = Esp_Player_Transparency Highlight.OutlineColor = Esp_Player_Outline_Color if Esp_Player_Outline == true then Highlight.OutlineTransparency = Esp_Player_Outline_Transparency else Highlight.OutlineTransparency = 1 end Highlight.Parent = Player_Storage  Highlight.Adornee = Player.Character end else local Highlight = Instance.new("Highlight") Highlight.FillColor = Esp_Player_Color Highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop Highlight.FillTransparency = Esp_Player_Transparency Highlight.OutlineColor = Esp_Player_Outline_Color if Esp_Player_Outline == true then Highlight.OutlineTransparency = Esp_Player_Outline_Transparency else Highlight.OutlineTransparency = 1 end Highlight.Parent = Player_Storage Highlight.Adornee = Player.Character end end  end end for i, v in pairs(Player_Storage:GetChildren()) do v:Destroy() end end) end

local Toggle = Esp_Tab:CreateToggle({Name = "Wall Esp | Not Recommended", CurrentValue = false, Flag = "Wall_Esp", Callback = function(Value) Esp_Walls = Value Walls_Esp() local Text = "" if Value == true then Text = "On" else Text = "Off" end Rayfield:Notify({Title = "Walls Esp | Turned "..tostring(Text), Content = "Updated Script Settings", Duration = 3, Image = 4483362458})end})

local Toggle = Esp_Tab:CreateToggle({Name = "Doors Esp | Not Recommended", CurrentValue = false, Flag = "Doors_Esp", Callback = function(Value) Esp_Doors = Value Doors_Esp() local Text = "" if Value == true then Text = "On" else Text = "Off" end Rayfield:Notify({Title = "Doors Esp | Turned "..tostring(Text), Content = "Updated Script Settings", Duration = 3, Image = 4483362458})end})

-- Esp | Player Section

local Section = Esp_Tab:CreateSection("Player Esp")

local Toggle = Esp_Tab:CreateToggle({Name = "Player Esp", CurrentValue = false, Flag = "Player_Esp", Callback = function(Value) Esp_Player = Value local Text = "" if Value == true then for i, Player in next, Players:GetPlayers() do Player_Esp(Player) end Text = "On" else Text = "Off" end Rayfield:Notify({Title = "Player Esp | Turned "..tostring(Text), Content = "Updated Script Settings", Duration = 3, Image = 4483362458})end})

local Slider = Esp_Tab:CreateSlider({Name = "Esp Delay", Range = {0.1, 5}, Increment = 0.1, Suffix = "Seconds", CurrentValue = 0.5, Flag = "Player_Delay_Esp", Callback = function(Value) Esp_Player_Delay = Value end})

local Toggle = Esp_Tab:CreateToggle({Name = "Team Check", CurrentValue = false, Flag = "Player_Esp_TeamCheck", Callback = function(Value) Esp_Player_TeamCheck = Value local Text = "" if Value == true then Text = "On" else Text = "Off" end Rayfield:Notify({Title = "Player Esp Team Check | Turned "..tostring(Text), Content = "Updated Script Settings", Duration = 3, Image = 4483362458})end})

local ColorPicker = Esp_Tab:CreateColorPicker({Name = "Esp Color", Color = Color3.fromRGB(255, 0, 0), Flag = "Player_Color_Esp", Callback = function(Value) Esp_Player_Color = Value end})

local Slider = Esp_Tab:CreateSlider({Name = "Esp Transparency", Range = {0, 0.9}, Increment = 0.1, Suffix = "Transparency", CurrentValue = 0.5, Flag = "Player_Transparency_Esp", Callback = function(Value) Esp_Player_Transparency = Value end})

local Toggle = Esp_Tab:CreateToggle({Name = "Esp Outlines", CurrentValue = true, Flag = "Player_Outlines_Esp", Callback = function(Value) Esp_Player_Outline = Value end})

local ColorPicker = Esp_Tab:CreateColorPicker({Name = "Esp Outline Color", Color = Color3.fromRGB(255, 255, 255), Flag = "Player_Outline_Color_Esp", Callback = function(Value) Esp_Player_Outline_Color = Value end})

local Slider = Esp_Tab:CreateSlider({Name = "Esp Outline Transparency", Range = {0, 0.9}, Increment = 0.1, Suffix = "Transparency", CurrentValue = 0, Flag = "Player_Outline_Transparency_Esp", Callback = function(Value) Esp_Player_Outline_Transparency = Value end})

-- Esp | Drone Section

local Section = Esp_Tab:CreateSection("Drone Esp")

local Toggle = Esp_Tab:CreateToggle({Name = "Drone Esp", CurrentValue = false, Flag = "Drone_Esp", Callback = function(Value) Drone_Esp() Esp_Drone = Value local Text = "" if Value == true then Text = "On" else Text = "Off" end Rayfield:Notify({Title = "Drone Esp | Turned "..tostring(Text), Content = "Updated Script Settings", Duration = 3, Image = 4483362458})end})

local ColorPicker = Esp_Tab:CreateColorPicker({Name = "Esp Color", Color = Color3.fromRGB(255, 0, 0), Flag = "Drone_Color_Esp", Callback = function(Value) Esp_Drone_Color = Value end})

local Slider = Esp_Tab:CreateSlider({Name = "Esp Transparency", Range = {0, 0.9}, Increment = 0.1, Suffix = "Transparency", CurrentValue = 0.5, Flag = "Drone_Transparency_Esp", Callback = function(Value) Esp_Drone_Transparency = Value end})

local Toggle = Esp_Tab:CreateToggle({Name = "Esp Outlines", CurrentValue = true, Flag = "Drone_Outlines_Esp", Callback = function(Value) Esp_Drone_Outline = Value end})

local ColorPicker = Esp_Tab:CreateColorPicker({Name = "Esp Outline Color", Color = Color3.fromRGB(255, 255, 255), Flag = "Drone_Outline_Color_Esp", Callback = function(Value) Esp_Drone_Outline_Color = Value end})

local Slider = Esp_Tab:CreateSlider({Name = "Esp Outline Transparency", Range = {0, 0.9}, Increment = 0.1, Suffix = "Transparency", CurrentValue = 0, Flag = "Drone_Outline_Transparency_Esp", Callback = function(Value) Esp_Drone_Outline_Transparency = Value end})

-- Esp | Camera Section

local Section = Esp_Tab:CreateSection("Camera Esp")

local Toggle = Esp_Tab:CreateToggle({Name = "Camera Esp", CurrentValue = false, Flag = "Camera_Esp", Callback = function(Value) Camera_Esp() Esp_Camera = Value local Text = "" if Value == true then Text = "On" else Text = "Off" end Rayfield:Notify({Title = "Camera Esp | Turned "..tostring(Text), Content = "Updated Script Settings", Duration = 3, Image = 4483362458})end})

local ColorPicker = Esp_Tab:CreateColorPicker({Name = "Esp Color", Color = Color3.fromRGB(0, 0, 55), Flag = "Camera_Color_Esp", Callback = function(Value) Esp_Camera_Color = Value end})

local Slider = Esp_Tab:CreateSlider({Name = "Esp Transparency", Range = {0, 0.9}, Increment = 0.1, Suffix = "Transparency", CurrentValue = 0.5, Flag = "Camera_Transparency_Esp", Callback = function(Value) Esp_Camera_Transparency = Value end})

local Toggle = Esp_Tab:CreateToggle({Name = "Esp Outlines", CurrentValue = true, Flag = "Camera_Outlines_Esp", Callback = function(Value) Esp_Camera_Outline = Value end})

local ColorPicker = Esp_Tab:CreateColorPicker({Name = "Esp Outline Color", Color = Color3.fromRGB(255, 255, 255), Flag = "Camera_Outline_Color_Esp", Callback = function(Value) Esp_Camera_Outline_Color = Value end})

local Slider = Esp_Tab:CreateSlider({Name = "Esp Outline Transparency", Range = {0, 0.9}, Increment = 0.1, Suffix = "Transparency", CurrentValue = 0, Flag = "Camera_Outline_Transparency_Esp", Callback = function(Value) Esp_Camera_Outline_Transparency = Value end})

-- Esp | Gadgets Section

local Section = Esp_Tab:CreateSection("Gadget Esp")

local Toggle = Esp_Tab:CreateToggle({Name = "Gadget Esp", CurrentValue = false, Flag = "Gadget_Esp", Callback = function(Value) Gadget_Esp() Esp_Gadget = Value local Text = "" if Value == true then Text = "On" else Text = "Off" end Rayfield:Notify({Title = "Gadget Esp | Turned "..tostring(Text), Content = "Updated Script Settings", Duration = 3, Image = 4483362458})end})

local ColorPicker = Esp_Tab:CreateColorPicker({Name = "Esp Color", Color = Color3.fromRGB(255, 0, 0), Flag = "Gadget_Color_Esp", Callback = function(Value) Esp_Gadget_Color = Value end})

local Slider = Esp_Tab:CreateSlider({Name = "Esp Transparency", Range = {0, 0.9}, Increment = 0.1, Suffix = "Transparency", CurrentValue = 0.5, Flag = "Gadget_Transparency_Esp", Callback = function(Value) Esp_Gadget_Transparency = Value end})

local Toggle = Esp_Tab:CreateToggle({Name = "Esp Outlines", CurrentValue = false, Flag = "Gadget_Outlines_Esp", Callback = function(Value) Esp_Gadget_Outline = Value end})

local ColorPicker = Esp_Tab:CreateColorPicker({Name = "Esp Outline Color", Color = Color3.fromRGB(255, 255, 255), Flag = "Gadget_Outline_Color_Esp", Callback = function(Value) Esp_Gadget_Outline_Color = Value end})

local Slider = Esp_Tab:CreateSlider({Name = "Esp Outline Transparency", Range = {0, 0.9}, Increment = 0.1, Suffix = "Transparency", CurrentValue = 0, Flag = "Gadget_Outline_Transparency_Esp", Callback = function(Value) Esp_Gadget_Outline_Transparency = Value end})


-- Lighting Tab

local Lighting_Tab = Window:CreateTab("Lighting", 4483362458)

local Lighting_NoShadows = false
local Lighting_SunRays = false
local Lighting_CameraCC = false
local Lighting_DroneCC = false
local Lighting_WinBlur = false
local Lighting_HurtBlur = false

-- Lighting | Main Section

local Section = Lighting_Tab:CreateSection("Main")

local Toggle = Lighting_Tab:CreateToggle({Name = "No Shadows", CurrentValue = false, Flag = "NoShadows_Lighting", Callback = function(Value) Lighting_NoShadows = Value NoShadows_Lighting() local Text = "" if Value == true then Text = "On" else Text = "Off" end Rayfield:Notify({Title = "No Shadows | Turned "..tostring(Text), Content = "Updated Script Settings", Duration = 3, Image = 4483362458})end})

-- Lighting | Effects Section

local Section = Lighting_Tab:CreateSection("Effects")

local Toggle = Lighting_Tab:CreateToggle({Name = "Disable Sun-Rays",  CurrentValue = false, Flag = "SunRays_Lighting", Callback = function(Value) SunRays_Lighting() Lighting_SunRays = Value local Text = "" if Value == true then Text = "Enabled" else Text = "Disabled" end Rayfield:Notify({Title = tostring(Text).." | Sun-Rays", Content = "Updated Script Settings", Duration = 3, Image = 4483362458})end})

local Toggle = Lighting_Tab:CreateToggle({Name = "Disable Camera Color Correction", CurrentValue = false, Flag = "CameraCC_Lighting", Callback = function(Value) CameraCC_Lighting() Lighting_CameraCC = Value local Text = "" if Value == true then Text = "Enabled" else Text = "Disabled" end Rayfield:Notify({Title = tostring(Text).." | Camera Color Correction", Content = "Updated Script Settings", Duration = 3, Image = 4483362458})end})

local Toggle = Lighting_Tab:CreateToggle({Name = "Disable Drone Color Correction", CurrentValue = false, Flag = "DroneCC_Lighting", Callback = function(Value) DroneCC_Lighting() Lighting_DroneCC = Value local Text = "" if Value == true then Text = "Enabled" else Text = "Disabled" end Rayfield:Notify({Title = tostring(Text).." | Drone Color Correction", Content = "Updated Script Settings", Duration = 3, Image = 4483362458})end})

local Toggle = Lighting_Tab:CreateToggle({Name = "Disable Win Blur", CurrentValue = false, Flag = "WinBlur_Lighting", Callback = function(Value) WinBlur_Lighting() Lighting_WinBlur = Value local Text = "" if Value == true then Text = "Enabled" else Text = "Disabled" end Rayfield:Notify({Title = tostring(Text).." | Win Blur", Content = "Updated Script Settings", Duration = 3, Image = 4483362458})end})

local Toggle = Lighting_Tab:CreateToggle({Name = "Disable Hurt Blur", CurrentValue = false, Flag = "HurtBlur_Lighting", Callback = function(Value) HurtBlur_Lighting() Lighting_HurtBlur = Value local Text = "" if Value == true then Text = "Enabled" else Text = "Disabled" end Rayfield:Notify({Title = tostring(Text).." | Hurt Blur", Content = "Updated Script Settings", Duration = 3, Image = 4483362458}) end})

-- Main | Functions

function ObjectivesAlwaysVisible_Main() spawn(function() while Main_ObjectivesAlwaysVisible == true do wait(2) for i, Objective in pairs(game.Workspace.Objective:GetChildren()) do if Objective.Name == "Bomb_A" or Objective.Name == "Bomb_B" then Objective.Center.Sinal.Enabled = true end end end end) end

function NoClipBarricades_Main() spawn(function() while Main_NoClipBarricades == true do wait(Main_NoClipDelay) for i, Barricade in pairs(game.Workspace.SE_Workspace.Doors:GetChildren()) do for i, Part in pairs(Barricade.Door:GetChildren()) do if Part:IsA("Part") then Part.CanCollide = false end end end end for i, Barricade in pairs(game.Workspace.SE_Workspace.Doors:GetChildren()) do for i, Part in pairs(Barricade.Door:GetChildren()) do if Part:IsA("Part") then Part.CanCollide = true end	end end end) end

function NoClipWalls_Main() spawn(function() while Main_NoClipWalls == true do wait(Main_NoClipDelay) for i, Wall in pairs(game.Workspace.SE_Workspace.Breach:GetChildren()) do if Wall.Name == "Reinforced" then for i, Part in pairs(Wall:GetChildren()) do if Part:IsA("Part") then Part.CanCollide = false end end else for i, Part in pairs(Wall.Destroyable:GetChildren()) do if Part:IsA("Part") then Part.CanCollide = false  end end end end end  for i, Wall in pairs(game.Workspace.SE_Workspace.Breach:GetChildren()) do if Wall.Name == "Reinforced" then for i, Part in pairs(Wall:GetChildren()) do if Part:IsA("Part") then Part.CanCollide = true end end else for i, Part in pairs(Wall.Destroyable:GetChildren()) do if Part:IsA("Part") then Part.CanCollide = true  end end end end end)  end

-- Esp | Functions

function Reminder_Esp()Rayfield:Notify({Title = "Esp Limit", Content = "Roblox Has A Set Adornee Limit (31 Highlights Max) | Use Less Esp Scripts!", Duration = 5, Image = 4483362458}) end

function Drone_Esp() spawn(function() while Esp_Drone == true do wait(Esp_Delay) for i, v in pairs(Drone_Storage:GetChildren()) do v:Destroy() end for i, v in pairs(game.Workspace.SE_Workspace.Drones:GetChildren()) do if v.Humanoid.Health ~= 0 then local Highlight = Instance.new("Highlight") Highlight.FillColor = Esp_Drone_Color Highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop Highlight.FillTransparency = Esp_Drone_Transparency Highlight.OutlineColor = Esp_Drone_Outline_Color if Esp_Drone_Outline == true then Highlight.OutlineTransparency = Esp_Drone_Outline_Transparency else Highlight.OutlineTransparency = 1 end Highlight.Parent = Drone_Storage Highlight.Adornee = v end end end for i, v in pairs(Drone_Storage:GetChildren()) do v:Destroy() end end) end

function Camera_Esp() spawn(function() while Esp_Camera == true do wait(Esp_Delay) for i, v in pairs(Camera_Storage:GetChildren()) do v:Destroy() end for i, v in pairs(game.Workspace.SE_Workspace.Cameras:GetChildren()) do if v.Humanoid.Health ~= 0 then local Highlight = Instance.new("Highlight") Highlight.FillColor = Esp_Camera_Color Highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop Highlight.FillTransparency = Esp_Camera_Transparency Highlight.OutlineColor = Esp_Camera_Outline_Color if Esp_Camera_Outline == true then Highlight.OutlineTransparency = Esp_Camera_Outline_Transparency else Highlight.OutlineTransparency = 1 end Highlight.Parent = Camera_Storage Highlight.Adornee = v end end end for i, v in pairs(Camera_Storage:GetChildren()) do v:Destroy() end end) end

function Gadget_Esp() spawn(function() while Esp_Gadget == true do wait(Esp_Delay) for i, v in pairs(Gadget_Storage:GetChildren()) do v:Destroy() end for i, v in pairs(game.Workspace.Gadgets:GetChildren()) do local Highlight = Instance.new("Highlight") Highlight.FillColor = Esp_Gadget_Color Highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop Highlight.FillTransparency = Esp_Gadget_Transparency Highlight.OutlineColor = Esp_Gadget_Outline_Color if Esp_Gadget_Outline == true then Highlight.OutlineTransparency = Esp_Gadget_Outline_Transparency else Highlight.OutlineTransparency = 1 end Highlight.Parent = Gadget_Storage Highlight.Adornee = v end end for i, v in pairs(Gadget_Storage:GetChildren()) do v:Destroy() end end) end

function Walls_Esp() spawn(function() while Esp_Walls == true do wait(Esp_Delay) for i, v in pairs(Walls_Storage:GetChildren()) do v:Destroy() end for i, v in pairs(game.Workspace.SE_Workspace.Breach:GetChildren()) do local Highlight = Instance.new("Highlight") Highlight.FillColor = Color3.fromRGB(255, 215, 215) Highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop Highlight.FillTransparency = 0.75 Highlight.OutlineColor = Color3.fromRGB(255, 255, 255) Highlight.OutlineTransparency = 1 Highlight.Parent = Walls_Storage Highlight.Adornee = v end end for i, v in pairs(Walls_Storage:GetChildren()) do v:Destroy() end end) end

function Doors_Esp() spawn(function() while Esp_Doors == true do wait(Esp_Delay) for i, v in pairs(Doors_Storage:GetChildren()) do v:Destroy() end for i, v in pairs(game.Workspace.SE_Workspace.Doors:GetChildren()) do local Highlight = Instance.new("Highlight") Highlight.FillColor = Color3.fromRGB(255, 155, 55) Highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop Highlight.FillTransparency = 0.75 Highlight.OutlineColor = Color3.fromRGB(255, 255, 255) Highlight.OutlineTransparency = 1 Highlight.Parent = Doors_Storage Highlight.Adornee = v end end for i, v in pairs(Doors_Storage:GetChildren()) do v:Destroy() end end) end

-- Lighting | Functions

function NoShadows_Lighting() if Lighting_NoShadows == true then Lighting.GlobalShadows = false else Lighting.GlobalShadows = true end end

function SunRays_Lighting() if Lighting_SunRays == true then Lighting.SunRays.Enabled = true else Lighting.SunRays.Enabled = false end end

function CameraCC_Lighting() if Lighting_CameraCC == true then Lighting.CameraCC.Brightness = 0 Lighting.CameraCC.Contrast = 0.25 Lighting.CameraCC.Saturation = -0.7 else Lighting.CameraCC.Brightness = 0 Lighting.CameraCC.Contrast = 0 Lighting.CameraCC.Saturation = 0 end end

function DroneCC_Lighting() if Lighting_DroneCC == true then Lighting.DroneCC.Brightness = 0 Lighting.DroneCC.Contrast = 0 Lighting.DroneCC.Saturation = -0.9 else Lighting.DroneCC.Brightness = 0 Lighting.DroneCC.Contrast = 0 Lighting.DroneCC.Saturation = 0 end end

function WinBlur_Lighting() if Lighting_WinBlur == true then Lighting.WinBlur.Enabled = true else Lighting.WinBlur.Enabled = false end end

function HurtBlur_Lighting() if Lighting_HurtBlur == true then Lighting.HurtBlur.Enabled = true else Lighting.HurtBlur.Enabled = false end end
