repeat task.wait() until game:IsLoaded()

local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local TweenService = game:GetService("TweenService")

local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

if playerGui:FindFirstChild("Collector") then
    playerGui.Collector:Destroy()
end

local remote = ReplicatedStorage
    :WaitForChild("Packages")
    :WaitForChild("Networking")
    :WaitForChild("RE/Events/CollectEventSpawnable")

local RUNS = 30
local INTERVAL = 20
local isActive = false

local gui = Instance.new("ScreenGui")
gui.Name = "Collector"
gui.ResetOnSpawn = false
gui.Parent = playerGui

local toggleBtn = Instance.new("ImageButton") 
toggleBtn.Size = UDim2.new(0, 40, 0, 40)
toggleBtn.Position = UDim2.new(1, -50, 0, 10)
toggleBtn.Image = "rbxassetid://76521609207622" 
toggleBtn.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
toggleBtn.Parent = gui

local toggleCorner = Instance.new("UICorner")
toggleCorner.CornerRadius = UDim.new(1, 0)
toggleCorner.Parent = toggleBtn

local main = Instance.new("Frame")
main.Size = UDim2.new(0, 240, 0, 160)
main.Position = UDim2.new(0.5, -120, 0.5, -80)
main.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
main.BorderSizePixel = 0
main.Draggable = true
main.Active = true
main.Parent = gui

toggleBtn.MouseButton1Click:Connect(function()
    main.Visible = not main.Visible
end)

local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0, 10)
corner.Parent = main

local stroke = Instance.new("UIStroke")
stroke.Color = Color3.fromRGB(255, 255, 255)
stroke.Thickness = 1.5
stroke.Parent = main

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 30)
title.Position = UDim2.new(0, 0, 0, 15)
title.Text = "COLLECTOR"
title.TextColor3 = Color3.fromRGB(200, 200, 200)
title.BackgroundTransparency = 1
title.Font = Enum.Font.GothamBold
title.TextSize = 20
title.Parent = main

local status = Instance.new("TextLabel")
status.Size = UDim2.new(1, 0, 0, 22)
status.Position = UDim2.new(0, 0, 0, 50)
status.Text = "INACTIVO"
status.TextColor3 = Color3.fromRGB(255, 90, 90)
status.BackgroundTransparency = 1
status.Font = Enum.Font.GothamBold
status.TextSize = 14
status.Parent = main

local btn = Instance.new("TextButton")
btn.Size = UDim2.new(0.6, 0, 0, 36)
btn.Position = UDim2.new(0.2, 0, 0, 85)
btn.Text = "ACTIVAR"
btn.BackgroundColor3 = Color3.fromRGB(0, 150, 255)
btn.TextColor3 = Color3.fromRGB(255, 255, 255)
btn.Font = Enum.Font.GothamBold
btn.TextSize = 15
btn.Parent = main

local btnCorner = Instance.new("UICorner")
btnCorner.CornerRadius = UDim.new(0, 8)
btnCorner.Parent = btn

local credits = Instance.new("TextLabel")
credits.Size = UDim2.new(1, 0, 0, 20)
credits.Position = UDim2.new(0, 0, 0, 135)
credits.Text = "MADE-BY  INCÓGNITO"
credits.TextColor3 = Color3.fromRGB(255, 255, 255)
credits.BackgroundTransparency = 1
credits.Font = Enum.Font.Gotham
credits.TextSize = 10
credits.Parent = main

local loopConnection

local function collect()
    while isActive do
        for i = 1, RUNS do
            if not isActive then break end
            pcall(function() remote:FireServer() end)
            task.wait(0.1)
        end
        if isActive then task.wait(INTERVAL) end
    end
end

btn.MouseButton1Click:Connect(function()
    isActive = not isActive
    if isActive then
        btn.Text = "DESACTIVAR"
        btn.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
        status.Text = "ACTIVO"
        status.TextColor3 = Color3.fromRGB(90, 255, 90)
        loopConnection = task.spawn(collect)
    else
        btn.Text = "ACTIVAR"
        btn.BackgroundColor3 = Color3.fromRGB(0, 150, 255)
        status.Text = "INACTIVO"
        status.TextColor3 = Color3.fromRGB(255, 90, 90)
        if loopConnection then task.cancel(loopConnection) end
    end
end)

task.spawn(function()
    while gui.Parent do
        local tweenInfo = TweenInfo.new(1.5, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut)
        
        TweenService:Create(stroke, tweenInfo, {Color = Color3.fromRGB(255, 255, 255)}):Play()
        TweenService:Create(title, tweenInfo, {TextColor3 = Color3.fromRGB(255, 255, 255)}):Play()
        TweenService:Create(credits, tweenInfo, {TextColor3 = Color3.fromRGB(255, 255, 255)}):Play()
        task.wait(1.5)
        
        TweenService:Create(stroke, tweenInfo, {Color = Color3.fromRGB(50, 50, 50)}):Play()
        TweenService:Create(title, tweenInfo, {TextColor3 = Color3.fromRGB(0, 0, 0)}):Play()
        TweenService:Create(credits, tweenInfo, {TextColor3 = Color3.fromRGB(0, 0, 0)}):Play()
        task.wait(1.5)
    end
end)
