<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/lua/lua-original.svg" width="40" height="40"/> <img src="https://cdn.discordapp.com/attachments/1345536244108755025/1411903388941025351/goongoongagnaan.png?ex=68b658ff&is=68b5077f&hm=05d6c960fa8e06fee770b025333559df55cf7cb897da8f349dac578bcba694e0&" width="40" height="40"/> 


# FortniteRaper2 - Roblox UI Library

A sleek, customizable UI library for Roblox games, featuring animated elements and rich text support.

***⚠️PLEASE NOTE THAT HIS UI LIBRARY IS STILL IN DEVELOPMENT SO BUGS MAY OCCUR.⚠️***


## Setup

Load the library using:

```lua
loadstring(game:HttpGet('https://raw.githubusercontent.com/Joqbai/FortniteRaper/refs/heads/main/FortniteRaper2'))()
```

Create a window:

```lua
local Library = loadstring(game:HttpGet('https://raw.githubusercontent.com/Joqbai/FortniteRaper/refs/heads/main/FortniteRaper2'))()
local window = Library:CreateWindow({
    Title = "My UI Window",
    ToggleKeybind = Enum.KeyCode.RightAlt
})
```

- **Title**: Window title (default: "No Title").
- **ToggleKeybind**: Key to toggle visibility (default: `RightAlt`).

## Tabs and Groups

Organize elements with tabs and groups:

```lua
local tab = window:CreateTab("Main Tab")
local group = tab:CreateGroup("Settings")
```

## UI Elements

Add interactive elements to groups. Many support rich text (e.g., colored labels).

### Toggle Button
On/off button with optional keybind.

```lua
group:AddToggle({
    Text = "Enable Feature",
    Callback = function(state) print("Toggled: ", state) end,
    Default = false,
    Keybind = true
})
```

- **Text**: Label (supports rich text).
- **Callback**: Called with state (`true`/`false`).
- **Default**: Initial state.
- **Keybind**: Enables key binding.

### Simple Button
Clickable button.

```lua
group:AddButton({
    Text = "Click Me",
    Callback = function() print("Button clicked!") end
})
```

- **Text**: Label (supports rich text).
- **Callback**: Called on click.

### Slider
Select a value in a range.

```lua
group:AddSlider({
    Text = "Slider",
    Callback = function(value) print("Value: ", value) end,
    Min = 0,
    Max = 100,
    Default = 50,
    Suffix = "%"
})
```

- **Text**: Label (supports rich text).
- **Callback**: Called with value.
- **Min/Max**: Range.
- **Default**: Initial value.
- **Suffix**: Appended to value.

### Keypicker
Bind a keyboard key.

```lua
group:AddKeypicker({
    Text = "Action Key",
    Callback = function(key) print("Key: ", key) end,
    Default = Enum.KeyCode.E
})
```

- **Text**: Label (supports rich text).
- **Callback**: Called with key.
- **Default**: Initial key.

### Dropdown
Select one or multiple options.

```lua
group:AddDropdown({
    Text = "Select Option",
    Callback = function(value) print("Selected: ", value) end,
    Values = {"Option 1", "Option 2", "Option 3"},
    Default = "Option 1",
    Multi = false
})
```

- **Text**: Label (supports rich text).
- **Callback**: Called with value(s).
- **Values**: Options list.
- **Default**: Initial selection.
- **Multi**: Allow multiple selections.

### Color Picker
Select colors with HSV and HEX/RGB input.

```lua
group:AddColorPicker({
    Text = "Pick Color",
    Callback = function(color) print("Color: ", color) end,
    Default = Color3.fromRGB(255, 131, 131)
})
```

- **Text**: Label (supports rich text).
- **Callback**: Called with `Color3`.
- **Default**: Initial color.

### Label
Non-interactive text.

```lua
group:AddLabel("Status: Ready")
```

- **Text**: Label (supports rich text).

### Divider
Horizontal separator.

```lua
group:AddDivider()
```

## Notifications

Show temporary notifications:

```lua
window:Notify("Welcome!", 5)
```

- **Text**: Message (concatenates additional arguments).
- **Duration**: Seconds before disappearing (default: 5).

## Tooltips

Add tooltips to elements:

```lua
window:AddTooltip(element, "This is a tooltip!", Color3.fromRGB(255, 255, 255))
```

- **Element**: Target UI element.
- **Text**: Tooltip message.
- **Color**: Text color (default: white).

## Rich Text

Customize labels with rich text:

```lua
group:AddButton({
    Text = "Colored Button",
    Styles = {{Type = "color", Value = Color3.fromRGB(255, 151, 66), Range = {1, 7}}}
})
```

- **Styles**: Supports `color`, `font`, `size`, `bold`, `italic`, `underline`, `strikethrough`.
- **Value**: E.g., `Color3` for color, string for font.
- **Range**: Text indices to format.

## Example

```lua
local Library = loadstring(game:HttpGet('https://raw.githubusercontent.com/Joqbai/FortniteRaper/refs/heads/main/FortniteRaper2'))()
local window = Library:CreateWindow({Title = "My Game UI", ToggleKeybind = Enum.KeyCode.RightShift})
local tab = window:CreateTab("Main")
local group = tab:CreateGroup("Controls")

group:AddToggle({
    Text = "Toggle Button",
    Callback = function(state) print("God Mode: ", state) end,
    Default = false,
    Keybind = true
})

group:AddSlider({
    Text = "Slider",
    Callback = function(value) print("Speed: ", value) end,
    Min = 0,
    Max = 100,
    Default = 50,
    Suffix = " units"
})

group:AddColorPicker({
    Text = "Color Picker",
    Callback = function(color) print("Color: ", color) end,
    Default = Color3.fromRGB(0, 255, 0)
})

window:Notify("UI Loaded!", 3)
```

## Features

- Smooth animations via `TweenService`.
- Dark theme with rounded corners.
- Search bar for filtering elements.
- Tooltips and notifications for enhanced UX.

FortniteRaper2 offers a modern, flexible UI framework for Roblox games with rich customization options.
