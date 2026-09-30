# Prestine Library (PrestineLib) 📦

**Author:** R3LIG

**Type:** Roblox GUI Library

**Status:** Active ✅

---

## Overview 🧭

**Prestine Library (PrestineLib)** is a lightweight, responsive Roblox GUI framework built for creating modular hubs composed of collapsible tab groups, content sections, interactive controls, live progress trackers, floating panels, and queued notifications.

> ⚠️ **Strict Execution Order:** The library requires components and profiles to be initialized in a specific sequential order. Deviating from this order may cause runtime failures or missing UI elements.

---

## Installation 🔧

The library must be loaded before any GUI-related functions are called:

```lua
-- Main Library (Required)
local PrestineLib = loadstring(game:HttpGet(
    "https://raw.githubusercontent.com/PrestineScripts/PrestineLibrary/refs/heads/main/Initializer.lua"
))()

```

---

## Quick Start 🚀

### Step 1: Create GUI Profile 🖥️

Creates the main window framework and defines its title metadata.

```lua
local PrestineGUI = PrestineLib:CreateGUI({
    Title = "Prestine Hub | [Game Title]",
    SubTitle = "Made By R3LIG",
})

```

### Step 2: Create Tabs & Collapsible Tab Groups 🗂️

Tabs must be registered before adding sections or components. `PrestineLib:CreateTab` supports two setups: **Collapsible Tab Categories (Sections)** and **Flat Tabs**.

#### Option A: Collapsible Tab Groups (Sidebar Sections)

Groups sub-tabs under an accordion header that can start opened or closed:

* **Group Fields:**
* `Section` *(string)*: Label text for the category header.
* `Icon` *(string / assetid)*: Category icon name or asset ID.
* `Open` *(boolean)*: Initial accordion visibility state (`true` for expanded, `false` for collapsed).
* `Tabs` *(table)*: Array of sub-tabs contained within this group:
* `Name` *(string)*: Tab name. Must match the `Tab` parameter when registering components.


* `LayoutOrder` *(number, optional)*: Explicit ordering position.





```lua
local AllTabs = {
    {
        Section = "Dashboard",
        Icon = "Home",
        Open = true, -- Starts expanded
        Tabs = {
            { Name = "Home", LayoutOrder = 1 },
            { Name = "Lobby", LayoutOrder = 2 }
        }
    },
    {
        Section = "Automation",
        Icon = "Automatic",
        Open = false, -- Starts collapsed
        Tabs = {
            { Name = "Auto", LayoutOrder = 3 },
            { Name = "Main", LayoutOrder = 4 },
            { Name = "Stuff", LayoutOrder = 5 }
        }
    },
    {
        Section = "Configuration",
        Icon = "Settings",
        Open = false,
        Tabs = {
            { Name = "Player", LayoutOrder = 6 },
            { Name = "Performance", LayoutOrder = 7 },
            { Name = "Utility", LayoutOrder = 8 },
            { Name = "Settings", LayoutOrder = 9 },
            { Name = "Config", LayoutOrder = 10 }
        }
    }
}

PrestineLib:CreateTab(AllTabs)

```

#### Option B: Flat Tab Array

A basic list of tabs without sidebar grouping:

```lua
local FlatTabs = {
    { Name = "Home", Icon = "rbxassetid://85741999712008" },
    { Name = "Main", Icon = "rbxassetid://85741999712008" }
}

PrestineLib:CreateTab(FlatTabs)

```

### Step 3: Set Configuration Namespace ⚙️

Defines the hub name and game configuration identity for state saving.

```lua
PrestineLib:Set("PrestineHub", "GameNamespace")

```

### Step 4: Add In-Tab Sections 🧩

Divides individual tab content areas into visual groups before adding controls.

```lua
local combatSec = PrestineLib:AddSection({
    Tab = "Auto",
    MainTitle = "Combat Features",
    Collidable = true -- Enables click-to-collapse for elements below it
})

```

---

## Containers & Resolution

Components accept a configuration table containing target placement parameters:

* `Tab` *(string)*: Case-sensitive name of the target tab (matches the sub-tab's `Name`).


* `Section` *(Instance/Reference)*: A reference returned by `PrestineLib:AddSection(...)`. When provided, elements nest directly beneath that section.



---

## Components Documentation 🧪

### Layout & Containers

#### `AddSection`

Creates an accented banner dividing elements into groups. Supports collapsible toggling for child components.

* **Parameters:**
* `Tab` *(string)*: Target tab name.


* `MainTitle` *(string)*: Header text.


* `Collidable` *(boolean, optional)*: Enables click-to-collapse functionality for items following this section.





```lua
local combatSec = PrestineLib:AddSection({
    Tab = "Auto",
    MainTitle = "Combat Features",
    Collidable = true
})

```

#### `AddLabel`

Renders an unobtrusive static label line.

* **Parameters:**
* `Tab` *(string)*: Target tab name.


* `Name` *(string)*: Text string to display.





```lua
PrestineLib:AddLabel({
    Tab = "Auto",
    Name = "Target Priority"
})

```

#### `AddDivider`

Inserts a subtle gradient separator line between components.

* **Parameters:**
* `Tab` *(string)*: Target tab name.





```lua
PrestineLib:AddDivider({
    Tab = "Auto"
})

```

---

### Content Components

#### `AddParagraph`

A container displaying a formatted title and multi-line body text.

* **Parameters:**
* `Tab` *(string)*: Target tab name.


* `MainTitle` *(string)*: Card title.


* `MainContent` *(string)*: Card body text.


* `paragraphSize` *(number, optional)*: Total frame height (default: `80`).




* **Controller Methods:**
* `paragraph:SetTitle(newTitle)`

* `paragraph:SetContent(newContent)`




```lua
local statusCard = PrestineLib:AddParagraph({
    Tab = "Home",
    MainTitle = "Server Status",
    MainContent = "All functions operational.",
    paragraphSize = 80
})

statusCard:SetContent("Updated server notice.")

```

#### `AddParagraphBars`

Displays progress bars and segmented trackers inside a styled card. Supports dynamic runtime updates, additions, and removals.

* **Parameters:**
* `Tab` *(string)*: Target tab name.


* `MainTitle` *(string)*: Card title.


* `MainContent` *(string, optional)*: Subtitle/description.


* `ShowContent` *(boolean, optional)*: Set `false` to hide body text.


* `Compact` *(boolean, optional)*: Applies tighter padding and typography.


* `Bars` *(table)*: List of progress bar definitions:


* `Key` *(string)*: Unique identifier.


* `Label` *(string)*: Metric label.


* `Progress` *(number)*: Current value.


* `Goal` *(number)*: Maximum limit.


* `Style` *(string)*: `"Bar"` (smooth fill) or `"Segments"` (discrete notches).


* `Segments` *(number, optional)*: Number of segments if style is `"Segments"` (default: `12`).


* `Emphasis` *(boolean, optional)*: Brightens text and accent styling.






* **Controller Methods:**
* `bars:SetProgress(keyOrIndex, value, tweenTime)`

* `bars:SetGoal(keyOrIndex, newGoal, tweenTime)`

* `bars:AddBar(barDef)`

* `bars:RemoveBar(keyOrIndex)`

* `bars:GetBar(keyOrIndex)`

* `bars:SetTitle(title)`

* `bars:SetContent(content)`




```lua
local playerStats = PrestineLib:AddParagraphBars({
    Tab = "Home",
    MainTitle = "Character Stats",
    MainContent = "Real-time attributes",
    Bars = {
        {
            Key = "xp",
            Label = "Experience",
            Progress = 450,
            Goal = 1000,
            Style = "Bar",
            Emphasis = true
        },
        {
            Key = "energy",
            Label = "Stamina",
            Progress = 8,
            Goal = 10,
            Style = "Segments",
            Segments = 10
        }
    }
})

playerStats:SetProgress("xp", 800)

```

#### `AddPanel`

Creates a draggable floating side window linked to an in-tab activation toggle button.

* **Parameters:**
* `Tab` *(string)*: Target tab containing the toggle button.


* `Title` *(string)*: Title displayed on the panel and toggle.


* `DefaultState` *(boolean, optional)*: Initial visibility state (default: `false`).


* `Content` *(string, optional)*: Initial multiline text content.


* `isExempted` *(boolean, optional)*: Skips persistent save state.




* **Controller Methods:**
* `panel:SetContent(newContent)`

* `panel:AddLine(newLine)`

* `panel:SetVisible(boolean)`

* `panel:GetVisible()`




```lua
local debugPanel = PrestineLib:AddPanel({
    Tab = "Utility",
    Title = "Event Log",
    DefaultState = false,
    Content = "[System Initialized]"
})

debugPanel:AddLine("Hooked entity events.")

```

---

### Interactive Components

#### `AddButton`

Action button with ripple effects, particle animations, and chevron transitions.

* **Parameters:**
* `Tab` *(string)*: Target tab name.


* `MainName` *(string)*: Button text.


* `SubTitle` *(string, optional)*: Secondary descriptive text.


* `Callback` *(function)*: Fires on activation.





```lua
PrestineLib:AddButton({
    Tab = "Auto",
    MainName = "Teleport to Safezone",
    SubTitle = "Bypasses combat tag",
    Callback = function()
        print("Teleporting...")
    end
})

```

#### `AddToggle`

Stateful on/off switch with persistent configuration support and an integrated loop runner (`WhileOn`).

* **Parameters:**
* `Tab` *(string)*: Target tab name.


* `MainName` *(string)*: Control label.


* `Description` *(string, optional)*: Explanatory subtitle below label.


* `DefaultState` *(boolean, optional)*: Initial state (default: `false`).


* `isExempted` *(boolean, optional)*: Skips configuration persistence.


* `Callback` *(function(state))*: Fires whenever the toggle state changes.


* `WhileOn` *(function, optional)*: Runs continuously while toggle is `true`.


* `WhileCooldown` *(number, optional)*: Delay between loop iterations in seconds (default: `0.1`).




* **Controller Methods:**
* `toggle:Set(boolean)`

* `toggle:Get()`




```lua
local farmToggle = PrestineLib:AddToggle({
    Tab = "Auto",
    MainName = "Auto Collect",
    Description = "Sweeps collectible drops within range",
    DefaultState = false,
    WhileCooldown = 0.25,
    Callback = function(state)
        print("Toggled:", state)
    end,
    WhileOn = function()
        print("Collecting entities...")
    end
})

```

#### `AddSaveToggle`

A shortcut toggle dedicated to setting configuration auto-saving (`_G.isSavingGV`).

* **Parameters:**
* `Tab` *(string)*: Target tab name.


* `MainName` *(string)*: Label name.


* `DefaultState` *(boolean)*: Initial state.





```lua
PrestineLib:AddSaveToggle({
    Tab = "Settings",
    MainName = "Auto Save Config",
    DefaultState = true
})

```

#### `AddTimedToggle`

A toggle paired with an integrated duration input and unit selector. Can run in `AutoOff` or `AutoOn` modes.

* **Parameters:**
* `Tab` *(string)*: Target tab name.


* `MainName` *(string)*: Toggle label.


* `DefaultState` *(boolean, optional)*: Initial state (default: `false`).


* `DefaultDuration` *(number, optional)*: Duration limit (default: `10`).


* `DefaultUnit` *(string, optional)*: `"s"`, `"m"`, `"h"`, `"d"`, or `"w"` (default: `"s"`).


* `Mode` *(string, optional)*: `"AutoOff"` or `"AutoOn"` (default: `"AutoOff"`).


* `Callback` *(function(state))*: Callback triggered on state flip.




* **Controller Methods:**
* `timedToggle:Set(tableOrBool)`: Supports `{ State = true, Duration = 60, Unit = "s" }` or boolean.


* `timedToggle:Get()`: Returns `toggleState, durationVal, unitVal`.


* `timedToggle:SetTimer(duration, unit)`




```lua
local timedBoost = PrestineLib:AddTimedToggle({
    Tab = "Auto",
    MainName = "Speed Burst",
    DefaultState = false,
    DefaultDuration = 30,
    DefaultUnit = "s",
    Mode = "AutoOff",
    Callback = function(state)
        print("Speed burst active:", state)
    end
})

```

#### `AddDropdown`

Selectable menu supporting single-choice selection, multi-choice filtering, real-time search queries, and dynamic option updates.

* **Parameters:**
* `Tab` *(string)*: Target tab name.


* `MainTitle` *(string)*: Dropdown label.


* `Description` *(string, optional)*: Explanatory subtitle below label.


* `ChoiceList` *(table)*: Array of string selections.


* `Multiple` *(boolean, optional)*: Enables multi-item selection (default: `false`).


* `DefaultChoice` *(string/table, optional)*: Initially active choice(s).


* `Callback` *(function(selected))*: Passes selection (string if single, array if multiple).




* **Controller Methods:**
* `dropdown:UpdateDropdown(newList)`

* `dropdown:Set(selection)`

* `dropdown:Close()`




```lua
local targetDropdown = PrestineLib:AddDropdown({
    Tab = "Auto",
    MainTitle = "Select Targets",
    Description = "Choose one or more entities to track",
    ChoiceList = {"Alpha", "Bravo", "Charlie", "Delta"},
    Multiple = true,
    DefaultChoice = {"Alpha"},
    Callback = function(selected)
        print("Selected:", table.concat(selected, ", "))
    end
})

targetDropdown:UpdateDropdown({"Echo", "Foxtrot", "Golf"})

```

#### `AddSlider`

A numerical slider featuring live input dragging, bounce-trail feedback, and step increments.

* **Parameters:**
* `Tab` *(string)*: Target tab name.


* `SliderTitle` *(string)*: Slider label.


* `Min` *(number)*: Lower boundary.


* `Max` *(number)*: Upper boundary.


* `DefaultValue` *(number)*: Starting value.


* `Increment` *(number, optional)*: Snapping step interval (default: `1`).


* `Callback` *(function(value))*: Fires when value changes.




* **Controller Methods:**
* `slider:Set(value)`




```lua
local speedSlider = PrestineLib:AddSlider({
    Tab = "Player",
    SliderTitle = "WalkSpeed",
    Min = 16,
    Max = 250,
    DefaultValue = 16,
    Increment = 2,
    Callback = function(val)
        print("WalkSpeed set to:", val)
    end
})

```

#### `AddInput`

A validated text input field with animated focus and commit states.

* **Parameters:**
* `Tab` *(string)*: Target tab name.


* `MainTitle` *(string)*: Input label.


* `PlaceHolder` *(string)*: Placeholder text.


* `Callback` *(function(text))*: Triggers when focus is lost.




* **Controller Methods:**
* `input:Set(text)`




```lua
PrestineLib:AddInput({
    Tab = "Config",
    MainTitle = "Webhook URL",
    PlaceHolder = "https://...",
    Callback = function(text)
        print("Configured webhook:", text)
    end
})

```

#### `AddKeybind`

Interactive key selector listening for keyboard inputs with formatting and live capture states.

* **Parameters:**
* `Tab` *(string)*: Target tab name.


* `MainTitle` *(string)*: Keybind label.


* `DefaultKey` *(Enum.KeyCode)*: Default trigger key.


* `Callback` *(function(key))*: Fires when a new key is mapped.




* **Controller Methods:**
* `keybind:SetKey(keyCodeOrString)`

* `keybind:GetKey()`




```lua
PrestineLib:AddKeybind({
    Tab = "Settings",
    MainTitle = "Menu Toggle",
    DefaultKey = Enum.KeyCode.RightControl,
    Callback = function(key)
        print("Bound key:", key.Name)
    end
})

```

#### `AddColorPicker`

Color selector with direct numerical RGB input boxes and a clickable quick-cycle preset swatch.

* **Parameters:**
* `Tab` *(string)*: Target tab name.


* `MainName` *(string)*: Label text.


* `DefaultColor` *(Color3)*: Initial Color3 value.


* `Callback` *(function(color3))*: Fires whenever the color updates.




* **Controller Methods:**
* `colorPicker:SetColor(color3OrTable)`

* `colorPicker:GetColor()`




```lua
local espColor = PrestineLib:AddColorPicker({
    Tab = "Performance",
    MainName = "ESP Color",
    DefaultColor = Color3.fromRGB(0, 170, 255),
    Callback = function(color)
        print("ESP Color updated to:", color)
    end
})

```

---

### Notifications

Notifications are routed into an automatic FIFO queue displayed on the screen.

#### `AddNotification`

Standard temporary toast popup with an animated duration progress bar.

```lua
PrestineLib:AddNotification({
    TitleText = "Settings Loaded",
    ContentText = "Configurations applied successfully.",
    Duration = 3 -- Display time in seconds
})

```

#### `AddInteractableNotif`

Actionable popup presenting confirmation buttons and an optional timeout callback.

```lua
PrestineLib:AddInteractableNotif({
    TitleText = "Server Reconnect",
    ContentText = "A game update was released. Reconnect now?",
    Duration = 8,
    Choices = {
        {
            Text = "Reconnect",
            Callback = function()
                print("Reconnecting...")
            end
        },
        {
            Text = "Dismiss",
            Callback = function()
                print("Dismissed.")
            end
        }
    },
    OnTimeout = function()
        print("Notification timed out without choice.")
    end
})

```

---

## Complete Example Using Tab Groups 🧬

```lua
-- 1. Load library
local PrestineLib = loadstring(game:HttpGet(
    "https://raw.githubusercontent.com/PrestineScripts/PrestineLibrary/refs/heads/main/Initializer.lua"
))()

-- 2. Create GUI Window
local PrestineGUI = PrestineLib:CreateGUI({
    Title = "Prestine Hub | Complete Build",
    SubTitle = "Made By R3LIG",
})

-- 3. Register Collapsible Tab Groups
local AllTabs = {
    {
        Section = "Dashboard",
        Icon = "Home",
        Open = true,
        Tabs = {
            { Name = "Home", LayoutOrder = 1 },
            { Name = "Lobby", LayoutOrder = 2 }
        }
    },
    {
        Section = "Automation",
        Icon = "Automatic",
        Open = false,
        Tabs = {
            { Name = "Auto", LayoutOrder = 3 },
            { Name = "Main", LayoutOrder = 4 }
        }
    },
    {
        Section = "Configuration",
        Icon = "Settings",
        Open = false,
        Tabs = {
            { Name = "Player", LayoutOrder = 5 },
            { Name = "Settings", LayoutOrder = 6 }
        }
    }
}

PrestineLib:CreateTab(AllTabs)

-- 4. Set Config Identity
PrestineLib:Set("PrestineHub", "DemoBuild")

-- 5. Add Sections
local combatSec = PrestineLib:AddSection({
    Tab = "Auto",
    MainTitle = "Auto Farm Setup",
    Collidable = true
})

-- 6. Add Components
PrestineLib:AddParagraph({
    Tab = "Home",
    MainTitle = "Welcome",
    MainContent = "PrestineLib setup with grouped collapsible tabs."
})

local tracker = PrestineLib:AddParagraphBars({
    Tab = "Home",
    MainTitle = "Session Progress",
    Bars = {
        { Key = "xp", Label = "Exp Gain", Progress = 30, Goal = 100, Style = "Bar", Emphasis = true },
        { Key = "stamina", Label = "Energy", Progress = 6, Goal = 10, Style = "Segments", Segments = 10 }
    }
})

local logger = PrestineLib:AddPanel({
    Tab = "Home",
    Title = "Runtime Log",
    DefaultState = false,
    Content = "Console ready."
})

PrestineLib:AddToggle({
    Tab = "Auto",
    MainName = "Auto Collect",
    Description = "Sweeps items within proximity",
    DefaultState = false,
    WhileCooldown = 0.5,
    WhileOn = function()
        tracker:SetProgress("xp", math.random(1, 100))
    end
})

PrestineLib:AddTimedToggle({
    Tab = "Auto",
    MainName = "Speed Burst",
    DefaultDuration = 15,
    DefaultUnit = "s",
    Mode = "AutoOff"
})

PrestineLib:AddSlider({
    Tab = "Player",
    SliderTitle = "WalkSpeed",
    Min = 16,
    Max = 150,
    DefaultValue = 16,
    Increment = 2
})

PrestineLib:AddDropdown({
    Tab = "Auto",
    MainTitle = "Target Mode",
    ChoiceList = {"Players", "NPCs", "Chests"},
    Multiple = false,
    DefaultChoice = "NPCs"
})

PrestineLib:AddSaveToggle({
    Tab = "Settings",
    MainName = "Auto Save Config",
    DefaultState = true
})

PrestineLib:AddKeybind({
    Tab = "Settings",
    MainTitle = "Menu Toggle",
    DefaultKey = Enum.KeyCode.RightShift
})

```

---

## License 📄

* Free to use in projects.
* Do not resell or redistribute as your own framework.
* Credit author (**R3LIG**).
