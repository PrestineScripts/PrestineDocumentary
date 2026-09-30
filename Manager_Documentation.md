# PrestineManager API Reference

### 1. Setup & Initialization

```lua
local PrestineLib = loadstring(game:HttpGet("https://.../PrestineLib.lua"))()
local PrestineManager = loadstring(game:HttpGet("https://.../PrestineManager.lua"))()

-- Required if using the Config tab
PrestineLib:Set("HubName", "GameIdentifier")

-- Initialize GUI and manager tabs
PrestineManager:Init(PrestineLib, {
    GUIArgs = {
        Title = "Prestine Hub | [" .. game:GetService("MarketplaceService"):GetProductInfo(game.PlaceId, Enum.InfoType.Asset).Name .. "]",
        SubTitle = "Made by R3LIG"
    },
    Tabs = { "Home", "Player", "Performance", "Utility", "Settings", "Config" }, -- Optional: filter tabs
    ExcludeFeatures = { "Infinite Jump" },                                     -- Optional: blacklist
    -- IncludeFeatures = { "Status & Info", "Anti AFK" }                       -- Optional: whitelist
})

```

(References:)

---

### 2. Properties & State

#### `PrestineManager.Config`

| Field | Type | Default | Description |
| --- | --- | --- | --- |
| `TravelMethod`<br> | `string` | `"Teleport"`<br> | Movement method: `"Teleport"`, `"Tween"`, or `"Walking"`.

 |
| `TweenSpeed`<br> | `number` | `150`<br> | Studs-per-second when `TravelMethod = "Tween"`.

 |
| `TeleportDelay`<br> | `number` | `0`<br> | Seconds to wait after a teleport before resolving.

 |
| `QueueMode`<br> | `boolean` | `false`<br> | If `true`, append calls to queue; if `false`, interrupt current action.

 |

#### `PrestineManager.State`

* `State.Busy` (`boolean`): `true` when a movement task is actively running.


* `State.CurrentTask` (`string`): Status identifier (`"Idle"`, `"Running"`, `"Cancelled"`, `"Died"`, `"Respawned"`).



---

### 3. Movement Methods

All movement targets accept `CFrame`, `Vector3`, or a `BasePart`.

* `PrestineManager:Travel(target)`

Moves to destination. Cancels previous movements unless `Config.QueueMode` is enabled.


```lua
PrestineManager:Travel(Vector3.new(0, 50, 0))

```


* `PrestineManager:CustomTravel(target, overrides)`

Executes movement with one-time overrides and reverts back to prior config upon completion.


```lua
PrestineManager:CustomTravel(workspace.Part, {
    Method = "Tween", -- "Teleport" | "Tween" | "Walking"
    Speed = 300,
    TeleportDelay = 0,
    QueueMode = false
})

```


* `PrestineManager:TravelMultiple(targetList)`

Clears active tasks and traverses a list of destinations sequentially.


```lua
PrestineManager:TravelMultiple({ cf1, cf2, cf3 })

```


* `PrestineManager:Cancel()`

Halts active tweens/paths, clears the queue, and sets `State.CurrentTask = "Cancelled"`.


* `PrestineManager:Enqueue(target)` / `PrestineManager:ClearQueue()` / `PrestineManager:StartQueue()`

Direct queue array control.



---

### 4. Configuration & Profiles

* `PrestineManager:SetConfig(key, value)`: Updates a config key with validation.


* `PrestineManager:ApplyProfile(profileName)`: Loads a profile preset from `PrestineManager.Profiles` (contains `"Default"` by default).



---

### 5. Built-in Tabs & Feature Whitelist/Blacklist

Features can be filtered via `IncludeFeatures` (whitelist) or `ExcludeFeatures` (blacklist) in `PrestineManager:Init()` or `PrestineManager:SetupTab()`.

| Tab | Feature Keys (`KnownFeatures`) |
| --- | --- |
| **`Home`**<br> | `"Home Links"`, `"Copy YouTube"`, `"Copy Discord"`, `"Status & Info"`, `"Character Status"`, `"Server Info"`, `"Performance"`, `"Queue Management"`, `"Clear Queue"`, `"Cancel Movement"`<br> |
| **`Player`**<br> | `"Player Properties"`, `"WalkSpeed"`, `"Jump Power"`, `"Infinite Jump"`, `"Player Camera"`, `"Select Player"`, `"Enable Spy POV"`<br> |
| **`Performance`**<br> | `"Rendering Options"`, `"Turn Off Textures"`, `"Turn Off Effects"`, `"Turn Off Lighting"`, `"Turn Off Fog"`, `"Disable Shadows"`, `"Reduce Render Distance"`, `"Disable Water Effects"`, `"Quick Presets"`, `"Low Graphics Preset"`<br> |
| **`Utility`**<br> | `"General Utility"`, `"Anti AFK"`, `"Reset Character"`, `"Position Data"`, `"Copy Position (CFrame)"`, `"Copy Position (Vector3)"`, `"Server Hop"`, `"Join Server Type"`, `"Join Server"`, `"Rejoin Server"`, `"Rejoin New Server"`<br> |
| **`Settings`**<br> | `"Movement Config"`, `"Travel Method"`, `"Tween Speed"`, `"Teleport Delay"`, `"Travel Queue Mode"`, `"Interface Settings"`, `"Toggle UI"`<br> |
| **`Config`**<br> | `"Config Scope"`, `"Scope"`, `"Config Selection"`, `"Select Config"`, `"Config Name"`, `"Config Operations"`, `"Create / Save Config"`, `"Overwrite Selected Config"`, `"Load Selected Config"`, `"Delete Selected Config"`, `"Config Automation"`, `"Set As Autoload"`, `"Auto Save Component Toggles"`<br> |

---

### 6. Storage & File System Details

Requires `readfile`, `writefile`, `isfolder`, `makefolder`, `delfile`, and `listfiles` in executor environment.

* **Local Scope**: Path is `<PrestineLib.gameFolderPath>/<ConfigName>.json`.


* **Global Scope**: Path is `<PrestineLib.mainFolder>/_global/<ConfigName>.json`.


* **Autoload File**: Stores `<Scope>|<ConfigName>` inside `<PrestineLib.gameFolderPath>/_autoload.txt` and loads automatically 1.5 seconds post-init.
