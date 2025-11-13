Basic Setup
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
Window & Layout
```
Creating Tabs
lua
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
Creating Sections
lua
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
Layout Management
lua
-- Columns for side-by-side layout
local left_col = tab:column({size = 0.5})
local right_col = tab:column({size = 0.5})

-- Separators in sidebar
window:seperator({name = "Category Name"})
UI Elements
1. Toggle
lua
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
2. Slider
lua
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
3. Dropdown
lua
-- Single selection
local dropdown = section:dropdown({
    name = "Dropdown",
    flag = "dropdown_flag",
    options = {"Option 1", "Option 2", "Option 3"},
    default = "Option 1",
    width = 130,              -- Dropdown width
    multi = false,            -- Single selection
    scrolling = false,        -- Enable scrolling
    info = "Choose an option",
    seperator = true,
    callback = function(selected)
        print("Selected:", selected)
    end
})

-- Multi-selection
local multi_dropdown = section:dropdown({
    name = "Multi Select",
    flag = "multi_flag",
    options = {"Item 1", "Item 2", "Item 3"},
    multi = true,
    default = {"Item 1"},
    callback = function(selected)
        print("Selected:", table.concat(selected, ", "))
    end
})

-- Update options dynamically
dropdown:refresh_options({"New", "Options", "List"})
4. Color Picker
lua
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
5. Keybind
lua
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
6. Textbox
lua
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
7. Button
lua
section:button({
    name = "Button",
    callback = function()
        print("Button clicked!")
        -- Your code here
    end
})
8. Label
lua
section:label({
    name = "Label Text",
    info = "Additional information",
    seperator = true
})
9. List
lua
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
Configuration System
Automatic Config Tab
lua
-- Adds complete config management
library:init_config(window)
Manual Config Operations
lua
-- Save config
local config_data = library:get_config()
writefile("config.cfg", config_data)

-- Load config
local saved_config = readfile("config.cfg")
library:load_config(saved_config)

-- Update config list display
library:update_config_list()
Notifications
lua
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
Utility Functions
Accessing Values
lua
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
Theme Management
lua
-- Change accent color
library:update_theme("accent", Color3.fromHex("FF0035"))
Settings Panel
lua
-- Create settings panel (gear icon)
local settings = section:settings({})
Complete Example
lua
local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Seriously56/dwadada/main/Main"))()

local window = library:window({
    name = "My Script",
    suffix = "tech",
    game_name = "Example Game"
})

local combat, visuals, misc = window:tab({
    name = "Main",
    tabs = {"Combat", "Visuals", "Misc"}
})

-- Combat Tab
combat:section({name = "Aimbot"}):toggle({
    name = "Enable Aimbot",
    flag = "aimbot",
    default = false
})

combat:section({name = "Settings"}):slider({
    name = "Aimbot FOV",
    flag = "aimbot_fov",
    min = 1,
    max = 360,
    default = 90
})

-- Visuals Tab
visuals:section({name = "ESP"}):toggle({
    name = "Player ESP",
    flag = "esp",
    default = true
})

visuals:section({name = "Colors"}):colorpicker({
    name = "ESP Color",
    flag = "esp_color",
    color = Color3.fromRGB(0, 255, 0)
})

-- Misc Tab
misc:section({name = "Settings"}):keybind({
    name = "UI Toggle",
    flag = "ui_toggle",
    key = Enum.KeyCode.Insert
})

misc:section({name = "Utilities"}):button({
    name = "Print All Flags",
    callback = function()
        for flag, value in pairs(library.flags) do
            print(flag, "=", value)
        end
    end
})

-- Add config system
library:init_config(window)
