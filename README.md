-- Configuração das variáveis principais
local player = game.Players.LocalPlayer
local farmArea = game.Workspace:WaitForChild("EnemyArea") -- Área com inimigos para farmar
local teleportKey = Enum.KeyCode.T -- A tecla para teleportar para uma área específica

-- Função para localizar inimigos próximos e atacá-los
function farmEnemies()
    local closestEnemy = nil
    local minDistance = math.huge
    
    -- Buscar inimigos na área de farm
    for _, enemy in pairs(farmArea:GetChildren()) do
        if enemy:IsA("Model") and enemy:FindFirstChild("Humanoid") then
            local distance = (enemy.HumanoidRootPart.Position - player.Character.HumanoidRootPart.Position).Magnitude
            if distance < minDistance then
                closestEnemy = enemy
                minDistance = distance
            end
        end
    end
    
    -- Atacar o inimigo mais próximo
    if closestEnemy then
        -- Comandos para atacar o inimigo mais próximo (o código do ataque depende da fruta e do estilo de combate)
        -- Exemplo fictício de ataque (aqui você usaria um ataque real do jogo)
        player.Character.HumanoidRootPart.CFrame = closestEnemy.HumanoidRootPart.CFrame
        -- Acionar ataque de habilidade aqui (dependente da fruta do jogador)
        print("Atacando inimigo: " .. closestEnemy.Name)
    end
end

-- Função de teleport para baús de dinheiro (simulação de mecânica de viagem)
function teleportToChest()
    -- Aqui, um código de teleportação para uma localização específica no mapa
    local chestLocation = Vector3.new(500, 10, 500) -- Coordenadas fictícias para baú de dinheiro
    player.Character.HumanoidRootPart.CFrame = CFrame.new(chestLocation)
    print("Teleportando para baú...")
end

-- Monitorando a tecla pressionada para teleportar ou farmar
game:GetService("UserInputService").InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed then return end

    if input.KeyCode == teleportKey then
        teleportToChest()
    elseif input.KeyCode == Enum.KeyCode.F then
        farmEnemies()  -- 'F' para começar a farmar os inimigos
    end
end)
