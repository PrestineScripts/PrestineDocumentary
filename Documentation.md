# Prestine Library (PrestineLib) 📦

> Transcript Log 📜  
> Subject: PrestineLib  
> Author: R3LIG  
> Type: Roblox GUI Library  
> Status: Active ✅

---

## Overview 🧭

Prestine Library, referred to as PrestineLib, is a lightweight Roblox GUI framework designed for creating hubs composed of tabs, sections, and interactive UI components.

The library enforces a strict order of execution. Deviating from this order may result in runtime failure or missing UI elements ⚠️.

---

## Installation 🔧

The library must be loaded before any GUI-related functions are called.

```lua
-- Main Library (Required)
local PrestineLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/PrestineScripts/PrestineLibrary/refs/heads/main/PrestineLib"))()
```

Required: This script is mandatory and must be executed first.

---

## Quick Start 🚀

### Step 1: Create GUI Profile 🖥️

Creates the main GUI window and defines its identity.

```lua
local PrestineGUI = PrestineLib:CreateGUI({
    Title = "Prestine Hub | [Unnamed Game]",
    SubTitle = "Made By R3LIG",
})
```

Options:
- Title (string): Main GUI title
- SubTitle (string): Secondary text displayed under the title

---

### Step 2: Create Tabs 🗂️

Tabs must be created before sections or UI components.

```lua
local Tabs = {
    { Name = "Home", Icon = "rbxassetid://85741999712008" },
    { Name = "Main", Icon = "rbxassetid://<assetid>" },
}

PrestineLib:CreateTab(Tabs)
```

Each tab requires:
- Name (string)
- Icon (rbxassetid)

---

### Step 3: Set Configuration ⚙️

Defines the hub name and game-specific configuration namespace.

```lua
PrestineLib:Set("PrestineHub", "UnnamedGame")
```

---

### Step 4: Add Sections 🧩

Sections divide a tab into logical areas.

```lua
PrestineLib:AddSection({
    Tab = "Home",
    MainTitle = "Home",
})
```

---

## UI Components 🧪

### AddParagraph 📄

Used for static text content.

```lua
PrestineLib:AddParagraph({
    Tab = "Home",
    MainTitle = "Paragraph Title",
    paragraphSize = 70,
    MainContent = "Content Here"
})
```

---

### AddButton 🔘

Executes a callback when clicked.

```lua
PrestineLib:AddButton({
    Tab = "Home",
    MainName = "Button Title",
    Callback = function()
        print("Button clicked")
    end
})
```

---

### AddToggle 🔁

Boolean on/off toggle.

```lua
PrestineLib:AddToggle({
    Tab = "Home",
    MainName = "Toggle Title",
    DefaultState = false,
    Callback = function(Value)
        print(Value)
    end
})
```

---

### AddDropdown 📋

Single or multiple choice selector.

```lua
PrestineLib:AddDropdown({
    Tab = "Home",
    MainTitle = "Select Choice",
    ChoiceList = {"1", "2", "3"},
    Multiple = false,
    DefaultChoice = {"1"},
    Callback = function(Value)
        print(Value)
    end
})
```

---

### AddInput ⌨️

Text input field.

```lua
PrestineLib:AddInput({
    Tab = "Home",
    MainTitle = "Input Title",
    PlaceHolder = "Placeholder",
    Callback = function(Value)
        print(Value)
    end
})
```

---

### AddSlider 🎚️

Numeric slider with adjustable range.

```lua
PrestineLib:AddSlider({
    Tab = "Home",
    SliderTitle = "Slider Title",
    Min = 0,
    Max = 300,
    DefaultValue = 150,
    Increment = 10,
    Callback = function(Value)
        print(Value)
    end
})
```

---

## Full Minimal Example 🧬

```lua
local PrestineLib = loadstring(game:HttpGet(
  "https://raw.githubusercontent.com/PrestineScripts/PrestineLibrary/refs/heads/main/PrestineLib"
))()

local PrestineGUI = PrestineLib:CreateGUI({
    Title = "Prestine Hub | Example",
    SubTitle = "Made By R3LIG",
})

local Tabs = {
    { Name = "Home", Icon = "rbxassetid://85741999712008" },
    { Name = "Main", Icon = "rbxassetid://1234567890" },
}

PrestineLib:CreateTab(Tabs)
PrestineLib:Set("PrestineHub", "ExampleGame")

PrestineLib:AddSection({
    Tab = "Home",
    MainTitle = "Home",
})

PrestineLib:AddParagraph({
    Tab = "Home",
    MainTitle = "Info",
    paragraphSize = 70,
    MainContent = "Hello from Prestine Library."
})

PrestineLib:AddButton({
    Tab = "Home",
    MainName = "Print Hello",
    Callback = function()
        print("Hello")
    end
})

PrestineLib:AddToggle({
    Tab = "Home",
    MainName = "Enable Feature",
    DefaultState = false,
    Callback = function(Value)
        print(Value)
    end
})

PrestineLib:AddDropdown({
    Tab = "Home",
    MainTitle = "Pick One",
    ChoiceList = {"1", "2", "3"},
    Multiple = false,
    DefaultChoice = {"1"},
    Callback = function(Value)
        print(Value)
    end
})

PrestineLib:AddInput({
    Tab = "Home",
    MainTitle = "Your Name",
    PlaceHolder = "Type here...",
    Callback = function(Value)
        print(Value)
    end
})

PrestineLib:AddSlider({
    Tab = "Home",
    SliderTitle = "Volume",
    Min = 0,
    Max = 300,
    DefaultValue = 150,
    Increment = 10,
    Callback = function(Value)
        print(Value)
    end
})
```

---

## Notes 📝

Execution order is mandatory:

1. Load library  
2. Create GUI  
3. Create tabs  
4. Set config  
5. Add sections  
6. Add components  

Tab names must match exactly.

---

## License 📄

Free to use.  
Do not resell as your own library.  
Credit the author (R3LIG).

