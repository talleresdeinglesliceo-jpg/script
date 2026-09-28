
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local CoreGui = game:GetService("CoreGui")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local Camera = workspace.CurrentCamera
local LocalPlayer = Players.LocalPlayer

if CoreGui:FindFirstChild("LuxedHUD") then
    CoreGui.LuxedHUD:Destroy()
end

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "LuxedHUD"
screenGui.ResetOnSpawn = false
screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
screenGui.Parent = CoreGui

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 240, 0, 115)
frame.AnchorPoint = Vector2.new(0.5, 0)
frame.Position = UDim2.new(0.5, 0, 0, 15)
frame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
frame.BackgroundTransparency = 0.35
frame.BorderSizePixel = 0
frame.Parent = screenGui

local uiCorner = Instance.new("UICorner")
uiCorner.CornerRadius = UDim.new(0, 10)
uiCorner.Parent = frame

local titleLabel = Instance.new("TextLabel")
titleLabel.Size = UDim2.new(1, -30, 0, 25)
titleLabel.Position = UDim2.new(0, 10, 0, 5)
titleLabel.BackgroundTransparency = 1
titleLabel.Font = Enum.Font.GothamBold
titleLabel.Text = "⚡ LUXED HUD"
titleLabel.TextColor3 = Color3.fromRGB(0, 150, 255)
titleLabel.TextSize = 13
titleLabel.TextXAlignment = Enum.TextXAlignment.Left
titleLabel.Parent = frame

local combatLabel = Instance.new("TextLabel")
combatLabel.Size = UDim2.new(1, -20, 0, 22)
combatLabel.Position = UDim2.new(0, 10, 0, 32)
combatLabel.BackgroundTransparency = 1
combatLabel.Font = Enum.Font.GothamBold
combatLabel.Text = "⚔️ [ COMBAT TAB ]"
combatLabel.TextColor3 = Color3.fromRGB(0, 150, 255)
combatLabel.TextSize = 11
combatLabel.TextXAlignment = Enum.TextXAlignment.Center
combatLabel.Parent = frame

local silentContainer = Instance.new("Frame")
silentContainer.Size = UDim2.new(1, -20, 0, 30)
silentContainer.Position = UDim2.new(0, 10, 0, 65)
silentContainer.BackgroundTransparency = 1
silentContainer.Parent = frame

local silentText = Instance.new("TextLabel")
silentText.Size = UDim2.new(0, 120, 1, 0)
silentText.Position = UDim2.new(0, 0, 0, 0)
silentText.BackgroundTransparency = 1
silentText.Font = Enum.Font.GothamSemibold
silentText.Text = "Silent Aim"
silentText.TextColor3 = Color3.fromRGB(255, 255, 255)
silentText.TextSize = 11
silentText.TextXAlignment = Enum.TextXAlignment.Left
silentText.Parent = silentContainer

local toggleSwitch = Instance.new("TextButton")
toggleSwitch.Size = UDim2.new(0, 48, 0, 24)
toggleSwitch.Position = UDim2.new(1, -48, 0.5, -12)
toggleSwitch.BackgroundColor3 = Color3.fromRGB(0, 150, 255)
toggleSwitch.AutoButtonColor = false
toggleSwitch.Text = ""
toggleSwitch.Parent = silentContainer

local switchCorner = Instance.new("UICorner")
switchCorner.CornerRadius = UDim.new(1, 0)
switchCorner.Parent = toggleSwitch

local switchKnob = Instance.new("Frame")
switchKnob.Size = UDim2.new(0, 20, 0, 20)
switchKnob.Position = UDim2.new(1, -22, 0.5, -10)
switchKnob.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
switchKnob.Parent = toggleSwitch

local knobCorner = Instance.new("UICorner")
knobCorner.CornerRadius = UDim.new(1, 0)
knobCorner.Parent = switchKnob

local silentActive = true

toggleSwitch.MouseButton1Click:Connect(function()
    silentActive = not silentActive
    local info = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    
    if silentActive then
        TweenService:Create(toggleSwitch, info, {BackgroundColor3 = Color3.fromRGB(0, 150, 255)}):Play()
        TweenService:Create(switchKnob, info, {Position = UDim2.new(1, -22, 0.5, -10)}):Play()
    else
        TweenService:Create(toggleSwitch, info, {BackgroundColor3 = Color3.fromRGB(60, 60, 60)}):Play()
        TweenService:Create(switchKnob, info, {Position = UDim2.new(0, 2, 0.5, -10)}):Play()
    end
end)

local toggleBtn = Instance.new("TextButton")
toggleBtn.Size = UDim2.new(0, 24, 0, 24)
toggleBtn.Position = UDim2.new(1, -28, 0, 5)
toggleBtn.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
toggleBtn.BackgroundTransparency = 0.3
toggleBtn.Font = Enum.Font.GothamBold
toggleBtn.Text = "-"
toggleBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
toggleBtn.TextSize = 14
toggleBtn.Parent = frame

local btnCorner = Instance.new("UICorner")
btnCorner.CornerRadius = UDim.new(0, 6)
btnCorner.Parent = toggleBtn

local isMinimized = false

toggleBtn.MouseButton1Click:Connect(function()
    isMinimized = not isMinimized
    local info = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    
    if isMinimized then
        combatLabel.Visible = false
        silentContainer.Visible = false
        titleLabel.Visible = false
        
        TweenService:Create(frame, info, {Size = UDim2.new(0, 100, 0, 34)}):Play()
        toggleBtn.Text = "+"
        TweenService:Create(toggleBtn, info, {Position = UDim2.new(0.5, -12, 0.5, -12)}):Play()
    else
        TweenService:Create(frame, info, {Size = UDim2.new(0, 240, 0, 115)}):Play()
        toggleBtn.Text = "-"
        TweenService:Create(toggleBtn, info, {Position = UDim2.new(1, -28, 0, 5)}):Play()
        
        task.wait(0.15)
        titleLabel.Visible = true
        combatLabel.Visible = true
        silentContainer.Visible = true
    end
end)

-- Restringido estrictamente al Torso (HumanoidRootPart / UpperTorso / LowerTorso)
local function getClosestTarget()
    local closestTarget = nil
    local shortestDistance = math.huge
    local mousePos = UserInputService:GetMouseLocation()

    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Character then
            local humanoid = player.Character:FindFirstChildOfClass("Humanoid")
            local torso = player.Character:FindFirstChild("HumanoidRootPart") 
                       or player.Character:FindFirstChild("UpperTorso") 
                       or player.Character:FindFirstChild("LowerTorso")
            
            if humanoid and humanoid.Health > 0 and torso then
                local screenPos, onScreen = Camera:WorldToViewportPoint(torso.Position)
                if onScreen then
                    local distance = (Vector2.new(screenPos.X, screenPos.Y) - mousePos).Magnitude
                    if distance < shortestDistance then
                        shortestDistance = distance
                        closestTarget = torso
                    end
                end
            end
        end
    end
    
    return closestTarget
end

local oldNamecall
oldNamecall = hookmetamethod(game, "__namecall", function(self, ...)
    local method = getnamecallmethod()
    local args = {...}
    
    if silentActive and (method == "FireServer" or method == "InvokeServer") then
        local target = getClosestTarget()
        if target then
            pcall(function()
                for i, v in ipairs(args) do
                    local t = typeof(v)
                    if t == "Vector3" then
                        args[i] = target.Position
                    elseif t == "CFrame" then
                        args[i] = CFrame.new(v.Position, target.Position)
                    elseif t == "Instance" and v:IsA("BasePart") then
                        args[i] = target
                    end
                end
            end)
            return oldNamecall(self, unpack(args))
        end
    end
    
    return oldNamecall(self, ...)
end)# script
