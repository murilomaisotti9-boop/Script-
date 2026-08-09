# Script-
-- Garante que o jogo carregou
repeat task.wait() until game:IsLoaded()

local player = game.Players.LocalPlayer
local hitboxesAtivas = false
local tamanhoDesejado = 6
local transparenciaDesejada = 0.5

-- Remove a interface anterior se já existir
if game.CoreGui:FindFirstChild("DocaHubHitboxPerfeito") then
    game.CoreGui.DocaHubHitboxPerfeito:Destroy()
end

-- Criação da Interface Principal (GUI)
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "DocaHubHitboxPerfeito"
ScreenGui.Parent = game.CoreGui
ScreenGui.ResetOnSpawn = false

-- Botão Flutuante (Abre/Fecha o Menu)
local OpenButton = Instance.new("TextButton")
OpenButton.Name = "OpenButton"
OpenButton.Parent = ScreenGui
OpenButton.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
OpenButton.Position = UDim2.new(0.02, 0, 0.4, 0)
OpenButton.Size = UDim2.new(0, 48, 0, 48)
OpenButton.Font = Enum.Font.GothamBold
OpenButton.Text = "DH"
OpenButton.TextColor3 = Color3.fromRGB(0, 170, 255)
OpenButton.TextSize = 18
OpenButton.Active = true
OpenButton.Draggable = true

local UICornerBtn = Instance.new("UICorner")
UICornerBtn.CornerRadius = UDim.new(0, 12)
UICornerBtn.Parent = OpenButton

local UIStrokeBtn = Instance.new("UIStroke")
UIStrokeBtn.Color = Color3.fromRGB(0, 170, 255)
UIStrokeBtn.Thickness = 2
UIStrokeBtn.Parent = OpenButton

-- Painel Principal (Visual Moderno Perfeito)
local MainFrame = Instance.new("Frame")
MainFrame.Name = "MainFrame"
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
MainFrame.Position = UDim2.new(0.1, 0, 0.3, 0)
MainFrame.Size = UDim2.new(0, 240, 0, 230)
MainFrame.Visible = false
MainFrame.Active = true
MainFrame.Draggable = true

local UICornerFrame = Instance.new("UICorner")
UICornerFrame.CornerRadius = UDim.new(0, 14)
UICornerFrame.Parent = MainFrame

local UIStrokeFrame = Instance.new("UIStroke")
UIStrokeFrame.Color = Color3.fromRGB(40, 40, 40)
UIStrokeFrame.Thickness = 2
UIStrokeFrame.Parent = MainFrame

-- Título do Menu
local Title = Instance.new("TextLabel")
Title.Parent = MainFrame
Title.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
Title.Size = UDim2.new(1, 0, 0, 40)
Title.Font = Enum.Font.GothamBold
Title.Text = "Doca Hub | Hitbox Pro"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.TextSize = 14

local UICornerTitle = Instance.new("UICorner")
UICornerTitle.CornerRadius = UDim.new(0, 14)
UICornerTitle.Parent = Title

-- Botão de Ligar/Desligar Hitbox
local ToggleHitbox = Instance.new("TextButton")
ToggleHitbox.Parent = MainFrame
ToggleHitbox.BackgroundColor3 = Color3.fromRGB(180, 40, 40)
ToggleHitbox.Position = UDim2.new(0.1, 0, 0.23, 0)
ToggleHitbox.Size = UDim2.new(0.8, 0, 0, 32)
ToggleHitbox.Font = Enum.Font.GothamBold
ToggleHitbox.Text = "Hitbox: OFF"
ToggleHitbox.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleHitbox.TextSize = 13

local UICornerToggle = Instance.new("UICorner")
UICornerToggle.CornerRadius = UDim.new(0, 8)
UICornerToggle.Parent = ToggleHitbox

-- Label de Tamanho
local LabelTamanho = Instance.new("TextLabel")
LabelTamanho.Parent = MainFrame
LabelTamanho.BackgroundTransparency = 1
LabelTamanho.Position = UDim2.new(0.1, 0, 0.43, 0)
LabelTamanho.Size = UDim2.new(0.8, 0, 0, 20)
LabelTamanho.Font = Enum.Font.GothamBold
LabelTamanho.Text = "Tamanho: 6"
LabelTamanho.TextColor3 = Color3.fromRGB(200, 200, 200)
LabelTamanho.TextSize = 12
LabelTamanho.TextXAlignment = Enum.TextXAlignment.Left

-- Botões de Tamanho
local BtnMenosSize = Instance.new("TextButton")
BtnMenosSize.Parent = MainFrame
BtnMenosSize.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
BtnMenosSize.Position = UDim2.new(0.1, 0, 0.53, 0)
BtnMenosSize.Size = UDim2.new(0.38, 0, 0, 28)
BtnMenosSize.Font = Enum.Font.GothamBold
BtnMenosSize.Text = "- Tamanho"
BtnMenosSize.TextColor3 = Color3.fromRGB(255, 255, 255)
BtnMenosSize.TextSize = 11

local UICornerMS = Instance.new("UICorner")
UICornerMS.CornerRadius = UDim.new(0, 8)
UICornerMS.Parent = BtnMenosSize

local BtnMaisSize = Instance.new("TextButton")
BtnMaisSize.Parent = MainFrame
BtnMaisSize.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
BtnMaisSize.Position = UDim2.new(0.52, 0, 0.53, 0)
BtnMaisSize.Size = UDim2.new(0.38, 0, 0, 28)
BtnMaisSize.Font = Enum.Font.GothamBold
BtnMaisSize.Text = "+ Tamanho"
BtnMaisSize.TextColor3 = Color3.fromRGB(255, 255, 255)
BtnMaisSize.TextSize = 11

local UICornerPS = Instance.new("UICorner")
UICornerPS.CornerRadius = UDim.new(0, 8)
UICornerPS.Parent = BtnMaisSize

-- Label de Transparência
local LabelTransp = Instance.new("TextLabel")
LabelTransp.Parent = MainFrame
LabelTransp.BackgroundTransparency = 1
LabelTransp.Position = UDim2.new(0.1, 0, 0.68, 0)
LabelTransp.Size = UDim2.new(0.8, 0, 0, 20)
LabelTransp.Font = Enum.Font.GothamBold
LabelTransp.Text = "Transparência: 0.5"
LabelTransp.TextColor3 = Color3.fromRGB(200, 200, 200)
LabelTransp.TextSize = 12
LabelTransp.TextXAlignment = Enum.TextXAlignment.Left

-- Botões de Transparência
local BtnMenosTransp = Instance.new("TextButton")
BtnMenosTransp.Parent = MainFrame
BtnMenosTransp.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
BtnMenosTransp.Position = UDim2.new(0.1, 0, 0.78, 0)
BtnMenosTransp.Size = UDim2.new(0.38, 0, 0, 28)
BtnMenosTransp.Font = Enum.Font.GothamBold
BtnMenosTransp.Text = "- Transp"
BtnMenosTransp.TextColor3 = Color3.fromRGB(255, 255, 255)
BtnMenosTransp.TextSize = 11

local UICornerMT = Instance.new("UICorner")
UICornerMT.CornerRadius = UDim.new(0, 8)
UICornerMT.Parent = BtnMenosTransp

local BtnMaisTransp = Instance.new("TextButton")
BtnMaisTransp.Parent = MainFrame
BtnMaisTransp.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
BtnMaisTransp.Position = UDim2.new(0.52, 0, 0.78, 0)
BtnMaisTransp.Size = UDim2.new(0.38, 0, 0, 28)
BtnMaisTransp.Font = Enum.Font.GothamBold
BtnMaisTransp.Text = "+ Transp"
BtnMaisTransp.TextColor3 = Color3.fromRGB(255, 255, 255)
BtnMaisTransp.TextSize = 11

local UICornerPT = Instance.new("UICorner")
UICornerPT.CornerRadius = UDim.new(0, 8)
UICornerPT.Parent = BtnMaisTransp

-- Abertura garantida por clique direto (compatível com Mobile/Delta)
OpenButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = not MainFrame.Visible
end)

ToggleHitbox.MouseButton1Click:Connect(function()
    hitboxesAtivas = not hitboxesAtivas
    if hitboxesAtivas then
        ToggleHitbox.Text = "Hitbox: ON"
        ToggleHitbox.BackgroundColor3 = Color3.fromRGB(40, 180, 40)
    else
        ToggleHitbox.Text = "Hitbox: OFF"
        ToggleHitbox.BackgroundColor3 = Color3.fromRGB(180, 40, 40)
        
        -- Restaura o tamanho original dos players ao desligar
        for _, outroPlayer in ipairs(game.Players:GetPlayers()) do
            if outroPlayer ~= player and outroPlayer.Character then
                local hrp = outroPlayer.Character:FindFirstChild("HumanoidRootPart")
                if hrp then
                    hrp.Size = Vector3.new(2, 2, 1)
                    hrp.Transparency = 1
                    hrp.CanCollide = true
                end
            end
        end
    end
end)

BtnMaisSize.MouseButton1Click:Connect(function()
    if tamanhoDesejado < 15 then
        tamanhoDesejado = tamanhoDesejado + 1
        LabelTamanho.Text = "Tamanho: " .. tostring(tamanhoDesejado)
    end
end)

BtnMenosSize.MouseButton1Click:Connect(function()
    if tamanhoDesejado > 3 then
        tamanhoDesejado = tamanhoDesejado - 1
        LabelTamanho.Text = "Tamanho: " .. tostring(tamanhoDesejado)
    end
end)

BtnMaisTransp.MouseButton1Click:Connect(function()
    if transparenciaDesejada < 1 then
        transparenciaDesejada = math.floor((transparenciaDesejada + 0.1) * 10 + 0.5) / 10
        LabelTransp.Text = "Transparência: " .. tostring(transparenciaDesejada)
    end
end)

BtnMenosTransp.MouseButton1Click:Connect(function()
    if transparenciaDesejada > 0 then
        transparenciaDesejada = math.floor((transparenciaDesejada - 0.1) * 10 + 0.5) / 10
        LabelTransp.Text = "Transparência: " .. tostring(transparenciaDesejada)
    end
end)

-- Loop principal da hitbox
task.spawn(function()
    while task.wait(0.3) do
        if hitboxesAtivas then
            for _, outroPlayer in ipairs(game.Players:GetPlayers()) do
                if outroPlayer ~= player and outroPlayer.Character then
                    local char = outroPlayer.Character
                    local hrp = char:FindFirstChild("HumanoidRootPart")
                    local hum = char:FindFirstChild("Humanoid")
                    
                    if hrp and hum and hum.Health > 0 then
                        hrp.Size = Vector3.new(tamanhoDesejado, tamanhoDesejado, tamanhoDesejado)
                        hrp.Transparency = transparenciaDesejada
                        hrp.CanCollide = false
                    end
                end
            end
        end
    end
end)
