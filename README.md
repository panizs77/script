local player = game:GetService("Players").LocalPlayer
local backpack = player:FindFirstChild("Backpack")
local broom = backpack and backpack:FindFirstChild("Broom")
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:FindFirstChild("HumanoidRootPart")

local trashFolder = workspace["Trash"]
if not trashFolder then return end

local trashItems = trashFolder:GetChildren()
local virtualInputManager = game:GetService("VirtualInputManager")

if broom then
    broom.Equipped:Connect(function()
        for _, targetTrash in ipairs(trashItems) do
            if targetTrash and targetTrash:IsA("BasePart") then
                humanoidRootPart.CFrame = targetTrash.CFrame
                wait(0.5)
                virtualInputManager:SendKeyEvent(true, Enum.KeyCode.E, false, game)
                wait(0.1)
                virtualInputManager:SendKeyEvent(false, Enum.KeyCode.E, false, game)
            end
        end
    end)

    broom.Unequipped:Connect(function() end)
end
