-- Fiat Hub Super Fast Attack 2 Faca Vampírica (Delta Executor, Roblox LuaU)

-- Criando a interface gráfica
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local mouse = player:GetMouse()

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "FiatHub"
ScreenGui.Parent = player:WaitForChild("PlayerGui")

local mainFrame = Instance.new("Frame")
mainFrame.Name = "MainFrame"
mainFrame.Size = UDim2.new(0, 320, 0, 170)
mainFrame.Position = UDim2.new(0, 0.2, 0, 0.3)
mainFrame.BackgroundColor3 = Color3.fromRGB(18, 81, 187)
mainFrame.BorderSizePixel = 0
mainFrame.Active = true
mainFrame.Draggable = true
mainFrame.Parent = ScreenGui

local title = Instance.new("TextLabel")
title.Text = "Fiat Hub Super Fast Attack 2 Faca Vampírica"
title.Size = UDim2.new(1, -40, 0, 36)
title.Position = UDim2.new(0, 20, 0, 10)
title.BackgroundTransparency = 1
title.TextColor3 = Color3.fromRGB(255,255,255)
title.Font = Enum.Font.FredokaOne
title.TextScaled = true
title.Parent = mainFrame

local closeBtn = Instance.new("TextButton")
closeBtn.Size = UDim2.new(0, 36, 0, 36)
closeBtn.Position = UDim2.new(1, -36, 0, 0)
closeBtn.BackgroundColor3 = Color3.fromRGB(25, 118, 210)
closeBtn.Text = "X"
closeBtn.TextColor3 = Color3.fromRGB(255,255,255)
closeBtn.Font = Enum.Font.FredokaOne
closeBtn.TextScaled = true
closeBtn.Parent = mainFrame

local fastAttackBtn = Instance.new("TextButton")
fastAttackBtn.Size = UDim2.new(0.75, 0, 0, 40)
fastAttackBtn.Position = UDim2.new(0.125, 0, 0, 60)
fastAttackBtn.BackgroundColor3 = Color3.fromRGB(33,150,243)
fastAttackBtn.Text = "Ligar Super Fast Attack"
fastAttackBtn.TextColor3 = Color3.fromRGB(255,255,255)
fastAttackBtn.Font = Enum.Font.FredokaOne
fastAttackBtn.TextScaled = true
fastAttackBtn.Parent = mainFrame

local statusBall = Instance.new("Frame")
statusBall.Size = UDim2.new(0, 26, 0, 26)
statusBall.Position = UDim2.new(0.85, 0, 0, 110)
statusBall.BackgroundColor3 = Color3.fromRGB(228, 61, 61)
statusBall.BorderSizePixel = 0
statusBall.AnchorPoint = Vector2.new(0.5, 0)
statusBall.Parent = mainFrame

local actionText = Instance.new("TextLabel")
actionText.Size = UDim2.new(1, 0, 0, 32)
actionText.Position = UDim2.new(0, 0, 0, 130)
actionText.BackgroundTransparency = 1
actionText.TextColor3 = Color3.fromRGB(255,255,255)
actionText.Font = Enum.Font.FredokaOne
actionText.TextScaled = true
actionText.Text = ""
actionText.Parent = mainFrame

-- Square F UI
local squareF = Instance.new("Frame")
squareF.Size = UDim2.new(0, 65, 0, 65)
squareF.Position = UDim2.new(0, 60, 0, 60)
squareF.BackgroundColor3 = Color3.fromRGB(18, 81, 187)
squareF.Visible = false
squareF.Active = true
squareF.Draggable = true
squareF.Parent = ScreenGui

local fBtn = Instance.new("TextButton")
fBtn.Size = UDim2.new(1, 0, 1, 0)
fBtn.Position = UDim2.new(0, 0, 0, 0)
fBtn.BackgroundTransparency = 1
fBtn.Text = "F"
fBtn.TextColor3 = Color3.fromRGB(255,255,255)
fBtn.Font = Enum.Font.FredokaOne
fBtn.TextScaled = true
fBtn.Parent = squareF

-- Função principal: Super Fast Attack
local running = false
local attackLoop

local function updateStatus()
    if running then
        statusBall.BackgroundColor3 = Color3.fromRGB(67, 234, 82)
        fastAttackBtn.Text = "Desligar Super Fast Attack"
        actionText.Text = "Tecla 2 + Tecla 3 + Clique"
    else
        statusBall.BackgroundColor3 = Color3.fromRGB(228, 61, 61)
        fastAttackBtn.Text = "Ligar Super Fast Attack"
        actionText.Text = ""
    end
end

fastAttackBtn.MouseButton1Click:Connect(function()
    running = not running
    updateStatus()
    if running then
        attackLoop = true
        spawn(function()
            while running and attackLoop do
                -- Simula pressionar teclas 2 e 3
                local VirtualInputManager = game:GetService("VirtualInputManager")
                VirtualInputManager:SendKeyEvent(true, Enum.KeyCode.Two, false, game)
                VirtualInputManager:SendKeyEvent(false, Enum.KeyCode.Two, false, game)
                VirtualInputManager:SendKeyEvent(true, Enum.KeyCode.Three, false, game)
                VirtualInputManager:SendKeyEvent(false, Enum.KeyCode.Three, false, game)
                -- Simula clique do mouse (MouseButton1Down)
                VirtualInputManager:SendMouseButtonEvent(mouse.X, mouse.Y, 0, true, game, 1)
                VirtualInputManager:SendMouseButtonEvent(mouse.X, mouse.Y, 0, false, game, 1)
                wait(0.2)
            end
        end)
    else
        attackLoop = false
    end
end)

closeBtn.MouseButton1Click:Connect(function()
    mainFrame.Visible = false
    squareF.Visible = true
end)

fBtn.MouseButton1Click:Connect(function()
    mainFrame.Visible = true
    squareF.Visible = false
end)

updateStatus()
