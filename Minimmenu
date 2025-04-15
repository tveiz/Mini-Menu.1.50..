-- FunÃ§Ã£o para deletar todas as NotifyGui
local function deletarNotifyGui()
  local playerGui = game.Players.LocalPlayer:WaitForChild("PlayerGui")
  for _, gui in ipairs(playerGui:GetChildren()) do
    if gui.Name == "NotifyGui" and gui:IsA("ScreenGui") then
      gui:Destroy() -- Deleta a NotifyGui
    end
  end
end

-- Lista de itens para pegar
local itens = { "AK47", "Uzi", "PARAFAL", "Faca", "IA2", "G3", "Hi Power", "Natalina", "AR-15", "C4", "Escudo", "Glock 17" }

-- Argumentos para a requisiÃ§Ã£o (prÃ©-alocado e reutilizado)
local args = {
  [1] = "mudaInv",
  [2] = "2", -- Slot (vai ser alterado no loop)
  [3] = "ItemName", -- Item (vai ser alterado no loop)
  [4] = "1"
}

-- Evita executar em servidores
if game:GetService("RunService"):IsClient() then

  -- Loop principal em uma coroutine para evitar travar o jogo
  coroutine.wrap(function()
    while true do
      -- Deletar todas as NotifyGui antes de pegar os itens
      deletarNotifyGui()

      -- Pegar itens
      for i, item in ipairs(itens) do
        if i <= 16 then -- SÃ³ tenta alocar atÃ© 16 slots
          args[3] = item -- Atualiza o item para o valor da vez
          args[2] = tostring(i) -- Atribui o slot dinamicamente (1, 2, 3, ..., 16)

          -- Usar task.spawn() para execuÃ§Ã£o sem delay (importante para mobile)
          task.spawn(function()
            -- Tenta pegar o serviÃ§o ReplicatedStorage
            local replicatedStorage = game:GetService("ReplicatedStorage")
            if replicatedStorage then
              -- Tenta pegar os mÃ³dulos dentro de ReplicatedStorage
              local modules = replicatedStorage:FindFirstChild("Modules")
              if modules then
                  --Tenta pegar InvRemotes
                  local InvRemotes = modules:FindFirstChild("InvRemotes")
                  if InvRemotes then
                      -- Tenta pegar InvRequest
                      local InvRequest = InvRemotes:FindFirstChild("InvRequest")
                      if InvRequest then
                        -- Envia a requisiÃ§Ã£o para o servidor com tratamento de erro
                        pcall(function()
                          InvRequest:InvokeServer(unpack(args))
                        end)
                      else
                        warn("InvRequest nÃ£o encontrado")
                      end
                  else
                    warn("InvRemotes nÃ£o encontrado")
                  end
              else
                  warn("Modules nÃ£o encontrado")
              end
            else
              warn("ReplicatedStorage nÃ£o encontrado")
            end
          end)
        end
      end

      task.wait(0.1) -- Espera um curto perÃ­odo para evitar uso excessivo de CPU (mais importante para mobile)
    end
  end)() -- Inicia a coroutine imediatamente

end
