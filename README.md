-- Script otimizado para Delta
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

-- 👑 LISTA DE ADMINS (Ninguém desta lista morre)
local ADMINS = {
    ["MAURO1928282"] = true,
    ["LiveYoug9909_BR"] = true,
    ["LUCARIOsinnoh33"] = true,
}

-- Criar a interface no CoreGui (ficará sempre visível)
local gui = Instance.new("ScreenGui")
gui.Name = "AdminPanel"
gui.ResetOnSpawn = false
gui.Parent = game:GetService("CoreGui") -- Delta permite acesso aqui

local botao = Instance.new("TextButton")
botao.Size = UDim2.new(0, 200, 0, 50)
botao.Position = UDim2.new(0.5, -100, 0.05, 0)
botao.Text = "Max Hub" -- Nome alterado conforme solicitado
botao.BackgroundColor3 = Color3.fromRGB(0, 0, 255) -- Fundo Azul
botao.TextColor3 = Color3.fromRGB(255, 255, 255)
botao.Font = Enum.Font.SourceSansBold
botao.TextScaled = true
botao.Parent = gui

-- Função que força a morte do personagem
local function matarPlayer(player)
    if player.Character and player.Character:FindFirstChild("Humanoid") then
        local hum = player.Character.Humanoid
        -- Primeiro força a vida a 0, depois força o estado para MORTO
        hum.Health = 0
        hum:ChangeState(Enum.HumanoidStateType.Dead)
    end
end

-- Ação do Botão
botao.MouseButton1Click:Connect(function()
    for _, p in pairs(Players:GetPlayers()) do
        -- Verifica se o jogador NÃO é admin e não é você
        if not ADMINS[p.Name] and p ~= LocalPlayer then
            matarPlayer(p)
        end
    end
end)
