if game.PlaceId == 131667667758514 then
    local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

    local Window = Rayfield:CreateWindow({
        Name = "PLuTo Script",
        LoadingTitle = "PLuTo Development Team",
        LoadingSubtitle = "by PLuTo Team",
        ConfigurationSaving = {
            Enabled = false,
            FolderName = nil, -- Create a custom folder for your hub/game
            FileName = "Big Hub"
        },
        Discord = {
            Enabled = false,
            Invite = "https://discord.gg/dRv4R96Mtj", -- The Discord invite code, do not include discord.gg/
            RememberJoins = true -- Set this to false to make them join the discord every time they load it up
        },
        KeySystem = false, -- Set this to true to use our key system
        KeySettings = {
            Title = "PLuTo Key System",
            Subtitle = "Key System",
            Note = "Join the discord (https://discord.gg/dRv4R96Mtj)",
            FileName = "SiriusKey",
            SaveKey = true,
            GrabKeyFromSite = false, -- If this is true, set Key below to the RAW site you would like Rayfield to get the key from
            Key = "Hello"
        }
    })
    local MainTab = Window:CreateTab("Home", nil) -- Title, Image
    local MainSection = MainTab:CreateSection("Auto Farm")

    local ReplicatedStorage = game:GetService("ReplicatedStorage")
    local Remotes = ReplicatedStorage:WaitForChild("Remotes")

    local RecieveCash = Remotes:WaitForChild("RecieveCash")
    local RecieveOnHoldCash = Remotes:WaitForChild("RecieveOnHoldCash")

    local FIRE_INTERVAL = 0.1
    local AUTO_COIN_ENABLED = false
    local currentLoopTask = nil

    local function startAutoCoin()
        while AUTO_COIN_ENABLED do
            local success, err = pcall(function()
                RecieveCash:FireServer()
                RecieveOnHoldCash:FireServer()
            end)
            if not success then
                warn("Auto Coin error:", err) -- Optional: Log errors for debugging
            end
            task.wait(FIRE_INTERVAL)
        end
        currentLoopTask = nil
    end
    local function toggleAutoCoin(enabled)
        AUTO_COIN_ENABLED = enabled
        if enabled then
            if currentLoopTask == nil then
                currentLoopTask = task.spawn(startAutoCoin)
            end
        else
            if currentLoopTask then
                task.cancel(currentLoopTask) -- Immediately stop the task if running
                currentLoopTask = nil
            end
        end
    end
    local Toggle = MainTab:CreateToggle({
        Name = "Auto Coin",
        CurrentValue = false,
        Flag = "AutoCoinFlag", -- Optional: Saves state across sessions if config saving is enabled
        Callback = function(Value)
            toggleAutoCoin(Value) -- Value is the new toggle state (true/false)
        end,
    })
end
