# PrestineLib Documentation

Welcome to the official, updated documentation for **PrestineLib**. This guide covers all available UI components, parameters, methods, and code examples based on the current library implementation.

---

## Table of Contents

1. [Containers & Resolution](https://www.google.com/search?q=%23containers--resolution)
2. [Layout Components](https://www.google.com/search?q=%23layout-components)
* [AddDivider](https://www.google.com/search?q=%23adddivider)
* [AddLabel](https://www.google.com/search?q=%23addlabel)
* [AddSection](https://www.google.com/search?q=%23addsection)


3. [Content Components](https://www.google.com/search?q=%23content-components)
* [AddParagraph](https://www.google.com/search?q=%23addparagraph)
* [AddParagraphBars](https://www.google.com/search?q=%23addparagraphbars)


4. [Interactive Components](https://www.google.com/search?q=%23interactive-components)
* [AddButton](https://www.google.com/search?q=%23addbutton)
* [AddToggle](https://www.google.com/search?q=%23addtoggle)
* [AddTimedToggle](https://www.google.com/search?q=%23addtimedtoggle)
* [AddSlider](https://www.google.com/search?q=%23addslider)
* [AddDropdown](https://www.google.com/search?q=%23adddropdown)


5. [Notifications](https://www.google.com/search?q=%23notifications)
* [AddNotification](https://www.google.com/search?q=%23addnotification)
* [AddInteractableNotif](https://www.google.com/search?q=%23addinteractablenotif)



---

## Containers & Resolution

Most components accept a `params` table. To specify where elements are placed, you can provide either:

* **`Tab`**: A string representing the target tab name (e.g., `Tab = "Home"`).
* **`Section`**: A reference object returned by `PrestineLib:AddSection(...)`.

---

## Layout Components

### AddDivider

Adds a subtle visual separator line to the container.

```lua
PrestineLib:AddDivider({
    Tab = "Home" -- or Section = sectionRef
})

```

### AddLabel

Displays a static text label.

```lua
PrestineLib:AddLabel({
    Tab = "Home",
    Name = "General Settings"
})

```

### AddSection

Creates a section header banner, which can optionally be collidable to hide/show subsequent elements.

```lua
local sectionRef = PrestineLib:AddSection({
    Tab = "Home",
    MainTitle = "Combat Features",
    Collidable = true -- Optional: enables collapsing child items when clicked
})

```

---

## Content Components

### AddParagraph

Displays a structured container with a title and multi-line textual content.

```lua
local paragraph = PrestineLib:AddParagraph({
    Tab = "Home",
    MainTitle = "Information",
    MainContent = "Welcome to the script hub."
})

-- Available Methods:
paragraph:SetContent("Updated text content.")
paragraph:SetTitle("New Title")

```

### AddParagraphBars

Displays progress bars or segmented trackers inside a styled paragraph box.

```lua
local barsCard = PrestineLib:AddParagraphBars({
    Tab = "Home",
    MainTitle = "Statistics",
    MainContent = "Current progress overview:",
    Bars = {
        { Key = "gold", Label = "Gold", Progress = 450, Goal = 1000, Style = "Bar" },
        { Key = "level", Label = "Level", Progress = 8, Goal = 10, Style = "Segments", Segments = 10 }
    }
})

-- Available Methods:
barsCard:SetProgress("gold", 600)
barsCard:SetGoal("gold", 1200)
barsCard:AddBar({ Key = "xp", Label = "XP", Progress = 50, Goal = 100 })
barsCard:SetTitle("Updated Stats")
barsCard:SetContent("New description")

```

---

## Interactive Components

### AddButton

Creates an interactive action button with animations and visual click/hover feedback.

```lua
PrestineLib:AddButton({
    Tab = "Home",
    MainName = "Teleport to Spawn",
    SubTitle = "Instant movement",
    Callback = function()
        print("Button clicked!")
    end
})

```

### AddToggle

Creates a toggle switch with state persistence and optional continuous loop execution (`WhileOn`).

```lua
local myToggle = PrestineLib:AddToggle({
    Tab = "Home",
    MainName = "Auto Farm",
    Description = "Automatically collects items",
    DefaultState = false,
    Callback = function(state)
        print("Toggle state:", state)
    end,
    WhileOn = function()
        -- Code executed continuously while the toggle is active
    end,
    WhileCooldown = 0.2 -- Delay between loop iterations (seconds)
})

-- Available Methods:
myToggle:Set(true)
local currentState = myToggle:Get()

```

### AddTimedToggle

Creates a toggle paired with a configurable duration timer.

```lua
PrestineLib:AddTimedToggle({
    Tab = "Home",
    MainName = "Boost Timer",
    DefaultState = false,
    DefaultDuration = 30,
    DefaultUnit = "s", -- Options: "s" (seconds), "m" (minutes), "h" (hours), "d" (days), "w" (weeks)
    Callback = function(state)
        print("Timed toggle state:", state)
    end
})

```

### AddSlider

Creates an interactive numerical range slider.

```lua
local mySlider = PrestineLib:AddSlider({
    Tab = "Home",
    MainName = "WalkSpeed",
    Min = 16,
    Max = 200,
    Default = 16,
    Callback = function(value)
        print("Slider value changed:", value)
    end
})

-- Available Methods:
mySlider:Set(50)
local currentValue = mySlider:Get()

```

### AddDropdown

Creates a selectable option menu containing a list of strings.

```lua
local myDropdown = PrestineLib:AddDropdown({
    Tab = "Home",
    MainName = "Select Target",
    Options = {"Player1", "Player2", "Player3"},
    Default = "Player1",
    Callback = function(selected)
        print("Dropdown selection:", selected)
    end
})

-- Available Methods:
myDropdown:Set("Player2")
myDropdown:Refresh({"Player1", "Player2", "Player3", "Player4"}, "Player4")
local currentSelection = myDropdown:Get()

```

---

## Notifications

### AddNotification

Displays a standard popup notification message that auto-dismisses after the specified duration.

```lua
PrestineLib:AddNotification({
    TitleText = "Success",
    ContentText = "Your settings have been successfully saved.",
    Duration = 3
})

```

### AddInteractableNotif

Displays an interactive notification with custom choice buttons and timeout handling.

```lua
PrestineLib:AddInteractableNotif({
    TitleText = "Confirmation",
    ContentText = "Are you sure you want to execute this action?",
    Duration = 5, -- Optional timeout
    Choices = {
        {
            Text = "Confirm",
            Callback = function()
                print("Confirmed!")
            end
        },
        {
            Text = "Cancel",
            Callback = function()
                print("Cancelled!")
            end
        }
    },
    OnTimeout = function()
        print("Notification timed out.")
    end
})

```
