# v00nz-undetectable-gui
Aaaaaaaaa. Very ep0k roblox gui by v00nz


-- Create the ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

-- Make the GUI draggable
local function makeDraggable(frame, handle)
    local dragging, dragInput, dragStart, startPos

    handle.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            dragging = true
            dragStart = input.Position
            startPos = frame.Position

            input.Changed:Connect(function()
                if input.UserInputState == Enum.UserInputState.End then
                    dragging = false
                end
            end)
        end
    end)

    handle.InputChanged:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseMovement then
            dragInput = input
        end
    end)

    game:GetService("UserInputService").InputChanged:Connect(function(input)
        if input == dragInput and dragging then
            local delta = input.Position - dragStart
            frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
        end
    end)
end

-- Create the main frame
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 400, 0, 600) -- Adjust size as needed
frame.Position = UDim2.new(0.5, -200, 0.5, -300) -- Centered
frame.BackgroundColor3 = Color3.fromRGB(0, 0, 0) -- Black background
frame.BorderColor3 = Color3.fromRGB(0, 255, 0) -- Green outline
frame.Parent = screenGui

-- Make the frame draggable
makeDraggable(frame, frame)

-- Create the title
local title = Instance.new("TextLabel")
title.Text = "v00nz undetectable gui v4"
title.Size = UDim2.new(1, 0, 0, 50)
title.Position = UDim2.new(0, 0, 0, 0)
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.BackgroundTransparency = 1
title.Font = Enum.Font.SourceSansBold
title.TextScaled = true
title.Parent = frame

-- Create the subtitle
local subText = Instance.new("TextLabel")
subText.Text = "xz00k/v00nz 'v4'"
subText.Size = UDim2.new(1, 0, 0, 30)
subText.Position = UDim2.new(0, 0, 0, 50)
subText.TextColor3 = Color3.fromRGB(255, 255, 255)
subText.BackgroundTransparency = 1
subText.Font = Enum.Font.SourceSans
subText.TextScaled = true
subText.Parent = frame

-- Button to apply ISIS decal
local function applyDecalToAllParts()
    local decalID = "rbxassetid://86906307951453"

    -- Function to apply decal to a part
    local function applyDecal(part)
        if part:IsA("BasePart") or part:IsA("Model") or part:IsA("UnionOperation") then
            local decal = Instance.new("Decal")
            decal.Texture = decalID
            decal.Parent = part
        end
    end

    -- Loop through all parts in the workspace
    for _, object in pairs(workspace:GetDescendants()) do
        if object:IsA("BasePart") or object:IsA("Model") then
            applyDecal(object)
        end
    end
end

-- Create the "ISIS Decal" button
local decalButton = Instance.new("TextButton")
decalButton.Text = "ISIS Decal"
decalButton.Size = UDim2.new(0, 150, 0, 40)
decalButton.Position = UDim2.new(0.5, -75, 0, 120)
decalButton.BackgroundColor3 = Color3.fromRGB(0, 0, 0) -- Black button
decalButton.BorderColor3 = Color3.fromRGB(255, 255, 255) -- White outline
decalButton.TextColor3 = Color3.fromRGB(255, 255, 255)
decalButton.Font = Enum.Font.SourceSansBold
decalButton.TextScaled = true
decalButton.Parent = frame

-- Connect the button click to the decal application
decalButton.MouseButton1Click:Connect(applyDecalToAllParts)
