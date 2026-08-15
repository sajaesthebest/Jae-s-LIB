# Jae's LIB

A clean, lightweight and modern UI library for Roblox, based on Orion Library with several improvements.

## Features

- Clean & minimalist design
- Smooth theme transitions
- Built-in theme system (Default, Dark, Midnight, Purple, Green)
- Custom themes support
- Window resizing
- Dynamic background image support
- Config saving system
- Notifications
- Intro animation
- Fully customizable elements

## Installation

```lua
local OrionLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/sajaesthebest/Jae-s-LIB/main/Source.lua"))()
```

## Quick Start

```lua
local OrionLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/sajaesthebest/Jae-s-LIB/main/Source.lua"))()

local Window = OrionLib:MakeWindow({
    Name = "Jae's LIB",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "JaeConfig",
    IntroEnabled = true,
    IntroText = "Jae's LIB"
})

local Tab = Window:MakeTab({
    Name = "Main",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

Tab:AddButton({
    Name = "Click Me",
    Callback = function()
        print("Button clicked!")
    end
})

OrionLib:Init()
```

## Themes

```lua
OrionLib:SetTheme("Purple") -- Default, Dark, Midnight, Purple, Green
```

Create your own theme:

```lua
OrionLib:CreateTheme("MyTheme", {
    Main = Color3.fromRGB(20, 10, 10),
    Second = Color3.fromRGB(30, 15, 15),
    Stroke = Color3.fromRGB(50, 25, 25),
    Divider = Color3.fromRGB(40, 20, 20),
    Text = Color3.fromRGB(255, 230, 230),
    TextDark = Color3.fromRGB(180, 140, 140),
    Accent = Color3.fromRGB(255, 80, 80)
})

OrionLib:SetTheme("MyTheme")
```

## Background Image

```lua
-- When creating the window
local Window = OrionLib:MakeWindow({
    Name = "My Hub",
    Background = "rbxassetid://123456789",
    BackgroundTransparency = 0.4
})

-- Or change it later
OrionLib:SetBackground("rbxassetid://123456789", 0.4)
OrionLib:SetBackground(nil) -- remove background
```

## Documentation

See [Documentation.md](Documentation.md) for full API reference.

## Credits

- Original Orion Library
- Improved and maintained by Jae
