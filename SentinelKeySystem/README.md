# SentinelUI Key System

---

| Field | Type | Description |
|-------|------|-------------|
| **GUIAnimations** | boolean | Toggles UI tween animations (WORK IN PROGRESS). |
| **KeyLink** | string | URL copied when the user clicks "Get Key". |
| **Keyless** | boolean | If true, bypasses key verification (WORK IN PROGRESS). |
| **MainLoader** | function or nil | Function executed after successful authorization. |

---

## Colors (Color3)

Dim = Color3.fromRGB(5, 5, 5)
LoaderBg = Color3.fromRGB(15, 15, 20)
ContentBg = Color3.fromRGB(0, 0, 0)

StrokeDark = Color3.fromRGB(23, 20, 33)
StrokeLight = Color3.fromRGB(29, 29, 29)
StrokeAccent = Color3.fromRGB(113, 56, 255)

TextWhite = Color3.fromRGB(255, 255, 255)
TextDim = Color3.fromRGB(220, 220, 220)
TextPlaceholder = Color3.fromRGB(68, 63, 79)

ButtonStatic = Color3.fromRGB(47, 47, 47)
InputBg = Color3.fromRGB(15, 15, 15)
InputBgVerify = Color3.fromRGB(94, 94, 94)

Primary = Color3.fromRGB(61, 55, 125)
AccentGradient1 = Color3.fromRGB(89, 67, 231)
AccentGradient2 = Color3.fromRGB(145, 99, 240)

IconNormal = Color3.fromRGB(203, 187, 255)
IconActive = Color3.fromRGB(241, 231, 255)
IconDim = Color3.fromRGB(169, 161, 255)

Success = Color3.fromRGB(83, 156, 70)
SuccessBg = Color3.fromRGB(10, 20, 8)

Fail = Color3.fromRGB(156, 63, 99)
FailBg = Color3.fromRGB(20, 9, 9)

NotificationBg = Color3.fromRGB(23, 23, 31)
NotificationText = Color3.fromRGB(180, 190, 255)

---

## Fonts

Main = Font.new("Nunito", Bold)
Header = Enum.Font.GothamBold
SubHeader = Enum.Font.GothamMedium
Simple = Enum.Font.SourceSans


---

## Assets

Key-value mapping of asset names to Roblox asset IDs.

Logo = "rbxassetid://101364305979184"
other images cant be changed.

---

## Settings

CornerRadius = UDim.new(0, 8) (WORK IN PROGRESS)
PillRadius = UDim.new(1, 0) (WORK IN PROGRESS)
AnimSpeed = 0.8 (WORK IN PROGRESS)
AnimStyle = Enum.EasingStyle.Exponential

Custom = {
Remember = true // default values on first launch
BackgroundTransparent = true // default values on first launch
}

---

## Updates

Updates = {
[1] = {
Version = "v0.4.0"
Date = "04.12.2024"
Updates = {
"tuff fire latest update",
"latest updates get more highlight",
}
}
}

---

# Initialize

```lua
SentinelUI.Initialize({
    KeyLink = "https://...",
    Keyless = false,
    Token = "SHA256_Hash",        -- REQUIRED
    MainLoader = function() end,  -- Runs after key is verified

    Function = function(InputKey)
        -- Must call one:
        -- SentinelUI.Authorize(Token)
        -- SentinelUI.Fail()
    end
})
SentinelUI.Notify

SentinelUI.Notify({
    Title = "Notification",
    Description = "Message",
    Duration = 5,
    Type = "info" -- success | warn | alert
})
SentinelUI.AddSettings

SentinelUI.AddSettings({
    Title = "Setting Name",
    Desc = "Description text",
    Default = true,
    Function = function(state)
        -- state = true/false
    end
})
SentinelUI.AddUpdate

SentinelUI.AddUpdate({
    Version = "v1.0.0",
    Date = "01.01.2025",
    Updates = {
        "Update 1",
        "Update 2"
    }
})
SentinelUI.AdjustTextbox

SentinelUI.AdjustTextbox("Success", 4)
Config Management

SentinelUI.SaveConfig()
SentinelUI.LoadConfig()
Example Script

local SentinelUI = loadstring(game:HttpGet(
    "https://raw.githubusercontent.com/AsuraXowner/Sentinel-Open-Source/refs/heads/main/SentinelKeySystem/Installer.lua"
))()

local AuthorizeToken = crypt.hash(tick()..tostring(math.random()), "sha256")

local function Load()
    print("runs the code!")
end

SentinelUI.Initialize({
    KeyLink = "",
    Token = AuthorizeToken,
    MainLoader = Load,
    Function = function(v)
        if v == "example_verify" then
            SentinelUI.Authorize(AuthorizeToken)
        else
            SentinelUI.Fail()
        end
    end
})

table.insert(SentinelUI.Keys.Updates, 3, {
    Version = "v0.5.0 (Custom)",
    Date = "09.12.2025",
    Updates = { "update1", "update2" }
})

SentinelUI.AddSettings({
    Title = "fire from mainscript",
    Desc = "432424",
    Default = true,
    Function = function(v)
        -- callback
    end
})
