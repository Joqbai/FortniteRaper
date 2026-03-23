<div align="center">
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/lua/lua-original.svg" width="60" height="60"/>
  <h1>FortniteRaper2</h1>
  <p>A sleek, customizable UI library for Roblox games featuring smooth animations, a two-column masonry layout, and rich text support.</p>

  ![Status](https://img.shields.io/badge/status-in%20development-orange)
  ![Language](https://img.shields.io/badge/language-Lua-blue)
  ![Platform](https://img.shields.io/badge/platform-Roblox-red)
</div>

> ⚠️ **This library is still in development. Bugs may occur.**

---

## Table of Contents

- [Setup](#setup)
- [Window](#window)
- [Tabs](#tabs)
- [Groups](#groups)
- [Elements](#elements)
  - [Toggle](#toggle)
  - [Button](#button)
  - [Slider](#slider)
  - [Keypicker](#keypicker)
  - [Dropdown](#dropdown)
  - [Color Picker](#color-picker)
  - [Textbox](#textbox)
  - [Label](#label)
  - [Divider](#divider)
- [Notifications](#notifications)
- [Tooltips](#tooltips)
- [Rich Text](#rich-text)
- [Full Example](#full-example)

---

## Setup

```lua
local Library = loadstring(game:HttpGet('https://raw.githubusercontent.com/Joqbai/FortniteRaper/refs/heads/main/FortniteRaper2'))()
```

---

## Window

```lua
local window = Library:CreateWindow({
    Title = "My UI",
    ToggleKeybind = Enum.KeyCode.RightAlt, -- default: RightAlt
    TitleRichText = nil                    -- optional: rich text styles for the title
})
```

| Property | Type | Default | Description |
|---|---|---|---|
| `Title` | `string` | `"No Title"` | Window title text |
| `ToggleKeybind` | `Enum.KeyCode` | `RightAlt` | Key to show/hide the window |
| `TitleRichText` | `table` | `nil` | Rich text styles applied to the title |

**Window controls:**
- **Drag** — click and drag the top bar to reposition the window
- **Close button** — destroys the entire ScreenGui
- **Minimize button** — hides the window (`Visible = false`)
- **Toggle keybind** — shows/hides the window from anywhere

**Window object properties:**

| Property | Description |
|---|---|
| `window.CreateTab(name, color?)` | Create a new tab |
| `window.CreateGroup(name, tabName)` | Create a group inside a named tab |
| `window.Notify(text, duration, ...)` | Show a notification |
| `window.AddTooltip(element, text, color?)` | Attach a hover tooltip to an element |
| `window.Main` | The root `CanvasGroup` frame |

---

## Tabs

```lua
local tab = window.CreateTab("Main", Color3.fromRGB(255, 255, 255)) -- color is optional
```

Tabs appear in a horizontal scrollable bar at the top of the window. The first tab created is selected automatically.

**Tab object properties:**

| Property | Description |
|---|---|
| `tab.Button` | The tab `TextButton` instance |
| `tab.Container` | The tab frame (contains the scroller) |

---

## Groups

```lua
local group = window.CreateGroup("Settings", "Main") -- second arg = tab name
```

Groups are placed inside the tab using a **two-column masonry layout** — they auto-fill the shorter column. Group height expands automatically to fit their contents.

---

## Elements

### Toggle

An on/off toggle with an optional keybind button.

```lua
group:AddToggle({
    Text = "Enable Feature",
    Default = false,
    Keybind = true,
    Callback = function(state)
        print("Toggled:", state)
    end
})
```

| Property | Type | Default | Description |
|---|---|---|---|
| `Text` | `string` | `"Toggle"` | Label text |
| `Default` | `boolean` | `false` | Initial toggle state |
| `Keybind` | `boolean` | `false` | Show a keybind button next to the toggle |
| `Callback` | `function(bool)` | — | Called with `true`/`false` on change |

> When `Keybind = true`, clicking the keybind button enters binding mode (displays `...`). Press any key to bind, or **Escape** to clear (displays `None`).

---

### Button

A simple clickable button.

```lua
group:AddButton({
    Text = "Click Me",
    Callback = function()
        print("Clicked!")
    end
})
```

| Property | Type | Default | Description |
|---|---|---|---|
| `Text` | `string` | `"Button"` | Label text |
| `Callback` | `function()` | — | Called on click |

---

### Slider

A draggable slider for selecting a numeric value. Also includes a text input box — the user can type a value and press Enter to set it.

```lua
group:AddSlider({
    Text = "Speed",
    Min = 0,
    Max = 100,
    Default = 50,
    Suffix = " units",
    Callback = function(value)
        print("Value:", value)
    end
})
```

| Property | Type | Default | Description |
|---|---|---|---|
| `Text` | `string` | `"Slider"` | Label text |
| `Min` | `number` | `0` | Minimum value |
| `Max` | `number` | `100` | Maximum value |
| `Default` | `number` | `Min` | Initial value |
| `Suffix` | `string` | `""` | Appended to the displayed value (e.g. `"%"`, `" units"`) |
| `Callback` | `function(number)` | — | Called with the current value on change |

---

### Keypicker

A standalone key binding button (not attached to a toggle).

```lua
group:AddKeypicker({
    Text = "Sprint Key",
    Default = Enum.KeyCode.E,
    Callback = function(key)
        -- key is a KeyCode, or nil if cleared
        print("Bound to:", key)
    end
})
```

| Property | Type | Default | Description |
|---|---|---|---|
| `Text` | `string` | `"Keypicker"` | Label text |
| `Default` | `Enum.KeyCode` | `nil` | Initial key binding |
| `Callback` | `function(KeyCode\|nil)` | — | Called with the new key, or `nil` if cleared |

> Click the button to enter binding mode. Press any key to bind, or **Escape** to clear (displays `None`, fires callback with `nil`).

---

### Dropdown

A dropdown for selecting one or multiple options from a list.

```lua
group:AddDropdown({
    Text = "Choose Team",
    Values = {"Red", "Blue", "Green"},
    Default = "Red",
    Multi = false,
    MaxVisibleItems = 8,
    Callback = function(value)
        -- single mode: value is a string
        -- multi mode:  value is a table of strings
        print(value)
    end
})
```

| Property | Type | Default | Description |
|---|---|---|---|
| `Text` | `string` | `"Dropdown"` | Label text |
| `Values` | `table` | `{}` | List of option strings |
| `Default` | `string` | `Values[1]` | Initially selected value |
| `Multi` | `boolean` | `false` | Allow multiple selections |
| `MaxVisibleItems` | `number` | `8` | Max visible items before the menu clips |
| `Callback` | `function` | — | Called with value (string) or values (table) |

**Multi-select display logic:**

| Selected count | Displayed text |
|---|---|
| 0 | `None` |
| 1 | The selected item |
| 2+ | `{Multiple Selected}` |

**Dropdown object methods:**

```lua
local dd = group:AddDropdown({ ... })

dd:SetValues({"A", "B", "C"}) -- replace options list, resets selection
dd:SetValue("B")               -- set selection programmatically (fires callback)
```

---

### Color Picker

An HSV color picker popup with HEX and RGB text inputs.

```lua
group:AddColorPicker({
    Text = "Trail Color",
    Default = Color3.fromRGB(255, 131, 131),
    Callback = function(color)
        print("Color:", color)
    end
})
```

| Property | Type | Default | Description |
|---|---|---|---|
| `Text` | `string` | `"Color Picker"` | Label text |
| `Default` | `Color3` | `Color3.fromRGB(255,131,131)` | Initial color |
| `Callback` | `function(Color3)` | — | Called with the new `Color3` on change |

The popup contains:
- HSV color square + hue bar
- HEX input (e.g. `#FF8383`) — press Enter to apply
- RGB input (e.g. `255,131,131`) — press Enter to apply
- **Copy RGB** / **Copy HEX** buttons (uses `setclipboard` if available)

**Color picker object methods:**

```lua
local cp = group:AddColorPicker({ ... })

cp:SetValue(Color3.fromRGB(0, 255, 0)) -- set color programmatically (fires callback)
```

---

### Textbox

A text input field.

```lua
group:AddTextbox({
    Text = "Player Name",
    Placeholder = "Enter name...",
    Default = "",
    Finished = true,
    Callback = function(text)
        print("Input:", text)
    end
})
```

| Property | Type | Default | Description |
|---|---|---|---|
| `Text` | `string` | `"Textbox"` | Label text (used as placeholder context) |
| `Placeholder` | `string` | `"Enter text..."` | Placeholder text |
| `Default` | `string` | `""` | Initial text value |
| `Finished` | `boolean` | `true` | If `true`: fires callback only on FocusLost/Enter. If `false`: fires on every keystroke |
| `Callback` | `function(string)` | — | Called with the current text |

---

### Label

A non-interactive text label.

```lua
group:AddLabel("Status: Ready", Color3.fromRGB(150, 255, 150))
```

| Argument | Type | Default | Description |
|---|---|---|---|
| `text` | `string` | — | Text to display |
| `color` | `Color3` | White | Text color |

---

### Divider

A thin horizontal separator line.

```lua
group:AddDivider()
```

---

## Notifications

Notifications stack vertically in the top-right corner. Each shows an animated progress bar that shrinks over its duration, then the notification slides away.

```lua
window.Notify("UI Loaded!", 5)

-- Additional arguments are concatenated into the message:
window.Notify("Speed set to: ", currentSpeed, " units", 3)
```

| Argument | Type | Default | Description |
|---|---|---|---|
| `text` | `string` | — | Notification message |
| `duration` | `number` | `5` | Seconds before auto-dismissal |
| `...` | `any` | — | Extra values concatenated onto the message |

---

## Tooltips

Attach a hover tooltip to any UI element. The tooltip follows the cursor.

```lua
local toggle = group:AddToggle({ Text = "Fly", Callback = function() end })
window.AddTooltip(toggle, "Enables fly mode", Color3.fromRGB(255, 255, 100))
```

| Argument | Type | Default | Description |
|---|---|---|---|
| `element` | `Instance` | — | Target UI element |
| `text` | `string` | — | Tooltip message |
| `color` | `Color3` | White | Text color |

---

## Rich Text

The window title supports rich text via the `TitleRichText` property. Styles use character index ranges (1-based, inclusive).

```lua
Library:CreateWindow({
    Title = "MyUI",
    TitleRichText = {
        {Type = "color", Value = Color3.fromRGB(0, 180, 255), Range = {1, 2}},
        {Type = "bold",  Range = {1, 4}}
    }
})
```

**Supported style types:**

| Type | `Value` |
|---|---|
| `color` | `Color3` |
| `font` | Font face name (`string`) |
| `size` | Font size (`number`) |
| `bold` | *(no value required)* |
| `italic` | *(no value required)* |
| `underline` | *(no value required)* |
| `strikethrough` | *(no value required)* |

---

## Full Example

```lua
local Library = loadstring(game:HttpGet('https://raw.githubusercontent.com/Joqbai/FortniteRaper/refs/heads/main/FortniteRaper2'))()

local window = Library:CreateWindow({
    Title = "My Game UI",
    ToggleKeybind = Enum.KeyCode.RightShift
})

local tab = window.CreateTab("Main")
local group = window.CreateGroup("Controls", "Main")

group:AddToggle({
    Text = "God Mode",
    Default = false,
    Keybind = true,
    Callback = function(state)
        print("God Mode:", state)
    end
})

group:AddSlider({
    Text = "Walk Speed",
    Min = 0,
    Max = 100,
    Default = 16,
    Suffix = " studs/s",
    Callback = function(value)
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = value
    end
})

group:AddDropdown({
    Text = "Team",
    Values = {"Red", "Blue", "Spectator"},
    Default = "Red",
    Callback = function(value)
        print("Team:", value)
    end
})

group:AddColorPicker({
    Text = "Trail Color",
    Default = Color3.fromRGB(0, 200, 255),
    Callback = function(color)
        print("Color:", color)
    end
})

group:AddTextbox({
    Text = "Custom Name",
    Placeholder = "Enter name...",
    Finished = true,
    Callback = function(text)
        print("Name:", text)
    end
})

group:AddLabel("Library loaded successfully!", Color3.fromRGB(150, 255, 150))
group:AddDivider()

window.Notify("UI Loaded!", 3)
```

---

## Features

- Smooth animations powered by `TweenService`
- Dark theme with rounded corners throughout
- Two-column masonry group layout
- Search bar (bottom-left) for filtering elements in the active tab by label text
- Draggable window via top bar
- Auto-closing dropdowns and color pickers when scrolling or switching tabs
- Stacking notifications with progress bar timers
- Cursor indicator dot that follows the mouse while the UI is open
