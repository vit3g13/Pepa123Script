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


loadstring(game:HttpGet('https://raw.githubusercontent.com/vit3g13/made-by-vit3g/refs/heads/main/README.md'))() 
showTip("Successfully loaded", 3)


-- Right Shift pro toggle menu
local guiVisible = true

-- Hlavní menu (frame)
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 250, 0, 375)
mainFrame.Position = UDim2.new(0.5, -125, 0.5, -150)
mainFrame.BackgroundColor3 = Color3.fromRGB(138, 146, 156)
mainFrame.BorderSizePixel = 0
mainFrame.Active = true
mainFrame.Draggable = true
mainFrame.Visible = guiVisible
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
	guiVisible = false
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
titleLabel.TextColor3 = Color3.fromRGB(0, 0, 0)
titleLabel.Parent = mainFrame

-- Layout pro tlačítka
local buttonHolder = Instance.new("Frame")
buttonHolder.Size = UDim2.new(1, 0, 1, -30)
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

-- Tlačítka se skripty
createButton("Wall hop script", function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/lyraEz/lol/refs/heads/main/loaders/NewWallhop.lua"))()
end)

createButton("Zephion for all games", function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/blackowl1231/ZYPHERION/refs/heads/main/main.lua"))()
end)

createButton("18+🔞", function()
	loadstring(game:HttpGet("https://pastebin.com/raw/FWwdST5Y"))()
end)

createButton("Buld a Boat", function()
loadstring(game:HttpGet('https://raw.githubusercontent.com/TheRealAsu/BABFT/refs/heads/main/UAP.lua'), true)()
end)


createButton("LALOL hub backdoor", function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/Its-LALOL/LALOL-Hub/main/Backdoor-Scanner/script"))()
end)


 createButton("Silent executor", function()
	loadstring(game:HttpGet(('https://raw.githubusercontent.com/vit3g13/SilenExecutor/refs/heads/main/Code.lua')))()
 end)

-- Zavřít tlačítkem
createButton("Close This", function()
	guiVisible = false
	mainFrame.Visible = false
	showTip("Press Right Shift to open", 3)
	
end)

-- Toggle pomocí RightShift
UserInputService.InputBegan:Connect(function(input, gameProcessed)
	if input.KeyCode == Enum.KeyCode.RightShift and not gameProcessed then
		guiVisible = not guiVisible
		mainFrame.Visible = guiVisible
	end
end)
