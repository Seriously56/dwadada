**BASIC SETUP**
```lua
-- Load the library
local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Seriously56/dwadada/main/Main"))()

-- Create main window
local window = library:window({
    name = "Your Script Name",
    suffix = "tech",           -- Appears after name
    game_name = "Game Name",   -- Bottom left text
    size = UDim2.new(0, 700, 0, 565) -- Window size
})
```

**Creating Tabs**
```lua
-- Single tab
local tab = window:tab({
    name = "Tab Name",
    icon = "rbxassetid://icon_id"  -- Optional
})

-- Multi-section tab (returns multiple objects)
local tab1, tab2, tab3 = window:tab({
    name = "Main Tab",
    tabs = {"Section1", "Section2", "Section3"}
})
```

**Creating Sections**
```lua
-- Basic section
local section = tab:section({
    name = "Section Name",
    side = "left",      -- "left" or "right"
    size = 0.5,         -- Relative size (0-1)
    icon = "rbxassetid://icon_id",
    fading = false,     -- Enable collapsible
    default = true      -- Start expanded if fading
})

-- Collapsible section
local collapsible = tab:section({
    name = "Advanced",
    fading = true,
    default = false
})
```
**Layout Management**
```lua
-- Columns for side-by-side layout
local left_col = tab:column({size = 0.5})
local right_col = tab:column({size = 0.5})

-- Separators in sidebar
window:seperator({name = "Category Name"})
```
**Toggle**
```lua
section:toggle({
    name = "Toggle Name",
    info = "Description text",  -- Optional tooltip
    flag = "unique_flag",
    type = "toggle",           -- "toggle" or "checkbox"
    default = false,
    folding = false,           -- Hide/show other elements
    seperator = true,         -- Add line below
    callback = function(state)
        print("Toggle:", state)
    end
})
```
**Slider**
```lua
section:slider({
    name = "Slider Name",
    flag = "slider_flag",
    min = 0,
    max = 100,
    intervals = 1,            -- Step size
    suffix = "%",             -- Value suffix
    default = 50,
    info = "Slider description",
    seperator = true,
    callback = function(value)
        print("Value:", value)
    end
})
```
**Dropdown**
```lua
section:dropdown({
    name = "Dropdown Name",
    flag = "unique_flag",
    items = {"Option 1", "Option 2", "Option 3"},
    default = "Option 1",  -- Optional
    multi = false,         -- Single selection
    callback = function(selected)
        print("Selected:", selected)
    end
})

section:dropdown({
    name = "Multi Select",
    flag = "multi_flag", 
    items = {"Item 1", "Item 2", "Item 3", "Item 4"},
    default = {"Item 1", "Item 3"},  -- Table for multi-select
    multi = true,  -- Enable multi-selection
    callback = function(selected)
        -- selected is a table of selected items
        print("Selected items:", table.concat(selected, ", "))
    end
})

Required Parameters:
name (string) - Display name of the dropdown

flag (string) - Unique identifier for the dropdown

items (table) - Array of options: {"Option1", "Option2", "Option3"}

callback (function) - Called when selection changes

Optional Parameters:
default (string/table) - Default selection. String for single, table for multi

multi (boolean) - Enable multi-selection (default: false)

seperator (boolean) - Add separator line below (default: false)

myDropdown:refresh_options({"Player3", "Player4", "Player5"})
```
**Color Picker**
```lua
section:colorpicker({
    name = "Color Picker",
    flag = "color_flag",
    color = Color3.fromRGB(255, 0, 0),  -- Default color
    alpha = 0.5,                        -- Transparency (0-1)
    seperator = true,
    callback = function(color, transparency)
        print("Color:", color, "Alpha:", transparency)
    end
})
```
**Keybind**
```lua
section:keybind({
    name = "Keybind",
    flag = "keybind_flag",
    key = Enum.KeyCode.LeftShift,
    mode = "Toggle",          -- "Toggle", "Hold", "Always"
    default = false,          -- Initial state
    ignore_key = false,       -- Ignore key input
    callback = function(state)
        print("Keybind active:", state)
    end
})
```
**Textbox**
```lua
section:textbox({
    name = "Text Input",
    flag = "textbox_flag",
    placeholder = "Type here...",
    default = "Default text",
    visible = true,
    callback = function(text)
        print("Text:", text)
    end
})
```
**Button**
```lua
section:button({
    name = "Button",
    callback = function()
        print("Button clicked!")
        -- Your code here
    end
})
```
**Label**
```lua
section:label({
    name = "Label Text",
    info = "Additional information",
    seperator = true
})
```
**List**
```lua
local list = section:list({
    name = "Options List",
    flag = "list_flag",
    options = {"Option 1", "Option 2", "Option 3"},
    callback = function(selected)
        print("Selected:", selected)
    end
})

-- Update list options
list:refresh_options({"New", "Options"})
```
**Automatic Config Tab**
```lua
-- Adds complete config management
library:init_config(window)
```
**Manual Config Operations**
```lua
-- Save config
local config_data = library:get_config()
writefile("config.cfg", config_data)

-- Load config
local saved_config = readfile("config.cfg")
library:load_config(saved_config)

-- Update config list display
library:update_config_list()
```
**Notifications**
```lua
-- Create notification
library.notifications:create_notification({
    name = "Title",
    info = "Message content",
    lifetime = 3  -- Seconds to display
})

-- Example
library.notifications:create_notification({
    name = "Success",
    info = "Settings saved successfully!",
    lifetime = 5
})
```
**Accessing Values**
```lua
-- All values stored in library.flags
print(library.flags.toggle_flag)      -- Boolean
print(library.flags.slider_flag)      -- Number
print(library.flags.dropdown_flag)    -- String
print(library.flags.color_flag)       -- Table: {Color, Transparency}
print(library.flags.keybind_flag)     -- Table: {mode, key, active}

-- Iterate all flags
for flag, value in pairs(library.flags) do
    print(flag, "=", value)
end
```
**Theme Management**
```lua
-- Change accent color
library:update_theme("accent", Color3.fromHex("FF0035"))
```
**Settings Panel**
```lua
-- Create settings panel (gear icon)
local settings = section:settings({})
```
**EXAMPLE SCRIPT**
```lua
-- Load the library
local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Seriously56/dwadada/main/Main"))()

-- Create main window
local window = library:window({
    name = "My Script",
    suffix = "tech",
    game_name = "Your Game Name",
    size = UDim2.new(0, 700, 0, 565)
})

-- Create tabs
local combat_tab, visuals_tab, misc_tab = window:tab({
    name = "Main",
    tabs = {"Combat", "Visuals", "Misc"}
})

-- COMBAT TAB
local combat_col = combat_tab:column({size = 0.5})
local aimbot_section = combat_col:section({
    name = "Aimbot",
    icon = "rbxassetid://6034767608"
})

aimbot_section:toggle({
    name = "Enable Aimbot",
    flag = "aimbot_enabled",
    default = false,
    callback = function(state)
        print("Aimbot:", state)
    end
})

aimbot_section:slider({
    name = "Aimbot FOV",
    flag = "aimbot_fov",
    min = 1,
    max = 360,
    default = 90,
    suffix = "°",
    callback = function(value)
        print("FOV:", value)
    end
})

aimbot_section:keybind({
    name = "Aimbot Key",
    flag = "aimbot_key",
    callback = function(state)
        print("Aimbot key:", state)
    end
})

-- VISUALS TAB
local visuals_col = visuals_tab:column({size = 0.5})
local esp_section = visuals_col:section({
    name = "ESP",
    icon = "rbxassetid://6034767608"
})

esp_section:toggle({
    name = "Player ESP",
    flag = "esp_enabled",
    default = true,
    callback = function(state)
        print("ESP:", state)
    end
})

esp_section:colorpicker({
    name = "ESP Color",
    flag = "esp_color",
    color = Color3.fromRGB(0, 255, 0),
    callback = function(color, transparency)
        print("ESP Color:", color, "Transparency:", transparency)
    end
})

esp_section:dropdown({
    name = "ESP Type",
    flag = "esp_type",
    options = {"Box", "Tracer", "Name", "All"},
    default = "Box",
    callback = function(selected)
        print("ESP Type:", selected)
    end
})

-- MISC TAB
local misc_col = misc_tab:column({size = 0.5})
local movement_section = misc_col:section({
    name = "Movement",
    icon = "rbxassetid://6034767608"
})

movement_section:toggle({
    name = "Speed Hack",
    flag = "speed_enabled",
    default = false,
    callback = function(state)
        print("Speed Hack:", state)
    end
})

movement_section:slider({
    name = "Speed Multiplier",
    flag = "speed_multiplier",
    min = 1,
    max = 10,
    default = 2,
    callback = function(value)
        print("Speed Multiplier:", value)
    end
})

movement_section:button({
    name = "Reset Character",
    callback = function()
        print("Resetting character...")
        -- Your reset code here
    end
})

-- Add config system (optional)
library:init_config(window)

-- Show success notification
library.notifications:create_notification({
    name = "Script Loaded",
    info = "UI successfully initialized!",
    lifetime = 3
})
```
