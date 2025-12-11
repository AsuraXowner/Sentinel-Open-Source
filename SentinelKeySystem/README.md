SentinelUI.Keys [
    (boolean) GUIAnimations = true // Toggles all UI tweens WORK IN PROGRESS
    (string) KeyLink = "https://bigrat.monster" // The link copied when 'Get Key' is clicked
    (boolean) Keyless = false // Bypasses the key system entirely WORK IN PROGRESS
    (function | nil) MainLoader = nil // The function to run after successful login

    Colors [ // All values are Color3
        (Color3) Dim = Color3.fromRGB(5, 5, 5) // Background overlay dim
        (Color3) LoaderBg = Color3.fromRGB(15, 15, 20) // Main card background
        (Color3) ContentBg = Color3.fromRGB(0, 0, 0) // Inner content container
        (Color3) StrokeDark = Color3.fromRGB(23, 20, 33) // Dark borders
        (Color3) StrokeLight = Color3.fromRGB(29, 29, 29) // Light borders
        (Color3) StrokeAccent = Color3.fromRGB(113, 56, 255) // Focused/Active borders
        (Color3) TextWhite = Color3.fromRGB(255, 255, 255) // Primary text
        (Color3) TextDim = Color3.fromRGB(220, 220, 220) // Secondary text
        (Color3) TextPlaceholder = Color3.fromRGB(68, 63, 79) // Input placeholders
        (Color3) ButtonStatic = Color3.fromRGB(47, 47, 47) // Button background
        (Color3) InputBg = Color3.fromRGB(15, 15, 15) // Textbox background
        (Color3) InputBgVerify = Color3.fromRGB(94, 94, 94) // Textbox background (Verifying)
        (Color3) Primary = Color3.fromRGB(61, 55, 125) // Main accent color
        (Color3) AccentGradient1 = Color3.fromRGB(89, 67, 231) // Gradient Start
        (Color3) AccentGradient2 = Color3.fromRGB(145, 99, 240) // Gradient End
        (Color3) IconNormal = Color3.fromRGB(203, 187, 255) // Default icon color
        (Color3) IconActive = Color3.fromRGB(241, 231, 255) // Hover/Active icon color
        (Color3) IconDim = Color3.fromRGB(169, 161, 255) // Dim/Disabled icon color
        (Color3) Success = Color3.fromRGB(83, 156, 70) // Success Status
        (Color3) SuccessBg = Color3.fromRGB(10, 20, 8) // Success Background
        (Color3) Fail = Color3.fromRGB(156, 63, 99) // Error Status
        (Color3) FailBg = Color3.fromRGB(20, 9, 9) // Error Background
        (Color3) NotificationBg = Color3.fromRGB(23, 23, 31) // Toast Background
        (Color3) NotificationText = Color3.fromRGB(180, 190, 255) // Toast Text
    ]

    Fonts [ // All values are Font instances or Enum.Font
        (Font) Main = Font.new("Nunito", Bold)
        (EnumItem) Header = Enum.Font.GothamBold
        (EnumItem) SubHeader = Enum.Font.GothamMedium
        (EnumItem) Simple = Enum.Font.SourceSans
    ]

    Assets [ // Key = Asset Name, Value = rbxassetid string
        (string) 'Logo' = 'rbxassetid://101364305979184'
    ]

    Settings [
        (UDim) CornerRadius = UDim.new(0, 8)  WORK IN PROGRESS
        (UDim) PillRadius = UDim.new(1, 0)  WORK IN PROGRESS
        (number) AnimSpeed = 0.8  WORK IN PROGRESS
        (EnumItem) AnimStyle = Enum.EasingStyle.Exponential
        
        Custom [
            (boolean) Remember = true // Auto-save/load key changes if user has settings but on first load it will use these
            (boolean) BackgroundTransparent = true // Makes background transparent on load if user has settings but on first load it will use these
        ]
    ]

    Updates [ // Table of Update Tables. Insert new updates here.
        [1] = {
            (string) Version = "v0.4.0"
            (string) Date = "04.12.2024" // DD.MM.YYYY
            (table) Updates = {
                "tuff fire lastest update",
                "lastest updates gets more highlight",
            }
        }
    ]
]

SentinelUI.Initialize(--runs script
    (table) Options [
        (string | nil) KeyLink = "https://..." // Keys.KeyLink
        (boolean | nil) Keyless = false // Keys.Keyless
        (string) Token = "SHA256_Hash" // REQUIRED: Security Token 
        (function) MainLoader = Function() // Runs after login
        (function) Function = Function(InputKey) --returns textbox text whatever put in
            // Inside this function, you MUST call either:
            // SentinelUI.Authorize(Token)
            // SentinelUI.Fail()
    ]
)

SentinelUI.Notify(--creates a notification
    (string) Title = "Notification"
    (string) Description = "Message content"
    (number) Duration = 5 // Seconds
    (string | nil) Type = "info" | "success" | "warn" | "alert"
)

SentinelUI.AddSettings(--creates settings
    (table) Options [
        (string) Title = "Setting Name"
        (string) Desc = "Description text"
        (boolean) Default = true or false or local
        (function) Function = Function(NewState) // Callback
    ]
)

SentinelUI.AddUpdate(--adds update
    (table) UpdateData [
        (string) Version = "v1.0.0"
        (string) Date = "01.01.2025" // DD.MM.YYYY
        (table) Updates = {
            "Update line 1",
            "Update line 2"
        }
    ],
)

SentinelUI.AdjustTextbox(--adjust textbox
    (string) State = "Success" | "Failed"
    (number) Duration = 4
)

SentinelUI.SaveConfig() -- run these if u wanna save by manual but script already saves
SentinelUI.LoadConfig() -- run these if u wanna save by manual but script already saves

               --EXAMPLE--
local SentinelUI = loadstring(game:HttpGet("https://raw.githubusercontent.com/AsuraXowner/Sentinel-Open-Source/refs/heads/main/SentinelKeySystem/Installer.lua", true))()
local AuthorizeToken = crypt.hash(tick()..tostring(math.random()), "sha256")--best result



local function Load()
print("runs the code!")--YOUR SCRIPT HERE
end

SentinelUI.Initialize({
	KeyLink = "",--get key link
	--Keyless = true,--keyless mode? work in progress
	Token = AuthorizeToken,--IS REQUIRED for protection
	MainLoader = Load, --runs the main script after verifiying key
	Function = function(v)--return textbox key
		if v == "example_verify" then
			SentinelUI.Authorize(AuthorizeToken)
		else
			SentinelUI.Fail() 
		end
	end 
})

table.insert(SentinelUI.Keys.Updates, 3, {
	Version = "v0.5.0 (Custom)",--version of update
	Date = "09.12.2025",--date of update
	Updates = {--updates so
		"update1",
		"update2",
	}
})

SentinelUI.AddSettings({
	Title = "fire from mainscript",--setting title
	Desc = "432424",--setting desc
	Default = true,--is enabled default
	Function = function(v)--returns true or false
		--code? duh
	end 
})
