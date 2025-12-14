-- CONFIG
local RUN_SPEED = 70

-- PLAYER
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")
local normalSpeed = humanoid.WalkSpeed

-- GUI
local gui = Instance.new("ScreenGui")
gui.Name = "RunButtonGui"
gui.Parent = player:WaitForChild("PlayerGui")

local button = Instance.new("TextButton")
button.Parent = gui
button.Size = UDim2.new(0, 80, 0, 80)
button.Position = UDim2.new(1, -100, 0.5, -40)
button.Text = "RUN"
button.TextColor3 = Color3.fromRGB(255, 255, 255)
button.TextScaled = true
button.AutoButtonColor = false
button.BackgroundColor3 = Color3.fromRGB(255, 0, 0)

-- BOTÃO REDONDO
local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(1, 0)
corner.Parent = button

-- BORDA
local stroke = Instance.new("UIStroke")
stroke.Thickness = 2
stroke.Color = Color3.fromRGB(255, 255, 255)
stroke.Parent = button

-- FUNÇÃO CORRER
button.MouseButton1Down:Connect(function()
	humanoid.WalkSpeed = RUN_SPEED
end)

button.MouseButton1Up:Connect(function()
	humanoid.WalkSpeed = normalSpeed
end)

button.TouchEnded:Connect(function()
	humanoid.WalkSpeed = normalSpeed
end)

-- 🌈 RGB EFFECT
task.spawn(function()
	local colors = {
		Color3.fromRGB(255, 0, 0),
		Color3.fromRGB(0, 255, 0),
		Color3.fromRGB(0, 0, 255),
		Color3.fromRGB(255, 255, 0),
		Color3.fromRGB(255, 0, 255),
		Color3.fromRGB(0, 255, 255)
	}

	local i = 1
	while button.Parent do
		button.BackgroundColor3 = colors[i]
		stroke.Color = colors[i]
		i = i + 1
		if i > #colors then
			i = 1
		end
		task.wait(0.2) -- velocidade do RGB
	end
end)
