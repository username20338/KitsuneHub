# KitsuneHub-- KitsuneHub Script para Blox Fruits

local Player = game.Players.LocalPlayer
local Character = Player.Character or Player.CharacterAdded:Wait()
local Humanoid = Character:WaitForChild("Humanoid")
local Camera = game.Workspace.CurrentCamera
local UIS = game:GetService("UserInputService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local TweenService = game:GetService("TweenService")
local Remote = ReplicatedStorage:WaitForChild("Remotes"):WaitForChild("Combat")
local RemoteFruit = ReplicatedStorage:WaitForChild("Remotes"):WaitForChild("Fruit")

-- Função para Teleporte
function teleportTo(coords)
    local Tween = TweenService:Create(Camera, TweenInfo.new(1, Enum.EasingStyle.Linear), {CFrame = CFrame.new(coords)})
    Tween:Play()
end

-- Função de Auto-Farm
function enableAutoFarm()
    while true do
        -- Itera por todos os inimigos ao redor
        for _, enemy in pairs(workspace:GetChildren()) do
            if enemy:FindFirstChild("Humanoid") and enemy.Humanoid.Health > 0 then
                -- Ataca o inimigo
                Remote:FireServer("Melee", enemy)  -- Simula um ataque
                wait(0.5)
            end
        end
        wait(1)  -- Tempo entre os ataques
    end
end

-- Função para pegar frutas
function autoGetFruit()
    for _, fruit in pairs(workspace:GetChildren()) do
        if fruit.Name == "Fruit" and fruit:FindFirstChild("Handle") then
            -- Coloca a lógica de pegar fruta aqui
            RemoteFruit:FireServer("Eat", fruit)  -- Simula pegar a fruta
            wait(2)
        end
    end
end

-- Função para ativar as habilidades automaticamente
function enableAutoSkills()
    while true do
        -- Ativa habilidades automaticamente
        -- Se o personagem tiver habilidades equipadas, você pode chamar suas funções aqui
        -- Exemplo para ativar habilidade 1
        if Character:FindFirstChild("Skill1") then
            Character.Skill1:Fire()  -- Simula usar a habilidade
        end
        wait(2)
    end
end

-- Função de Fly Mode
function enableFlyMode()
    local flying = true
    while flying do
        -- Controla o voo com a tecla "F"
        if UIS:IsKeyDown(Enum.KeyCode.F) then
            Character:MoveTo(Character.Position + Vector3.new(0, 10, 0))  -- Simula voo
        end
        wait(0.1)
    end
end

-- Função de Auto Equip
function autoEquip()
    -- Equipar automaticamente a espada e habilidades
    if not Character:FindFirstChild("Sword") then
        local sword = Instance.new("Tool")
        sword.Name = "Sword"
        sword.Parent = Character
    end
end

-- Função para ativar a corrida automática
function enableAutoRun()
    -- O personagem corre automaticamente
    Humanoid.WalkSpeed = 100  -- Velocidade de corrida
end

-- Função para ativar o God Mode (invencibilidade)
function enableGodMode()
    while true do
        Humanoid.Health = math.huge  -- Define saúde infinita
        wait(1)
    end
end

-- Menu GUI para interagir com o script
local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
local MainFrame = Instance.new("Frame", ScreenGui)
MainFrame.Size = UDim2.new(0, 300, 0, 400)
MainFrame.Position = UDim2.new(0, 50, 0, 50)
MainFrame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)

local ButtonTele = Instance.new("TextButton", MainFrame)
ButtonTele.Size = UDim2.new(0, 280, 0, 50)
ButtonTele.Position = UDim2.new(0, 10, 0, 10)
ButtonTele.Text = "Teleport to Specified Coordinates"
ButtonTele.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
ButtonTele.TextColor3 = Color3.fromRGB(255, 255, 255)
ButtonTele.MouseButton1Click:Connect(function()
    teleportTo(Vector3.new(100, 50, 200))  -- Coordenadas de exemplo
end)

local ButtonAutoFarm = Instance.new("TextButton", MainFrame)
ButtonAutoFarm.Size = UDim2.new(0, 280, 0, 50)
ButtonAutoFarm.Position = UDim2.new(0, 10, 0, 70)
ButtonAutoFarm.Text = "Enable Auto Farm"
ButtonAutoFarm.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
ButtonAutoFarm.TextColor3 = Color3.fromRGB(255, 255, 255)
ButtonAutoFarm.MouseButton1Click:Connect(function()
    enableAutoFarm()
end)

local ButtonAutoGetFruit = Instance.new("TextButton", MainFrame)
ButtonAutoGetFruit.Size = UDim2.new(0, 280, 0, 50)
ButtonAutoGetFruit.Position = UDim2.new(0, 10, 0, 130)
ButtonAutoGetFruit.Text = "Auto Get Fruit"
ButtonAutoGetFruit.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
ButtonAutoGetFruit.TextColor3 = Color3.fromRGB(255, 255, 255)
ButtonAutoGetFruit.MouseButton1Click:Connect(function()
    autoGetFruit()
end)

local ButtonAutoSkills = Instance.new("TextButton", MainFrame)
ButtonAutoSkills.Size = UDim2.new(0, 280, 0, 50)
ButtonAutoSkills.Position = UDim2.new(0, 10, 0, 190)
ButtonAutoSkills.Text = "Enable Auto Skills"
ButtonAutoSkills.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
ButtonAutoSkills.TextColor3 = Color3.fromRGB(255, 255, 255)
ButtonAutoSkills.MouseButton1Click:Connect(function()
    enableAutoSkills()
end)

local ButtonFlyMode = Instance.new("TextButton", MainFrame)
ButtonFlyMode.Size = UDim2.new(0, 280, 0, 50)
ButtonFlyMode.Position = UDim2.new(0, 10, 0, 250)
ButtonFlyMode.Text = "Enable Fly Mode"
ButtonFlyMode.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
ButtonFlyMode.TextColor3 = Color3.fromRGB(255, 255, 255)
ButtonFlyMode.MouseButton1Click:Connect(function()
    enableFlyMode()
end)

local ButtonEquip = Instance.new("TextButton", MainFrame)
ButtonEquip.Size = UDim2.new(0, 280, 0, 50)
ButtonEquip.Position = UDim2.new(0, 10, 0, 310)
ButtonEquip.Text = "Auto Equip"
ButtonEquip.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
ButtonEquip.TextColor3 = Color3.fromRGB(255, 255, 255)
ButtonEquip.MouseButton1Click:Connect(function()
    autoEquip()
end)

local ButtonRun = Instance.new("TextButton", MainFrame)
ButtonRun.Size = UDim2.new(0, 280, 0, 50)
ButtonRun.Position = UDim2.new(0, 10, 0, 370)
ButtonRun.Text = "Enable Auto Run"
ButtonRun.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
ButtonRun.TextColor3 = Color3.fromRGB(255, 255, 255)
ButtonRun.MouseButton1Click:Connect(function()
    enableAutoRun()
end)

local ButtonGodMode = Instance.new("TextButton", MainFrame)
ButtonGodMode.Size = UDim2.new(0, 280, 0, 50)
ButtonGodMode.Position = UDim2.new(0, 10, 0, 430)
ButtonGodMode.Text = "Enable God Mode"
ButtonGodMode.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
ButtonGodMode.TextColor3 = Color3.fromRGB(255, 255, 255)
ButtonGodMode.MouseButton1Click:Connect(function()
    enableGodMode()
end)

-- Função de ativação do script
ScreenGui.Parent = game
