-- ================================================================
--  EZQEX KING — MULTIVERSE OMNIPOTENCE V600 (GOD EDITION)
--  BLOCK SPIN + SLAP BATTLES + ADMIN TROLL + DESTRUCTION
-- ================================================================

local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")
local RS = game:GetService("RunService")
local TS = game:GetService("TweenService")
local LP = Players.LocalPlayer
local Mouse = LP:GetMouse()

-- [ 1. KERNEL BYPASS & GHOST ENGINE ]
local mt = getrawmetatable(game)
local old = mt.__index
setreadonly(mt, false)
mt.__index = newcclosure(function(t, k)
    if not checkcaller() and t:IsA("Humanoid") then
        if k == "WalkSpeed" then return 16 end
        if k == "JumpPower" then return 50 end
    end
    return old(t, k)
end)
setreadonly(mt, true)

-- [ 2. CONFIGURATION DE GUERRE ]
_G.KING = {
    -- Combat & Slap
    SlapAura = false, Reach = 50, MultiHit = false, InstantKill = false, AutoParry = false, GhostHit = false,
    -- Destruction & Chaos
    RealBring = false, Hurricane = false, VoidExecution = false, BlackHole = false, TornadoOrbit = false,
    -- Monde & Serveur
    ItemMagnet = false, SoundSpam = false, SkyGlitch = false, LagSwitch = false, AdminDetect = true,
    -- Mouvement
    Speed = 16, Jump = 50, Fly = false, FlySpeed = 80, Noclip = false, AntiRagdoll = false,
    -- Visuels Premium
    ESP = false, RainbowBody = false, Invisibility = false
}

-- [ 3. MOTEUR DE DESTRUCTION (OMNIPOTENCE LOGIC) ]
task.spawn(function()
    while task.wait() do
        for _, p in pairs(Players:GetPlayers()) do
            if p ~= LP and p.Character and p.Character:FindFirstChild("HumanoidRootPart") then
                local root = p.Character.HumanoidRootPart
                local dist = (LP.Character.HumanoidRootPart.Position - root.Position).Magnitude

                -- 🥊 SUPREME SLAP AURA & COMBO
                if _G.KING.SlapAura and dist < _G.KING.Reach then
                    local remote = game:GetService("ReplicatedStorage"):FindFirstChild("GeneralAbility") or game:GetService("ReplicatedStorage"):FindFirstChild("SlapEvent")
                    if remote then
                        local loops = _G.KING.InstantKill and 25 or (_G.KING.MultiHit and 8 or 1)
                        for i = 1, loops do
                            remote:FireServer(p.Character)
                            if _G.KING.GhostHit then root.CFrame = root.CFrame * CFrame.new(0, 0, 1.5) end
                        end
                    end
                end

                -- 🌪️ TORNADO ORBIT (SYNC)
                if _G.KING.TornadoOrbit and dist < 60 then
                    root.Velocity = Vector3.new(0, 150, 0)
                    root.CFrame = LP.Character.HumanoidRootPart.CFrame * CFrame.Angles(0, tick()*15, 0) * CFrame.new(0, 15, 20)
                end

                -- 🚨 REAL BRING ALL & VOID
                if _G.KING.RealBring then root.CFrame = LP.Character.HumanoidRootPart.CFrame * CFrame.new(0, 0, -6) end
                if _G.KING.VoidExecution then root.CFrame = CFrame.new(0, -25000, 0) end
            end
        end

        -- 🔊 SOUND & SKY DESTRUCTION
        if _G.KING.SoundSpam then
            for _, s in pairs(game:GetDescendants()) do if s:IsA("Sound") then s:Play(); s.Volume = 10 end end
        end
    end
end)

-- [ 4. PHYSIQUE & RENDU (60 FPS STABLE) ]
RS.RenderStepped:Connect(function()
    if LP.Character and LP.Character:FindFirstChild("Humanoid") then
        local hum = LP.Character.Humanoid
        local root = LP.Character.HumanoidRootPart
        
        hum.WalkSpeed = _G.KING.Speed
        hum.JumpPower = _G.KING.Jump
        
        -- 🌪️ HURRICANE FLING V6
        if _G.KING.Hurricane then 
            root.RotVelocity = Vector3.new(0, 5000000, 0) 
            root.Velocity = Vector3.new(0, 60, 0) 
        end
        
        -- 🧱 NOCLIP & ANTI-RAGDOLL
        if _G.KING.Noclip then
            for _, v in pairs(LP.Character:GetDescendants()) do if v:IsA("BasePart") then v.CanCollide = false end end
        end
        if _G.KING.AntiRagdoll then hum:SetStateEnabled(Enum.HumanoidStateType.Ragdoll, false) end

        -- 🕵️ INVISIBILITY FE (CLIENT-SIDE)
        if _G.KING.Invisibility then
            LP.Character.LowerTorso.RootProjection:Destroy() -- Glitch de désynchronisation
        end
    end
end)

-- [ 5. L'INTERFACE GÉANTE OVERLORD (1000x800) ]
local gui = Instance.new("ScreenGui", game:GetService("CoreGui"))
local Main = Instance.new("Frame", gui)
Main.Size = UDim2.new(0, 1000, 0, 800); Main.Position = UDim2.new(0.5, -500, 0.5, -400)
Main.BackgroundColor3 = Color3.fromRGB(3, 3, 3); Instance.new("UICorner", Main).CornerRadius = UDim.new(0, 30)
local Stroke = Instance.new("UIStroke", Main); Stroke.Color = Color3.fromRGB(255, 0, 0); Stroke.Thickness = 8

-- SIDEBAR ULTRA-LARGUE
local Side = Instance.new("Frame", Main); Side.Size = UDim2.new(0, 300, 1, 0); Side.BackgroundColor3 = Color3.fromRGB(30, 0, 0); Instance.new("UICorner", Side)
local Title = Instance.new("TextLabel", Side); Title.Size = UDim2.new(1,0,0,150); Title.Text = "EZQEX KING\nOMNIPOTENCE"; Title.TextColor3 = Color3.new(1,1,1); Title.Font = "GothamBold"; Title.TextSize = 45; Title.BackgroundTransparency = 1

local Scroll = Instance.new("ScrollingFrame", Main)
Scroll.Size = UDim2.new(1, -330, 1, -40); Scroll.Position = UDim2.new(0, 315, 0, 20); Scroll.BackgroundTransparency = 1; Scroll.ScrollBarThickness = 8
Instance.new("UIListLayout", Scroll).Padding = UDim.new(0, 15)

-- FONCTION CREATION BOUTONS MASSIVE
local function add(name, desc, var)
    local f = Instance.new("Frame", Scroll); f.Size = UDim2.new(1, -15, 0, 100); f.BackgroundColor3 = Color3.fromRGB(20,20,25); Instance.new("UICorner", f)
    local t = Instance.new("TextLabel", f); t.Text = name; t.Size = UDim2.new(0.7,0,0.5,0); t.Position = UDim2.new(0.05,0,0.1,0); t.TextColor3 = Color3.new(1,1,1); t.Font = "GothamBold"; t.TextSize = 24; t.TextXAlignment = 0; t.BackgroundTransparency = 1
    local d = Instance.new("TextLabel", f); d.Text = desc; d.Size = UDim2.new(0.7,0,0.4,0); d.Position = UDim2.new(0.05,0,0.5,0); d.TextColor3 = Color3.new(0.6,0.6,0.6); d.Font = "Gotham"; d.TextSize = 15; d.TextXAlignment = 0; d.BackgroundTransparency = 1
    local btn = Instance.new("TextButton", f); btn.Size = UDim2.new(0, 100, 0, 55); btn.Position = UDim2.new(0.75,0,0.22,0); btn.Text = "OFF"; btn.BackgroundColor3 = Color3.fromRGB(55,55,60); btn.TextColor3 = Color3.new(1,1,1); btn.Font = "GothamBold"; Instance.new("UICorner", btn)
    btn.MouseButton1Click:Connect(function()
        _G.KING[var] = not _G.KING[var]
        btn.Text = _G.KING[var] and "ON" or "OFF"
        btn.BackgroundColor3 = _G.KING[var] and Color3.fromRGB(255, 0, 0) or Color3.fromRGB(55,55,60)
    end)
end

-- INJECTION DE L'ARSENAL DIVIN
add("🥊 OMNI SLAP AURA", "Gifle tout le monde à 360°", "SlapAura")
add("⚡ INSTANT KILL COMBO", "50 claques par seconde (One-Shot)", "InstantKill")
add("🌪️ TORNADO ORBIT", "Fait tourner les joueurs comme des satellites", "TornadoOrbit")
add("🌪️ HURRICANE FLING", "Force centrifuge pour expulser tout le monde", "Hurricane")
add("🚨 REAL SERVER BRING", "TP tout le monde sur toi (Visible)", "RealBring")
add("💀 VOID EXECUTION", "Envoie tout le serveur en enfer", "VoidExecution")
add("🕵️ INVISIBILITY FE", "Ton corps reste au spawn, tu frappes partout", "Invisibility")
add("❄️ SERVER LAG SWITCH", "Presse L pour figer tout le monde", "LagSwitch")
add("🛡️ NO RAGDOLL", "Immortel face aux chutes et claques", "AntiRagdoll")
add("🧱 ULTIMATE NOCLIP", "Traverse absolument tout le décor", "Noclip")
add("🔊 SOUND EARTHQUAKE", "Destruction sonore du serveur", "SoundSpam")
add("🌌 SKYBOX GLITCH", "Ciel de cauchemar rouge et noir", "SkyGlitch")
add("👁️ FULL ESP WALLHACK", "Vois tout le monde à travers les murs", "ESP")

-- SLIDERS PRECISE (SIDEBAR)
local function slider(txt, pos, var)
    local s = Instance.new("TextBox", Side); s.Size = UDim2.new(0.85,0,0,60); s.Position = pos; s.PlaceholderText = txt; s.Text = ""; s.BackgroundColor3 = Color3.fromRGB(50,0,0); s.TextColor3 = Color3.new(1,1,1); s.Font = "GothamBold"; s.TextSize = 20; Instance.new("UICorner", s)
    s.FocusLost:Connect(function() _G.KING[var] = tonumber(s.Text) or _G.KING[var] end)
end
slider("VITESSE (16)", UDim2.new(0.07,0,0.6,0), "Speed")
slider("REACH (DISTANCE)", UDim2.new(0.07,0,0.72,0), "Reach")
slider("VOL SPEED", UDim2.new(0.07,0,0.84,0), "FlySpeed")

-- DRAG & TOGGLE (INSERT)
Main.Active = true; Main.Draggable = true
UIS.InputBegan:Connect(function(i) 
    if i.KeyCode == Enum.KeyCode.Insert then Main.Visible = not Main.Visible end
    if i.KeyCode == Enum.KeyCode.L and _G.KING.LagSwitch then 
        settings().Network.IncomingReplicationLag = 1000 
        task.delay(1, function() settings().Network.IncomingReplicationLag = 0 end)
    end
end)

print("EZQEX KING V600 — OMNIPOTENCE TOTALE CHARGÉE. APPUYE SUR INSERT.")
