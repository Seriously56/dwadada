#BASIC SETUP
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
