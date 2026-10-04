local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")

local Player = Players.LocalPlayer

local MINATO_IMAGE_ID = "rbxassetid://0"
local NARUTO_IMAGE_ID = "rbxassetid://0"

local Gui = Instance.new("ScreenGui")
Gui.Name = "NarutoModz"
Gui.ResetOnSpawn = false
Gui.Parent = Player:WaitForChild("PlayerGui")

local function Corner(obj, radius)
	local c = Instance.new("UICorner")
	c.CornerRadius = UDim.new(0, radius or 8)
	c.Parent = obj
end

local Main = Instance.new("Frame")
Main.Size = UDim2.fromOffset(650, 430)
Main.Position = UDim2.new(.5, -325, .5, -215)
Main.BackgroundColor3 = Color3.fromRGB(10, 8, 14)
Main.BorderSizePixel = 0
Main.Parent = Gui
Corner(Main, 12)

local Background = Instance.new("ImageLabel")
Background.Size = UDim2.fromScale(1, 1)
Background.BackgroundTransparency = 1
Background.Image = MINATO_IMAGE_ID
Background.ImageTransparency = .65
Background.ScaleType = Enum.ScaleType.Crop
Background.Parent = Main
Corner(Background, 12)

local Dark = Instance.new("Frame")
Dark.Size = UDim2.fromScale(1, 1)
Dark.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
Dark.BackgroundTransparency = .25
Dark.BorderSizePixel = 0
Dark.Parent = Main
Corner(Dark, 12)

local Header = Instance.new("Frame")
Header.Size = UDim2.new(1, 0, 0, 65)
Header.BackgroundTransparency = 1
Header.Parent = Main

local Title = Instance.new("TextLabel")
Title.Size = UDim2.fromOffset(300, 35)
Title.Position = UDim2.fromOffset(18, 7)
Title.BackgroundTransparency = 1
Title.Text = "NARUTO MODZ"
Title.TextColor3 = Color3.fromRGB(205, 60, 255)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 25
Title.TextXAlignment = Enum.TextXAlignment.Left
Title.Parent = Header

local Close = Instance.new("TextButton")
Close.Size = UDim2.fromOffset(40, 40)
Close.Position = UDim2.new(1, -50, 0, 12)
Close.BackgroundColor3 = Color3.fromRGB(35, 20, 45)
Close.Text = "×"
Close.TextColor3 = Color3.new(1, 1, 1)
Close.TextSize = 28
Close.Font = Enum.Font.GothamBold
Close.Parent = Header
Corner(Close, 10)

local Body = Instance.new("Frame")
Body.Size = UDim2.new(1, -20, 1, -75)
Body.Position = UDim2.fromOffset(10, 70)
Body.BackgroundTransparency = 1
Body.Parent = Main

local Sidebar = Instance.new("Frame")
Sidebar.Size = UDim2.new(0, 145, 1, 0)
Sidebar.BackgroundColor3 = Color3.fromRGB(9, 7, 13)
Sidebar.BackgroundTransparency = .15
Sidebar.Parent = Body
Corner(Sidebar, 10)

local SideLayout = Instance.new("UIListLayout")
SideLayout.Padding = UDim.new(0, 6)
SideLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
SideLayout.Parent = Sidebar

local SidePad = Instance.new("UIPadding")
SidePad.PaddingTop = UDim.new(0, 10)
SidePad.Parent = Sidebar

local Content = Instance.new("Frame")
Content.Size = UDim2.new(1, -155, 1, 0)
Content.Position = UDim2.fromOffset(155, 0)
Content.BackgroundColor3 = Color3.fromRGB(7, 6, 10)
Content.BackgroundTransparency = .2
Content.Parent = Body
Corner(Content, 10)

local Pages = {}
local Tabs = {}

local function Page(name)
	local p = Instance.new("ScrollingFrame")
	p.Name = name
	p.Size = UDim2.new(1, -20, 1, -20)
	p.Position = UDim2.fromOffset(10, 10)
	p.BackgroundTransparency = 1
	p.BorderSizePixel = 0
	p.ScrollBarThickness = 3
	p.Visible = false
	p.Parent = Content

	local l = Instance.new("UIListLayout")
	l.Padding = UDim.new(0, 8)
	l.Parent = p

	local pad = Instance.new("UIPadding")
	pad.PaddingTop = UDim.new(0, 5)
	pad.PaddingBottom = UDim.new(0, 10)
	pad.Parent = p

	l:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
		p.CanvasSize = UDim2.fromOffset(0, l.AbsoluteContentSize.Y + 20)
	end)

	Pages[name] = p
	return p
end

local function Tab(name, icon)
	local b = Instance.new("TextButton")
	b.Size = UDim2.fromOffset(130, 42)
	b.BackgroundColor3 = Color3.fromRGB(22, 17, 29)
	b.Text = icon .. "  " .. name
	b.TextColor3 = Color3.fromRGB(205, 205, 205)
	b.Font = Enum.Font.GothamBold
	b.TextSize = 13
	b.AutoButtonColor = false
	b.Parent = Sidebar
	Corner(b, 8)

	Tabs[name] = b

	b.MouseButton1Click:Connect(function()
		for n, p in pairs(Pages) do
			p.Visible = n == name
		end

		for n, x in pairs(Tabs) do
			x.BackgroundColor3 =
				n == name
				and Color3.fromRGB(130, 20, 220)
				or Color3.fromRGB(22, 17, 29)
		end
	end)
end

Tab("Combat", "⚔")
Tab("Movement", "🏃")
Tab("Visuals", "👁")
Tab("Misc", "👤")
Tab("Settings", "⚙")

local Combat = Page("Combat")
local Movement = Page("Movement")
local Visuals = Page("Visuals")
local Misc = Page("Misc")
local Settings = Page("Settings")

local function Switch(parent, name, callback)
	local holder = Instance.new("Frame")
	holder.Size = UDim2.new(1, 0, 0, 48)
	holder.BackgroundColor3 = Color3.fromRGB(19, 16, 24)
	holder.Parent = parent
	Corner(holder, 8)

	local label = Instance.new("TextLabel")
	label.Size = UDim2.new(1, -80, 1, 0)
	label.Position = UDim2.fromOffset(14, 0)
	label.BackgroundTransparency = 1
	label.Text = name
	label.TextColor3 = Color3.fromRGB(240, 240, 240)
	label.Font = Enum.Font.GothamBold
	label.TextSize = 14
	label.TextXAlignment = Enum.TextXAlignment.Left
	label.Parent = holder

	local button = Instance.new("TextButton")
	button.Size = UDim2.fromOffset(46, 24)
	button.Position = UDim2.new(1, -58, .5, -12)
	button.BackgroundColor3 = Color3.fromRGB(55, 50, 60)
	button.Text = ""
	button.Parent = holder
	Corner(button, 15)

	local circle = Instance.new("Frame")
	circle.Size = UDim2.fromOffset(18, 18)
	circle.Position = UDim2.fromOffset(3, 3)
	circle.BackgroundColor3 = Color3.fromRGB(235, 235, 235)
	circle.Parent = button
	Corner(circle, 20)

	local state = false

	button.MouseButton1Click:Connect(function()
		state = not state

		button.BackgroundColor3 = state
			and Color3.fromRGB(165, 30, 245)
			or Color3.fromRGB(55, 50, 60)

		circle.Position = state
			and UDim2.new(1, -21, 0, 3)
			or UDim2.fromOffset(3, 3)

		if callback then
			callback(state)
		end
	end)
end

local function Slider(parent, name, min, max, default, callback)
	local holder = Instance.new("Frame")
	holder.Size = UDim2.new(1, 0, 0, 72)
	holder.BackgroundColor3 = Color3.fromRGB(19, 16, 24)
	holder.Parent = parent
	Corner(holder, 8)

	local label = Instance.new("TextLabel")
	label.Size = UDim2.fromOffset(250, 25)
	label.Position = UDim2.fromOffset(14, 5)
	label.BackgroundTransparency = 1
	label.Text = name
	label.TextColor3 = Color3.fromRGB(240, 240, 240)
	label.Font = Enum.Font.GothamBold
	label.TextSize = 14
	label.TextXAlignment = Enum.TextXAlignment.Left
	label.Parent = holder

	local valueLabel = Instance.new("TextLabel")
	valueLabel.Size = UDim2.fromOffset(70, 25)
	valueLabel.Position = UDim2.new(1, -85, 0, 5)
	valueLabel.BackgroundTransparency = 1
	valueLabel.Text = tostring(default)
	valueLabel.TextColor3 = Color3.fromRGB(190, 50, 255)
	valueLabel.Font = Enum.Font.GothamBold
	valueLabel.TextSize = 13
	valueLabel.TextXAlignment = Enum.TextXAlignment.Right
	valueLabel.Parent = holder

	local bar = Instance.new("Frame")
	bar.Size = UDim2.new(1, -30, 0, 6)
	bar.Position = UDim2.fromOffset(15, 48)
	bar.BackgroundColor3 = Color3.fromRGB(55, 50, 60)
	bar.Parent = holder
	Corner(bar, 5)

	local fill = Instance.new("Frame")
	fill.Size = UDim2.new((default-min)/(max-min), 0, 1, 0)
	fill.BackgroundColor3 = Color3.fromRGB(175, 30, 245)
	fill.Parent = bar
	Corner(fill, 5)

	local dragging = false

	local function SetValue(x)
		local percent = math.clamp(
			(x - bar.AbsolutePosition.X) / bar.AbsoluteSize.X,
			0,
			1
		)

		local value = math.floor(min + (max-min) * percent)

		fill.Size = UDim2.new(percent, 0, 1, 0)
		valueLabel.Text = tostring(value)

		if callback then
			callback(value)
		end
	end

	bar.InputBegan:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseButton1
			or input.UserInputType == Enum.UserInputType.Touch then
			dragging = true
			SetValue(input.Position.X)
		end
	end)

	UIS.InputChanged:Connect(function(input)
		if dragging and (
			input.UserInputType == Enum.UserInputType.MouseMovement
			or input.UserInputType == Enum.UserInputType.Touch
		) then
			SetValue(input.Position.X)
		end
	end)

	UIS.InputEnded:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseButton1
			or input.UserInputType == Enum.UserInputType.Touch then
			dragging = false
		end
	end)
end

-- COMBAT

Switch(Combat, "Aim Silent")
Switch(Combat, "Aimbot")
Switch(Combat, "Aim Kill")
Slider(Combat, "FOV", 0, 360, 180)

-- MOVEMENT

Slider(Movement, "Speed", 32, 100, 32, function(value)
	local character = Player.Character
	local humanoid = character and character:FindFirstChildOfClass("Humanoid")

	if humanoid then
		humanoid.WalkSpeed = value
	end
end)

Switch(Movement, "Spinbot")
Switch(Movement, "Infinity Jump")

-- VISUALS

Switch(Visuals, "Box")
Switch(Visuals, "Line")
Switch(Visuals, "Nome")
Switch(Visuals, "Distance")
Switch(Visuals, "Vida")
Switch(Visuals, "Mostrar FOV")

-- MISC

Switch(Misc, "Ocultar painel", function(state)
	Main.Visible = not state
end)

Switch(Misc, "Stream Mode")

-- SETTINGS

Slider(Settings, "Tamanho do menu", 70, 130, 100, function(value)
	local scale = value / 100
	Main.Size = UDim2.fromOffset(650 * scale, 430 * scale)
end)

-- BOTÃO FLUTUANTE

local Floating = Instance.new("ImageButton")
Floating.Size = UDim2.fromOffset(65, 65)
Floating.Position = UDim2.new(0, 25, .5, -32)
Floating.BackgroundColor3 = Color3.fromRGB(15, 10, 20)
Floating.Image = NARUTO_IMAGE_ID
Floating.ScaleType = Enum.ScaleType.Crop
Floating.Visible = false
Floating.Parent = Gui
Corner(Floating, 50)

Close.MouseButton1Click:Connect(function()
	Main.Visible = false
	Floating.Visible = true
end)

Floating.MouseButton1Click:Connect(function()
	Main.Visible = true
	Floating.Visible = false
end)

-- ARRASTAR MENU

local dragging = false
local dragStart
local startPos

Header.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1
		or input.UserInputType == Enum.UserInputType.Touch then

		dragging = true
		dragStart = input.Position
		startPos = Main.Position
	end
end)

UIS.InputChanged:Connect(function(input)
	if dragging and (
		input.UserInputType == Enum.UserInputType.MouseMovement
		or input.UserInputType == Enum.UserInputType.Touch
	) then

		local delta = input.Position - dragStart

		Main.Position = UDim2.new(
			startPos.X.Scale,
			startPos.X.Offset + delta.X,
			startPos.Y.Scale,
			startPos.Y.Offset + delta.Y
		)
	end
end)

UIS.InputEnded:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1
		or input.UserInputType == Enum.UserInputType.Touch then
		dragging = false
	end
end)

Pages.Combat.Visible = true
Tabs.Combat.BackgroundColor3 = Color3.fromRGB(130, 20, 220)
