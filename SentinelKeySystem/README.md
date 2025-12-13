# SentinelUI Key System v0.32

---

| Field | Type | Description |
|-------|------|-------------|
| **GUIAnimations** | boolean | Toggles UI tween animations (WORK IN PROGRESS). |
| **KeyLink** | string | URL copied when the user clicks "Get Key". |
| **Keyless** | boolean | If true, bypasses key verification. |
| **MainLoader** | function or nil | Function executed after successful login. |

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

--Images

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

## Notify

SentinelUI.Notify(--creates a notification (string)
Title = "Notification" (string) 
Description = "content" (string) 
Duration = 5 // Seconds
Type = "info" // "success" | "warn" | "alert"

---

# EXAMPLE SCRIPT

```lua
local SentinelUI = loadstring(game:HttpGet("https://raw.githubusercontent.com/AsuraXowner/Sentinel-Open-Source/refs/heads/main/SentinelKeySystem/Installer.lua"))()
local AuthorizeToken = crypt.hash(tick()..tostring(math.random()), "sha256")--dont change this

--SentinelUI.Keys.MainTitle = "Your KeySystem name"
--SentinelUI.Keys.MainDesc = "Your KeySystem description"
--SentinelUI.Keys.Assets.Logo = "rbxassetid://101364305979184"--ASSET ID key system logo if u wish to use getcustomasset u need to buy source

local function Load()
    print("runs the code!")--your script here
end

SentinelUI.Initialize({
    KeyLink = "",
    Token = AuthorizeToken,
    MainLoader = Load,
    Function = function(v)--returns textbox text
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
