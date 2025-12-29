# if _G.a then
    for a, a in pairs(_G.a) do
        a:Disconnect()
    end;
    _G.a = nil
end;

local b = nil;
repeat
    task.wait()
until game.Players.LocalPlayer;

a = game.Players.LocalPlayer;
local b = nil;
local b = nil;
local c = nil;
local d = nil;
local e = false;
local f = {}

-- Atualiza partes do personagem
local b = function()
    b = a.Character or a.CharacterAdded:Wait()
    c = b:WaitForChild("Humanoid")
    d = b:WaitForChild("HumanoidRootPart")
    f = {}
    for a, a in pairs(b:GetDescendants()) do
        if a:IsA("BasePart") and a.Transparency == 0 then
            f[# f + 1] = a
        end
    end
end;

-- Cria a GUI
local g = function()
    local a = Instance.new("ScreenGui")
    local btn = Instance.new("TextButton")
    
    btn.Size = UDim2.new(0, 100, 0, 50)
    btn.Position = UDim2.new(0.5, -50, 0.1, 0)
    
    -- Configurações visuais (Azul e Null Void)
    btn.Text = "Null Void"
    btn.BackgroundColor3 = Color3.fromRGB(0, 85, 255) -- Azul
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    
    btn.Parent = a;
    a.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
    
    -- SISTEMA DE ARRASTAR
    local isDragging = false
    local dragInput = nil
    local dragStart = nil
    local startPos = nil

    btn.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            isDragging = true
            dragStart = input.Position
            startPos = btn.Position
            
            input.Changed:Connect(function()
                if input.UserInputState == Enum.UserInputState.End then
                    isDragging = false
                end
            end)
        end
    end)

    btn.InputChanged:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
            dragInput = input
        end
    end)

    game:GetService("UserInputService").InputChanged:Connect(function(input)
        if input == dragInput and isDragging then
            local delta = input.Position - dragStart
            btn.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
        end
    end)

    btn.MouseButton1Click:Connect(function()
        e = not e;
        for k, v in pairs(f) do
            if v then v.Transparency = e and 0.5 or 0 end
        end
    end)
end;

b()
g()

local h = {}
h[1] = a:GetMouse().KeyDown:Connect(function(key)
    if key == "g" then 
        e = not e;
        for k, v in pairs(f) do
            if v then v.Transparency = e and 0.5 or 0 end
        end
    end
end)

h[2] = game:GetService("RunService").Heartbeat:Connect(function()
    if e and d and c then
        local a = d.CFrame;
        local b = c.CameraOffset;
        
        -- MUDANÇA AQUI: Positivo e 100 Trilhões
        -- 100.000.000.000.000
        local targetCF = a * CFrame.new(0, 100000000000000, 0) 
        
        d.CFrame = targetCF;
        c.CameraOffset = targetCF:ToObjectSpace(CFrame.new(a.Position)).Position;
        
        game:GetService("RunService").RenderStepped:Wait()
        
        d.CFrame = a;
        c.CameraOffset = b
    end
end)

a.CharacterAdded:Connect(function()
    e = false;
    b()
    g()
end)

_G.a = h
