loadstring(game:HttpGet("https://raw.githubusercontent.com/gumanba/Scripts/main/EscapeTsunamiForBrainrots"))()
--// Tạo GUI
local plr = game.Players.LocalPlayer
local gui = Instance.new("ScreenGui", plr:WaitForChild("PlayerGui"))
gui.ResetOnSpawn = false

-- Khung chính
local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0, 160, 0, 60)
frame.Position = UDim2.new(0, 20, 0, 100)
frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
frame.Active = true
frame.Draggable = true

local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1, 0, 0.4, 0)
title.BackgroundTransparency = 1
title.TextColor3 = Color3.fromRGB(255,255,255)
title.Text = "ANTI AFK"
title.TextSize = 18

local button = Instance.new("TextButton", frame)
button.Size = UDim2.new(1, -20, 0.45, 0)
button.Position = UDim2.new(0,10, 0.45, 0)
button.Text = "OFF"
button.BackgroundColor3 = Color3.fromRGB(120, 0, 0)
button.TextColor3 = Color3.fromRGB(255,255,255)
button.TextSize = 16

-- Biến Anti-AFK
local Enabled = false

-- Hàm mô phỏng hoạt động
local vu = game:GetService("VirtualUser")

button.MouseButton1Click:Connect(function()
    Enabled = not Enabled
    if Enabled then
        button.Text = "ON"
        button.BackgroundColor3 = Color3.fromRGB(0, 120, 0)
    else
        button.Text = "OFF"
        button.BackgroundColor3 = Color3.fromRGB(120, 0, 0)
    end
end)

-- Vòng lặp Anti-AFK
task.spawn(function()
    while true do
        if Enabled then
            vu:Button2Down(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
            task.wait(0.2)
            vu:Button2Up(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
        end
        task.wait(25) -- mô phỏng mỗi 25 giây
    end
end)
