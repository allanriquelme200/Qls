-- Interface simples para Auto Farm de Lixo
local Gui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local StartButton = Instance.new("TextButton")
local StopButton = Instance.new("TextButton")

local running = false

-- Interface
Gui.Name = "AutoFarmGui"
Gui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

Frame.Parent = Gui
Frame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
Frame.Position = UDim2.new(0.1, 0, 0.1, 0)
Frame.Size = UDim2.new(0, 200, 0, 120)
Frame.Active = true
Frame.Draggable = true

StartButton.Parent = Frame
StartButton.Position = UDim2.new(0, 10, 0, 10)
StartButton.Size = UDim2.new(0, 180, 0, 40)
StartButton.Text = "Iniciar Auto Farm"
StartButton.BackgroundColor3 = Color3.fromRGB(0, 170, 0)
StartButton.TextColor3 = Color3.fromRGB(255, 255, 255)

StopButton.Parent = Frame
StopButton.Position = UDim2.new(0, 10, 0, 65)
StopButton.Size = UDim2.new(0, 180, 0, 40)
StopButton.Text = "Parar Auto Farm"
StopButton.BackgroundColor3 = Color3.fromRGB(170, 0, 0)
StopButton.TextColor3 = Color3.fromRGB(255, 255, 255)

-- Função de farm simples (exemplo genérico)
local function autoFarm()
    while running do
        -- Exemplo: Procura por objetos chamados "Lixo" no workspace
        for _, obj in pairs(workspace:GetDescendants()) do
            if obj:IsA("Part") and obj.Name:lower():find("lixo") then
                game.Players.LocalPlayer.Character:MoveTo(obj.Position)
                wait(1.5) -- Aguarda para "coletar"
                fireproximityprompt(obj:FindFirstChildOfClass("ProximityPrompt"))
                wait(0.5)
            end
        end
        wait(3)
    end
end

-- Botões
StartButton.MouseButton1Click:Connect(function()
    if not running then
        running = true
        autoFarm()
    end
end)

StopButton.MouseButton1Click:Connect(function()
    running = false
end)
