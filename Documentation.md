# Jae's LIB - Documentation

Complete API reference for Jae's LIB.

---

## Loading the Library

```lua
local OrionLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/sajaesthebest/Jae-s-LIB/main/Source.lua"))()
```

---

## MakeWindow

Creates the main window.

```lua
local Window = OrionLib:MakeWindow({
    Name = "Window Name",                  -- string
    HidePremium = false,                   -- boolean
    SaveConfig = false,                    -- boolean
    ConfigFolder = "MyConfig",             -- string
    IntroEnabled = true,                   -- boolean
    IntroText = "My Hub",                  -- string
    IntroIcon = "rbxassetid://8834748103", -- string
    ShowIcon = false,                      -- boolean
    Icon = "rbxassetid://8834748103",      -- string
    Background = nil,                      -- string (rbxassetid)
    BackgroundTransparency = 0.4,          -- number (0 to 1)
    CloseCallback = function() end         -- function
})
```

---

## MakeTab

Creates a new tab.

```lua
local Tab = Window:MakeTab({
    Name = "Tab Name",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})
```

---

## Elements

### AddSection

```lua
local Section = Tab:AddSection({
    Name = "Section Name"
})
```

### AddLabel

```lua
local Label = Tab:AddLabel("This is a label")

Label:Set("New text")
```

### AddParagraph

```lua
local Paragraph = Tab:AddParagraph("Title", "This is the content of the paragraph.")

Paragraph:Set("New content")
```

### AddButton

```lua
Tab:AddButton({
    Name = "Button Name",
    Icon = "rbxassetid://3944703587", -- optional
    Callback = function()
        print("Clicked!")
    end
})
```

### AddToggle

```lua
local Toggle = Tab:AddToggle({
    Name = "Toggle Name",
    Default = false,
    Color = Color3.fromRGB(88, 101, 242), -- optional
    Flag = "MyToggle",                    -- optional (for config)
    Save = true,                          -- optional
    Callback = function(Value)
        print(Value)
    end
})

Toggle:Set(true)
```

### AddSlider

```lua
local Slider = Tab:AddSlider({
    Name = "Slider Name",
    Min = 0,
    Max = 100,
    Default = 50,
    Increment = 1,
    ValueName = "%",
    Color = Color3.fromRGB(88, 101, 242), -- optional
    Flag = "MySlider",
    Save = true,
    Callback = function(Value)
        print(Value)
    end
})

Slider:Set(75)
```

### AddDropdown

```lua
local Dropdown = Tab:AddDropdown({
    Name = "Dropdown Name",
    Default = "Option 1",
    Options = {"Option 1", "Option 2", "Option 3"},
    Flag = "MyDropdown",
    Save = true,
    Callback = function(Value)
        print(Value)
    end
})

Dropdown:Set("Option 2")
Dropdown:Refresh({"New 1", "New 2"}, true) -- true = clear old options
```

### AddBind

```lua
local Bind = Tab:AddBind({
    Name = "Keybind",
    Default = Enum.KeyCode.E,
    Hold = false,
    Flag = "MyBind",
    Save = true,
    Callback = function(Value) -- Value is true/false only when Hold = true
        print("Key pressed")
    end
})

Bind:Set(Enum.KeyCode.Q)
```

### AddTextbox

```lua
Tab:AddTextbox({
    Name = "Textbox Name",
    Default = "",
    TextDisappear = false,
    Callback = function(Value)
        print(Value)
    end
})
```

### AddColorpicker

```lua
local Colorpicker = Tab:AddColorpicker({
    Name = "Colorpicker",
    Default = Color3.fromRGB(255, 255, 255),
    Flag = "MyColor",
    Save = true,
    Callback = function(Value)
        print(Value)
    end
})

Colorpicker:Set(Color3.fromRGB(255, 0, 0))
```

---

## Notifications

```lua
OrionLib:MakeNotification({
    Name = "Title",
    Content = "This is the notification content.",
    Image = "rbxassetid://4384403532",
    Time = 5
})
```

---

## Themes

### SetTheme

```lua
OrionLib:SetTheme("Purple") -- Default | Dark | Midnight | Purple | Green
```

### CreateTheme

```lua
OrionLib:CreateTheme("Custom", {
    Main = Color3.fromRGB(16, 16, 20),
    Second = Color3.fromRGB(22, 22, 28),
    Stroke = Color3.fromRGB(40, 40, 50),
    Divider = Color3.fromRGB(30, 30, 38),
    Text = Color3.fromRGB(240, 240, 245),
    TextDark = Color3.fromRGB(130, 130, 145),
    Accent = Color3.fromRGB(88, 101, 242)
})
```

### ChangeThemeColor

```lua
OrionLib:ChangeThemeColor("Accent", Color3.fromRGB(255, 100, 50))
```

---

## Background

### On Window Creation

```lua
OrionLib:MakeWindow({
    Background = "rbxassetid://123456789",
    BackgroundTransparency = 0.4
})
```

### Dynamically

```lua
OrionLib:SetBackground("rbxassetid://123456789", 0.4)
OrionLib:SetBackground(nil) -- removes the background
```

---

## Config System

When `SaveConfig = true`, the library automatically saves and loads values that have `Flag` + `Save = true`.

Supported elements:
- Toggle
- Slider
- Dropdown
- Bind
- Colorpicker

```lua
OrionLib:Init() -- Call this at the end of your script to load saved config
```

---

## Other Functions

### Destroy

```lua
OrionLib:Destroy()
```

### IsRunning

```lua
if OrionLib:IsRunning() then
    print("UI is active")
end
```

---

## Full Example

```lua
local OrionLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/sajaesthebest/Jae-s-LIB/main/Source.lua"))()

local Window = OrionLib:MakeWindow({
    Name = "Example Hub",
    SaveConfig = true,
    ConfigFolder = "ExampleHub",
    IntroEnabled = true,
    IntroText = "Example Hub"
})

local Main = Window:MakeTab({
    Name = "Main",
    Icon = "rbxassetid://4483345998"
})

Main:AddButton({
    Name = "Notify",
    Callback = function()
        OrionLib:MakeNotification({
            Name = "Hello",
            Content = "This is a test notification",
            Time = 4
        })
    end
})

local Config = Window:MakeTab({
    Name = "Config",
    Icon = "rbxassetid://6031280882"
})

Config:AddDropdown({
    Name = "Theme",
    Default = "Default",
    Options = {"Default", "Dark", "Midnight", "Purple", "Green"},
    Callback = function(Value)
        OrionLib:SetTheme(Value)
    end
})

Config:AddColorpicker({
    Name = "Accent",
    Default = Color3.fromRGB(88, 101, 242),
    Callback = function(Value)
        OrionLib:ChangeThemeColor("Accent", Value)
    end
})

OrionLib:Init()
```
