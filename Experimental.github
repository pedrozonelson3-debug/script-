--========================================================
-- ROBLOX MOBILE HUB - MULTI-SECCIÓN (FREECAM TOGGLE)
--========================================================

local Players = game:GetService("Players")
local CoreGui = game:GetService("CoreGui")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local LocalPlayer = Players.LocalPlayer
local Camera = workspace.CurrentCamera

local FREECAM_URL = "https://rawscripts.net/raw/Universal-Script-universal-freecam-open-src-229296"
local F3X_URL = "https://rawscripts.net/raw/Universal-Script-F3X-Tool-44387"

-- Limpiar interfaz previa
pcall(function()
    local old = CoreGui:FindFirstChild("UnifiedMobileHubV2")
    if old then old:Destroy() end
end)

local gui = Instance.new("ScreenGui")
gui.Name = "UnifiedMobileHubV2"
gui.ResetOnSpawn = false
pcall(function() gui.Parent = CoreGui end)
if not gui.Parent then gui.Parent = LocalPlayer:WaitForChild("PlayerGui") end

-- Funciones de diseño base
local function corner(instance, radius)
    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0, radius or 8)
    c.Parent = instance
    return c
end

local function stroke(instance, color, thickness)
    local s = Instance.new("UIStroke")
    s.Color = color or Color3.fromRGB(255, 170, 0)
    s.Thickness = thickness or 1
    s.Parent = instance
    return s
end

--========================================================
-- VENTANA PRINCIPAL
--========================================================

local main = Instance.new("Frame")
main.Size = UDim2.new(0, 300, 0, 340)
main.Position = UDim2.new(0.5, -150, 0.3, 0)
main.BackgroundColor3 = Color3.fromRGB(24, 25, 31)
main.BorderSizePixel = 0
main.Active = true
main.Draggable = true
main.Parent = gui

corner(main, 12)
stroke(main, Color3.fromRGB(255, 170, 0), 1.5)

-- Header
local header = Instance.new("Frame")
header.Size = UDim2.new(1, 0, 0, 40)
header.BackgroundColor3 = Color3.fromRGB(35, 36, 44)
header.BorderSizePixel = 0
header.Parent = main
corner(header, 10)

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, -50, 1, 0)
title.Position = UDim2.new(0, 12, 0, 0)
title.BackgroundTransparency = 1
title.Font = Enum.Font.GothamBold
title.Text = "MOBILE HUB // V2"
title.TextColor3 = Color3.fromRGB(255, 190, 65)
title.TextSize = 14
title.TextXAlignment = Enum.TextXAlignment.Left
title.Parent = header

local minimize = Instance.new("TextButton")
minimize.Size = UDim2.new(0, 28, 0, 26)
minimize.Position = UDim2.new(1, -34, 0, 7)
minimize.BackgroundColor3 = Color3.fromRGB(55, 56, 66)
minimize.Text = "—"
minimize.TextColor3 = Color3.new(1, 1, 1)
minimize.Font = Enum.Font.GothamBold
minimize.TextSize = 14
minimize.Parent = header
corner(minimize, 6)

--========================================================
-- SISTEMA DE PESTAÑAS (TABS)
--========================================================

local tabContainer = Instance.new("Frame")
tabContainer.Size = UDim2.new(1, -16, 0, 32)
tabContainer.Position = UDim2.new(0, 8, 0, 46)
tabContainer.BackgroundTransparency = 1
tabContainer.Parent = main

local function createTabButton(name, positionX)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0.23, 0, 1, 0)
    btn.Position = UDim2.new(positionX, 0, 0, 0)
    btn.BackgroundColor3 = Color3.fromRGB(40, 42, 52)
    btn.Text = name
    btn.TextColor3 = Color3.fromRGB(200, 200, 210)
    btn.Font = Enum.Font.GothamBold
    btn.TextSize = 11
    btn.Parent = tabContainer
    corner(btn, 6)
    return btn
end

local tabHome = createTabButton("Home", 0)
local tabMove = createTabButton("Movilidad", 0.25)
local tabVisual = createTabButton("Visuales", 0.50)
local tabUtils = createTabButton("Utilidades", 0.75)

-- Contenedores de secciones (Páginas)
local function createPage()
    local p = Instance.new("ScrollingFrame")
    p.Size = UDim2.new(1, -16, 1, -95)
    p.Position = UDim2.new(0, 8, 0, 86)
    p.BackgroundTransparency = 1
    p.BorderSizePixel = 0
    p.CanvasSize = UDim2.new(0, 0, 0, 280)
    p.ScrollBarThickness = 4
    p.Visible = false
    p.Parent = main
    return p
end

local pageHome = createPage(); pageHome.Visible = true
local pageMove = createPage()
local pageVisual = createPage()
local pageUtils = createPage()

local function switchPage(activePage)
    pageHome.Visible = (pageHome == activePage)
    pageMove.Visible = (pageMove == activePage)
    pageVisual.Visible = (pageVisual == activePage)
    pageUtils.Visible = (pageUtils == activePage)
end

tabHome.MouseButton1Click:Connect(function() switchPage(pageHome) end)
tabMove.MouseButton1Click:Connect(function() switchPage(pageMove) end)
tabVisual.MouseButton1Click:Connect(function() switchPage(pageVisual) end)
tabUtils.MouseButton1Click:Connect(function() switchPage(pageUtils) end)

--========================================================
-- CONTENIDO DE CADA SECCIÓN
--========================================================

local function addMenuButton(parent, text, yPos, callback)
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(1, 0, 0, 38)
    b.Position = UDim2.new(0, 0, 0, yPos)
    b.BackgroundColor3 = Color3.fromRGB(45, 47, 58)
    b.Font = Enum.Font.GothamBold
    b.Text = text
    b.TextColor3 = Color3.fromRGB(245, 245, 250)
    b.TextSize = 12
    b.Parent = parent
    corner(b, 7)
    
    b.MouseButton1Click:Connect(function()
        callback(b)
    end)
    return b
end

-- --- PÁGINA HOME (CON FREECAM TOGGLE) ---
local statusHome = Instance.new("TextLabel")
statusHome.Size = UDim2.new(1, 0, 0, 30)
statusHome.Position = UDim2.new(0, 0, 0, 5)
statusHome.BackgroundTransparency = 1
statusHome.Font = Enum.Font.Gotham
statusHome.Text = "Estado: Todo operando correctamente"
statusHome.TextColor3 = Color3.fromRGB(170, 175, 185)
statusHome.TextSize = 11
statusHome.Parent = pageHome

local freecamActive = false
local freecamSnapshot = {}

local function getContainers()
    local result = {}
    local pg = LocalPlayer:FindFirstChildOfClass("PlayerGui")
    local backpack = LocalPlayer:FindFirstChildOfClass("Backpack")
    if pg then table.insert(result, pg) end
    if backpack then table.insert(result, backpack) end
    if LocalPlayer.Character then table.insert(result, LocalPlayer.Character) end
    pcall(function() table.insert(result, CoreGui) end)
    return result
end

local function snapshotObjects()
    local seen = {}
    for _, container in ipairs(getContainers()) do
        local ok, children = pcall(function() return container:GetChildren() end)
        if ok then
            for _, child in ipairs(children) do seen[child] = true end
        end
    end
    return seen
end

addMenuButton(pageHome, "📷 Freecam Externa: APAGADO", 45, function(btn)
    if freecamActive then
        -- Apagar y limpiar Freecam
        local removed = 0
        for _, container in ipairs(getContainers()) do
            local ok, children = pcall(function() return container:GetChildren() end)
            if ok then
                for _, child in ipairs(children) do
                    if not freecamSnapshot[child] then
                        local name = string.lower(child.Name)
                        if child:IsA("ScreenGui") and (name:find("freecam") or name:find("camera")) then
                            pcall(function() child:Destroy() end)
                            removed = removed + 1
                        end
                    end
                end
            end
        end
        freecamActive = false
        freecamSnapshot = {}
        btn.Text = "📷 Freecam Externa: APAGADO"
        btn.BackgroundColor3 = Color3.fromRGB(45, 47, 58)
        statusHome.Text = "Freecam apagada (" .. removed .. " elementos eliminados)"
    else
        -- Encender Freecam
        statusHome.Text = "Cargando Freecam..."
        local before = snapshotObjects()
        local ok, err = pcall(function()
            local source = game:HttpGet(FREECAM_URL)
            loadstring(source)()
        end)
        
        if ok then
            freecamSnapshot = before
            freecamActive = true
            btn.Text = "🟢 Freecam Externa: ENCENDIDO"
            btn.BackgroundColor3 = Color3.fromRGB(40, 135, 75)
            statusHome.Text = "Freecam activada. Pulsa otra vez para apagar."
        else
            statusHome.Text = "Error al cargar Freecam"
            warn("[Hub] Freecam error: " .. tostring(err))
        end
    end
end)

addMenuButton(pageHome, "🧰 Cargar F3X Building", 90, function()
    statusHome.Text = "Cargando F3X..."
    pcall(function() loadstring(game:HttpGet(F3X_URL))() end)
    statusHome.Text = "F3X ejecutado."
end)


-- --- PÁGINA MOVILIDAD ---
local noclipEnabled = false
RunService.Stepped:Connect(function()
    if noclipEnabled and LocalPlayer.Character then
        for _, part in ipairs(LocalPlayer.Character:GetDescendants()) do
            if part:IsA("BasePart") then
                part.CanCollide = false
            end
        end
    end
end)

addMenuButton(pageMove, "👻 Noclip (Atravesar Paredes): OFF", 5, function(btn)
    noclipEnabled = not noclipEnabled
    btn.Text = "👻 Noclip: " .. (noclipEnabled and "ON (Activo)" or "OFF")
    btn.BackgroundColor3 = noclipEnabled and Color3.fromRGB(40, 135, 75) or Color3.fromRGB(45, 47, 58)
end)

local speedEnabled = false
addMenuButton(pageMove, "⚡ Velocidad Rápida (WalkSpeed: 50)", 48, function(btn)
    speedEnabled = not speedEnabled
    if LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass("Humanoid") then
        LocalPlayer.Character:FindFirstChildOfClass("Humanoid").WalkSpeed = speedEnabled and 50 or 16
    end
    btn.Text = "⚡ Velocidad: " .. (speedEnabled and "50" or "16 (Normal)")
    btn.BackgroundColor3 = speedEnabled and Color3.fromRGB(40, 135, 75) or Color3.fromRGB(45, 47, 58)
end)

local jumpEnabled = false
addMenuButton(pageMove, "🦘 Super Salto (JumpPower: 100)", 91, function(btn)
    jumpEnabled = not jumpEnabled
    local hum = LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
    if hum then
        hum.UseJumpPower = true
        hum.JumpPower = jumpEnabled and 100 or 50
    end
    btn.Text = "🦘 Super Salto: " .. (jumpEnabled and "100" or "50 (Normal)")
    btn.BackgroundColor3 = jumpEnabled and Color3.fromRGB(40, 135, 75) or Color3.fromRGB(45, 47, 58)
end)


-- --- PÁGINA VISUALES (ESP NPCS) ---
local espEnabled = false
local trackedModels = {}

local function clearESP()
    for model, data in pairs(trackedModels) do
        if data.Highlight then pcall(function() data.Highlight:Destroy() end) end
        if data.Billboard then pcall(function() data.Billboard:Destroy() end) end
    end
    trackedModels = {}
end

local function getMainPart(model)
    return model.PrimaryPart 
        or model:FindFirstChild("HumanoidRootPart") 
        or model:FindFirstChild("Torso") 
        or model:FindFirstChild("UpperTorso") 
        or model:FindFirstChild("Head") 
        or model:FindFirstChildOfClass("BasePart")
end

task.spawn(function()
    while gui.Parent do
        if espEnabled then
            for _, obj in ipairs(workspace:GetChildren()) do
                if obj:IsA("Model") and not Players:GetPlayerFromCharacter(obj) and obj ~= LocalPlayer.Character then
                    local part = getMainPart(obj)
                    if part and not trackedModels[obj] then
                        local highlight = Instance.new("Highlight")
                        highlight.Name = "Universal_Highlight"
                        highlight.FillColor = Color3.fromRGB(255, 170, 0)
                        highlight.FillTransparency = 0.4
                        highlight.OutlineColor = Color3.fromRGB(255, 255, 255)
                        highlight.Enabled = false
                        highlight.Adornee = obj
                        highlight.Parent = obj

                        local billboard = Instance.new("BillboardGui")
                        billboard.Name = "Universal_Name"
                        billboard.Adornee = part
                        billboard.Size = UDim2.new(0, 100, 0, 30)
                        billboard.StudsOffset = Vector3.new(0, 2, 0)
                        billboard.AlwaysOnTop = true
                        billboard.Enabled = false

                        local label = Instance.new("TextLabel")
                        label.Size = UDim2.new(1, 0, 1, 0)
                        label.BackgroundTransparency = 1
                        label.TextColor3 = Color3.fromRGB(255, 215, 0)
                        label.TextStrokeTransparency = 0
                        label.Font = Enum.Font.GothamBold
                        label.TextSize = 12
                        label.Parent = billboard
                        billboard.Parent = part

                        trackedModels[obj] = {
                            Highlight = highlight,
                            Billboard = billboard,
                            Label = label,
                            Part = part,
                            LastPos = part.Position
                        }
                    end
                end
            end

            for model, data in pairs(trackedModels) do
                if model and model.Parent and data.Part and data.Part.Parent then
                    local currentPos = data.Part.Position
                    local distanceMoved = (currentPos - data.LastPos).Magnitude
                    
                    if distanceMoved > 0.1 then
                        data.Highlight.Enabled = true
                        data.Billboard.Enabled = true
                        
                        if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
                            local myPos = LocalPlayer.Character.HumanoidRootPart.Position
                            local dist = math.floor((myPos - currentPos).Magnitude)
                            data.Label.Text = "NPC [" .. dist .. "m]"
                        end
                    else
                        data.Highlight.Enabled = false
                        data.Billboard.Enabled = false
                    end
                    
                    data.LastPos = currentPos
                else
                    trackedModels[model] = nil
                end
            end
        end
        task.wait(0.2)
    end
    clearESP()
end)

addMenuButton(pageVisual, "🟠 ESP NPCs (Motion): APAGADO", 5, function(btn)
    espEnabled = not espEnabled
    if espEnabled then
        btn.Text = "🟢 ESP NPCs (Motion): ENCENDIDO"
        btn.BackgroundColor3 = Color3.fromRGB(40, 135, 75)
    else
        btn.Text = "🟠 ESP NPCs (Motion): APAGADO"
        btn.BackgroundColor3 = Color3.fromRGB(45, 47, 58)
        clearESP()
    end
end)

local fullbrightOn = false
addMenuButton(pageVisual, "☀️ Fullbright: OFF", 48, function(btn)
    fullbrightOn = not fullbrightOn
    local lighting = game:GetService("Lighting")
    lighting.Brightness = fullbrightOn and 3 or 1
    lighting.GlobalShadows = not fullbrightOn
    btn.Text = "☀️ Fullbright: " .. (fullbrightOn and "ON" or "OFF")
    btn.BackgroundColor3 = fullbrightOn and Color3.fromRGB(40, 135, 75) or Color3.fromRGB(45, 47, 58)
end)

local fovOn = false
addMenuButton(pageVisual, "🔍 Campo de Visión (FOV: 100)", 91, function(btn)
    fovOn = not fovOn
    Camera.FieldOfView = fovOn and 100 or 70
    btn.Text = "🔍 FOV Amplio: " .. (fovOn and "100" or "70")
    btn.BackgroundColor3 = fovOn and Color3.fromRGB(40, 135, 75) or Color3.fromRGB(45, 47, 58)
end)


-- --- PÁGINA UTILIDADES ---
addMenuButton(pageUtils, "🔄 Rejoin (Reconectar al Servidor)", 5, function()
    game:GetService("TeleportService"):TeleportToPlaceInstance(game.PlaceId, game.JobId, LocalPlayer)
end)

local antiAfkOn = false
addMenuButton(pageUtils, "🛡️ Anti-AFK: OFF", 48, function(btn)
    antiAfkOn = not antiAfkOn
    if antiAfkOn then
        local vu = game:GetService("VirtualUser")
        LocalPlayer.Idled:Connect(function()
            if antiAfkOn then
                vu:Button2Down(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
                task.wait(1)
                vu:Button2Up(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
            end
        end)
    end
    btn.Text = "🛡️ Anti-AFK: " .. (antiAfkOn and "ON" or "OFF")
    btn.BackgroundColor3 = antiAfkOn and Color3.fromRGB(40, 135, 75) or Color3.fromRGB(45, 47, 58)
end)


--========================================================
-- BURBUJA FLOTANTE PARA MINIMIZAR
--========================================================

local bubble = Instance.new("TextButton")
bubble.Size = UDim2.new(0, 45, 0, 45)
bubble.Position = UDim2.new(0.04, 0, 0.35, 0)
bubble.BackgroundColor3 = Color3.fromRGB(25, 26, 32)
bubble.Text = "HUB"
bubble.TextColor3 = Color3.fromRGB(255, 190, 65)
bubble.Font = Enum.Font.GothamBold
bubble.TextSize = 11
bubble.Visible = false
bubble.Active = true
bubble.Draggable = true
bubble.Parent = gui
corner(bubble, 22)
stroke(bubble, Color3.fromRGB(255, 170, 0), 2)

minimize.MouseButton1Click:Connect(function()
    main.Visible = false
    bubble.Visible = true
end)

bubble.MouseButton1Click:Connect(function`())
    bubble.Visible = false
    main.Visible = true
end)
