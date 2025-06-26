local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- GUI container
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "DraggableMenuGui"
screenGui.ResetOnSpawn = false
screenGui.Parent = playerGui

-- Tip Label (nápis nahoře)
local tipLabel = Instance.new("TextLabel")
tipLabel.Size = UDim2.new(1, 0, 0, 30)
tipLabel.Position = UDim2.new(0, 0, 0, 0)
tipLabel.BackgroundTransparency = 1
tipLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
tipLabel.Font = Enum.Font.SourceSansBold
tipLabel.TextSize = 22
tipLabel.Text = ""
tipLabel.Parent = screenGui

local function showTip(message, duration)
	tipLabel.Text = message
	task.delay(duration, function()
		tipLabel.Text = ""
	end)
end

-- ✅ Zobrazí zprávu po spuštění
showTip("Successfully loaded", 3)

-- Hlavní menu (frame)
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 250, 0, 375)
mainFrame.Position = UDim2.new(0.5, -125, 0.5, -150)
mainFrame.BackgroundColor3 = Color3.fromRGB(138, 146, 156)
mainFrame.BorderSizePixel = 0
mainFrame.Active = true
mainFrame.Draggable = true
mainFrame.Parent = screenGui

-- Zavírací tlačítko v pravém horním rohu menu
local closeButton = Instance.new("TextButton")
closeButton.Size = UDim2.new(0, 30, 0, 30)
closeButton.Position = UDim2.new(1, -30, 0, 0)
closeButton.BackgroundColor3 = Color3.fromRGB(150, 0, 0)
closeButton.Text = "X"
closeButton.TextColor3 = Color3.new(1, 1, 1)
closeButton.Font = Enum.Font.SourceSansBold
closeButton.TextSize = 18
closeButton.Parent = mainFrame

closeButton.MouseButton1Click:Connect(function()
	mainFrame.Visible = false
	showTip("Press Right Shift to open", 3)
end)

-- Název panelu
local titleLabel = Instance.new("TextLabel")
titleLabel.Size = UDim2.new(1, 0, 0, 30)
titleLabel.Position = UDim2.new(0, 0, 0, 0)
titleLabel.BackgroundColor3 = Color3.fromRGB(129, 133, 138)
titleLabel.Text = "Script hub"
titleLabel.Font = Enum.Font.SourceSansBold
titleLabel.TextSize = 20
titleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
titleLabel.Parent = mainFrame

-- Layout pro tlačítka
local buttonHolder = Instance.new("Frame")
buttonHolder.Size = UDim2.new(1, 0, 1, 300)
buttonHolder.Position = UDim2.new(0, 0, 0, 30)
buttonHolder.BackgroundTransparency = 1
buttonHolder.Parent = mainFrame

local layout = Instance.new("UIListLayout")
layout.Padding = UDim.new(0, 10)
layout.FillDirection = Enum.FillDirection.Vertical
layout.HorizontalAlignment = Enum.HorizontalAlignment.Center
layout.VerticalAlignment = Enum.VerticalAlignment.Top
layout.SortOrder = Enum.SortOrder.LayoutOrder
layout.Parent = buttonHolder

-- Funkce pro vytvoření tlačítek
local function createButton(text, callback)
	local button = Instance.new("TextButton")
	button.Size = UDim2.new(0, 200, 0, 40)
	button.BackgroundColor3 = Color3.fromRGB(57, 60, 64)
	button.TextColor3 = Color3.fromRGB(255, 255, 255)
	button.Text = text
	button.Font = Enum.Font.SourceSans
	button.TextSize = 18
	button.AutoButtonColor = true
	button.Parent = buttonHolder

	button.MouseButton1Click:Connect(callback)
end

createButton("Wall hop script", function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/lyraEz/lol/refs/heads/main/loaders/NewWallhop.lua"))()
end)

createButton("Zephion for all games", function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/blackowl1231/ZYPHERION/refs/heads/main/main.lua"))()
end)

createButton("18+🔞", function()
	loadstring(game:HttpGet("https://pastebin.com/raw/FWwdST5Y"))()
end)

createButton("LALOL hub backdoor", function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/Its-LALOL/LALOL-Hub/main/Backdoor-Scanner/script"))()
end)

createButton("Van script", function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/vit3g13/dsdsd/refs/heads/main/README.md"))()
end)

createButton("Close This", function()
	mainFrame.Visible = guiVisible
	showTip("Press Right Shift to open", 3)
end)

-- Right Shift pro toggle menu
local guiVisible = true

UserInputService.InputBegan:Connect(function(input, gameProcessed)
	if input.KeyCode == Enum.KeyCode.RightShift and not gameProcessed then
		guiVisible = not guiVisible
		mainFrame.Visible = guiVisible
	end
end)
