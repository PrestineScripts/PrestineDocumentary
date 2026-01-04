# Prestine Library (PrestineLib) 📦

> Transcript Log 📜  
> Subject: PrestineLib  
> Author: R3LIG  
> Type: Roblox GUI Library  
> Status: Active ✅

---

## Overview 🧭

Prestine Library (**PrestineLib**) is a lightweight Roblox GUI framework for creating hubs composed of **tabs**, **sections**, and **interactive UI components**.

⚠️ The library enforces a **strict order of execution**. Deviating from this order may result in runtime failure or missing UI elements.

---

## Installation 🔧

The library must be loaded before any GUI-related functions are called.

~~~lua
-- Main Library (Required)
local PrestineLib = loadstring(game:HttpGet(
    "https://raw.githubusercontent.com/PrestineScripts/PrestineLibrary/refs/heads/main/PrestineLib"
))()
~~~

Required: This script is mandatory and must be executed first.

---

## Quick Start 🚀

### Step 1: Create GUI Profile 🖥️

Creates the main GUI window and defines its identity.

~~~lua
local PrestineGUI = PrestineLib:CreateGUI({
    Title = "Prestine Hub | [Unnamed Game]",
    SubTitle = "Made By R3LIG",
})
~~~

Options:
- Title (string): Main GUI title  
- SubTitle (string): Secondary text displayed under the title  

---

### Step 2: Create Tabs 🗂️

Tabs must be created before sections or UI components.

~~~lua
local Tabs = {
    { Name = "Home", Icon = "rbxassetid://85741999712008" },
    { Name = "Main", Icon = "rbxassetid://<assetid>" },
}

PrestineLib:CreateTab(Tabs)
~~~

Each tab requires:
- Name (string)
- Icon (rbxassetid)

---

### Step 3: Set Configuration ⚙️

Defines the hub name and game-specific configuration namespace.

~~~lua
PrestineLib:Set("PrestineHub", "UnnamedGame")
~~~

---

### Step 4: Add Sections 🧩

Sections divide a tab into logical areas. **You must add a section before adding components into that tab.**

~~~lua
PrestineLib:AddSection({
    Tab = "Home",
    MainTitle = "Home",
})
~~~

---

## Components Tutorials 🧪

Below, **every component has its own tutorial** with:
- What it does
- Required fields
- Example
- Callback behavior (if it has one)

> Tip: The `Tab` value must match your tab name exactly (case-sensitive).

---

## AddParagraph 📄 (Static Text)

### What it does
Creates a paragraph/text block for information, credits, status messages, etc.

### Required Fields
- Tab (string)
- MainTitle (string)
- paragraphSize (number)
- MainContent (string)

### Example
~~~lua
local statusParagraph = PrestineLib:AddParagraph({
    Tab = "Home",
    MainTitle = "Status",
    paragraphSize = 70,
    MainContent = "Im the best"
})
~~~

### Notes
Some libraries return a handle (like `statusParagraph`) so you can later update it if supported.

---

## AddNotification 🔔 (Popup Toast)

### What it does
Shows a temporary notification pop-up.

### Required Fields
- TitleText (string)
- ContentText (string)
- Duration (number) seconds

### Example
~~~lua
PrestineLib:AddNotification({
    TitleText = "Saved",
    ContentText = "Your settings were saved successfully.",
    Duration = 3
})
~~~

### Notes
Use this after actions like saving configs, enabling features, finishing tasks, etc.

---

## AddButton 🔘 (Click Action)

### What it does
Creates a clickable button that runs a function when pressed.

### Required Fields
- Tab (string)
- MainName (string)
- Callback (function)

### Example
~~~lua
PrestineLib:AddButton({
    Tab = "Home",
    MainName = "Button Title",
    Callback = function()
        print("Clicked!")
    end
})
~~~

### Callback
Runs once every time the button is clicked.

---

## AddToggle 🔁 (On/Off Switch)

### What it does
Creates a boolean toggle (true/false).

### Required Fields
- Tab (string)
- MainName (string)
- DefaultState (boolean)
- Callback (function(Value))

### Example
~~~lua
PrestineLib:AddToggle({
    Tab = "Home",
    MainName = "Toggle Title",
    DefaultState = false,
    Callback = function(Value)
        print("Toggle:", Value)
    end
})
~~~

### Callback
`Value` will be `true` or `false`.

---

## AddDropdown 📋 (Choose Option)

### What it does
Creates a dropdown menu for picking one option, or multiple if `Multiple = true`.

### Required Fields
- Tab (string)
- MainTitle (string)
- ChoiceList (table)
- Multiple (boolean)
- DefaultChoice (table)
- Callback (function(Value))

### Example (Single Select)
~~~lua
PrestineLib:AddDropdown({
    Tab = "Home",
    MainTitle = "Select Choice",
    ChoiceList = {"1", "2", "3", "4", "5", "67"},
    Multiple = false,
    DefaultChoice = {"1"},
    Callback = function(Value)
        print("Selected:", Value)
    end
})
~~~

### Notes
- If `Multiple = false`, the callback usually returns a single selection.
- If `Multiple = true`, it may return a table of chosen values (depends on library behavior).

---

## AddInput ⌨️ (Text Box)

### What it does
Creates a text input field (user can type text).

### Required Fields
- Tab (string)
- MainTitle (string)
- PlaceHolder (string)
- Callback (function(Value))

### Example
~~~lua
PrestineLib:AddInput({
    Tab = "Home",
    MainTitle = "Input Title",
    PlaceHolder = "Placeholder",
    Callback = function(Value)
        print("Typed:", Value)
    end
})
~~~

### Callback
Returns what the user entered as a string.

---

## AddSlider 🎚️ (Number Picker)

### What it does
Creates a slider with a min/max range and step increments.

### Required Fields
- Tab (string)
- SliderTitle (string)
- Min (number)
- Max (number)
- DefaultValue (number)
- Increment (number)
- Callback (function(Value))

### Example
~~~lua
PrestineLib:AddSlider({
    Tab = "Home",
    SliderTitle = "Slider Title",
    Min = 0,
    Max = 300,
    DefaultValue = 150,
    Increment = 10,
    Callback = function(Value)
        print("Slider:", Value)
    end
})
~~~

### Callback
Returns the current slider value (number).

---

## AddKeybind ⌨️🗝️ (Key Toggle / Hotkey)

### What it does
Lets the user press a key to trigger an action.

### Required Fields
- Tab (string)
- MainTitle (string)
- DefaultKey (Enum.KeyCode)
- Callback (function(key))

### Example
~~~lua
PrestineLib:AddKeybind({
    Tab = "Home",
    MainTitle = "Toggle UI",
    DefaultKey = Enum.KeyCode.RightShift,
    Callback = function(key)
        print("Pressed:", key.Name)
        -- Example: PrestineGUI:Toggle() (if your GUI supports it)
    end
})
~~~

### Callback
Returns the key pressed (usually the keybind key).

---

## AddColorPicker 🎨 (Pick a Color)

### What it does
Creates a color picker for selecting Color3 values (great for themes/accent colors).

### Required Fields
- Tab (string)
- MainName (string)
- DefaultColor (Color3)
- Callback (function(color))

### Example
~~~lua
PrestineLib:AddColorPicker({
    Tab = "Home",
    MainName = "Accent Color",
    DefaultColor = Color3.fromRGB(0, 140, 255),
    Callback = function(color)
        print("Color:", color)
        -- Example usage: set accent theme if supported by your library
    end
})
~~~

### Callback
Returns a `Color3` value.

---

## AddTimedToggle ⏱️🔁 (Toggle With Timer / Hold)

### What it does
A toggle that behaves like an auto feature toggle (often used for autofarm/loop features).
(Some libraries implement extra timing UI or timed activation — depends on the library.)

### Required Fields
- Tab (string)
- MainName (string)
- Callback (function(state))

### Example
~~~lua
PrestineLib:AddTimedToggle({
    Tab = "Home",
    MainName = "Auto Farm",
    Callback = function(state)
        print("Auto Farm:", state)

        -- Example loop pattern:
        -- if state then
        --     while state do
        --         task.wait(0.25)
        --         -- your farm code here
        --     end
        -- end
    end
})
~~~

### Callback
`state` is true/false depending on toggle state.

---

## Complete Example Using Your Components 🧬

~~~lua
-- Load library (1)
local PrestineLib = loadstring(game:HttpGet(
    "https://raw.githubusercontent.com/PrestineScripts/PrestineLibrary/refs/heads/main/PrestineLib"
))()

-- Create GUI (2)
local PrestineGUI = PrestineLib:CreateGUI({
    Title = "Prestine Hub | Example",
    SubTitle = "Made By R3LIG",
})

-- Create tabs (3)
local Tabs = {
    { Name = "Home", Icon = "rbxassetid://85741999712008" },
}
PrestineLib:CreateTab(Tabs)

-- Set config (4)
PrestineLib:Set("PrestineHub", "ExampleGame")

-- Add section (5)
PrestineLib:AddSection({
    Tab = "Home",
    MainTitle = "Home",
})

-- Paragraph
local statusParagraph = PrestineLib:AddParagraph({
    Tab = "Home",
    MainTitle = "Status",
    paragraphSize = 70,
    MainContent = "Im the best"
})

-- Notification
PrestineLib:AddNotification({
    TitleText = "Saved",
    ContentText = "Your settings were saved successfully.",
    Duration = 3
})

-- Button
PrestineLib:AddButton({
    Tab = "Home",
    MainName = "Button Title",
    Callback = function()
        print("Button clicked")
    end
})

-- Toggle
PrestineLib:AddToggle({
    Tab = "Home",
    MainName = "Toggle Title",
    DefaultState = false,
    Callback = function(Value)
        print(Value)
    end
})

-- Dropdown
PrestineLib:AddDropdown({
    Tab = "Home",
    MainTitle = "Select Choice",
    ChoiceList = {"1", "2", "3", "4", "5", "67"},
    Multiple = false,
    DefaultChoice = {"1"},
    Callback = function(Value)
        print(Value)
    end
})

-- Input
PrestineLib:AddInput({
    Tab = "Home",
    MainTitle = "Input Title",
    PlaceHolder = "Placeholder",
    Callback = function(Value)
        print(Value)
    end
})

-- Slider
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

-- Keybind
PrestineLib:AddKeybind({
    Tab = "Home",
    MainTitle = "Toggle UI",
    DefaultKey = Enum.KeyCode.RightShift,
    Callback = function(key)
        print(key)
    end
})

-- Color Picker
PrestineLib:AddColorPicker({
    Tab = "Home",
    MainName = "Accent Color",
    DefaultColor = Color3.fromRGB(0, 140, 255),
    Callback = function(color)
        print(color)
    end
})

-- Timed Toggle
PrestineLib:AddTimedToggle({
    Tab = "Home",
    MainName = "Auto Farm",
    Callback = function(state)
        print(state)
    end
})
~~~

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

