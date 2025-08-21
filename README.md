local Players = game:GetService("Players")
local player = Players.LocalPlayer
local mouse = player:GetMouse()
local Lighting = game:GetService("Lighting")
local VirtualInputManager = game:GetService("VirtualInputManager")

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "FiatHub"
ScreenGui.Parent = player:WaitForChild("PlayerGui")

local mainFrame = Instance.new("Frame")
mainFrame.Name = "MainFrame"
mainFrame.Size = UDim2.new(0, 340, 0, 230)
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

local updateLabel = Instance.new("TextLabel")
updateLabel.Text = "update: 0.1"
updateLabel.Size = UDim2.new(0, 65, 0, 20)
updateLabel.Position = UDim2.new(1, -100, 0, 14)
updateLabel.BackgroundTransparency = 1
updateLabel.TextColor3 = Color3.fromRGB(255, 220, 220)
updateLabel.Font = Enum.Font.FredokaOne
updateLabel.TextScaled = true
updateLabel.Parent = mainFrame

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

local dayBtn = Instance.new("TextButton")
dayBtn.Size = UDim2.new(0.75, 0, 0, 32)
dayBtn.Position = UDim2.new(0.125, 0, 0, 110)
dayBtn.BackgroundColor3 = Color3.fromRGB(240, 180, 45)
dayBtn.Text = "Função 3: Deixar de Dia"
dayBtn.TextColor3 = Color3.fromRGB(0,0,0)
dayBtn.Font = Enum.Font.FredokaOne
dayBtn.TextScaled = true
dayBtn.Parent = mainFrame

local skinBtn = Instance.new("TextButton")
skinBtn.Size = UDim2.new(0.75, 0, 0, 32)
skinBtn.Position = UDim2.new(0.125, 0, 0, 150)
skinBtn.BackgroundColor3 = Color3.fromRGB(200, 60, 60)
skinBtn.Text = "Função 3: Espiar Tesla Laboratório"
skinBtn.TextColor3 = Color3.fromRGB(255,255,255)
skinBtn.Font = Enum.Font.FredokaOne
skinBtn.TextScaled = true
skinBtn.Parent = mainFrame

local statusBall = Instance.new("Frame")
statusBall.Size = UDim2.new(0, 26, 0, 26)
statusBall.Position = UDim2.new(0.85, 0, 0, 200)
statusBall.BackgroundColor3 = Color3.fromRGB(228, 61, 61)
statusBall.BorderSizePixel = 0
statusBall.AnchorPoint = Vector2.new(0.5, 0)
statusBall.Parent = mainFrame

local actionText = Instance.new("TextLabel")
actionText.Size = UDim2.new(1, 0, 0, 32)
actionText.Position = UDim2.new(0, 0, 0, 190)
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

-- Função principal: Super Fast Attack (Touch)
local running = false
local attackLoop

local function updateStatus()
    if running then
        statusBall.BackgroundColor3 = Color3.fromRGB(67, 234, 82)
        fastAttackBtn.Text = "Desligar Super Fast Attack"
        actionText.Text = "Tecla 2 + Tecla 3 + Toque Celular"
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
                VirtualInputManager:SendKeyEvent(true, Enum.KeyCode.Two, false, game)
                VirtualInputManager:SendKeyEvent(false, Enum.KeyCode.Two, false, game)
                VirtualInputManager:SendKeyEvent(true, Enum.KeyCode.Three, false, game)
                VirtualInputManager:SendKeyEvent(false, Enum.KeyCode.Three, false, game)
                -- Simula toque do celular (touch)
                VirtualInputManager:SendTouchEvent(mouse.X, mouse.Y, 0, true, game, 1)
                VirtualInputManager:SendTouchEvent(mouse.X, mouse.Y, 0, false, game, 1)
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

-- Função 3: Deixar de Dia
dayBtn.MouseButton1Click:Connect(function()
    Lighting.TimeOfDay = "14:00:00"
    actionText.Text = "Agora está de dia!"
end)

-- Função 3: Espiar construção Tesla laboratório
local teslaEspiar = false

skinBtn.MouseButton1Click:Connect(function()
    teslaEspiar = not teslaEspiar
    if teslaEspiar then
        skinBtn.Text = "Desligar Espiar Tesla"
        actionText.Text = "Monitorando spawn Tesla laboratório..."
    else
        skinBtn.Text = "Função 3: Espiar Tesla Laboratório"
        actionText.Text = ""
    end
end)

local function highlightTesla(obj)
    local teslaLabel = Instance.new("TextLabel")
    teslaLabel.Text = obj.Name
    teslaLabel.Size = UDim2.new(0, 200, 0, 32)
    teslaLabel.Position = UDim2.new(0.5, -100, 0, 40)
    teslaLabel.BackgroundTransparency = 0.2
    teslaLabel.BackgroundColor3 = Color3.fromRGB(255,0,0)
    teslaLabel.TextColor3 = Color3.fromRGB(255,255,255)
    teslaLabel.Font = Enum.Font.FredokaOne
    teslaLabel.TextScaled = true
    teslaLabel.Parent = mainFrame
    game:GetService("Debris"):AddItem(teslaLabel, 3)
end

game.Workspace.ChildAdded:Connect(function(obj)
    if teslaEspiar and string.find(string.lower(obj.Name), "tesla") then
        highlightTesla(obj)
    end
end)

updateStatus()

