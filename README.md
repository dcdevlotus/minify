Automatically [minify](https://en.wikipedia.org/wiki/Minification_(programming)) all client **`Lua`** files when the server starts

## Setup
Download the latest [release](https://github.com/pachxl/minify/releases) and place in your `resources` folder, rename to `minify`<br>
In your server.cfg, add `ensure minify` at the start of your resource list, it is key that this resource starts before any other script you want to use it on.<br>
This __will not__ run this on every resource by default, to enable it, add 
```lua
minify "yes"
```
to the `fxmanifest.lua`<br>
<br>
This will go through **every file** in the `client/` folder, minify the contents of the file, and copy in a new folder called `client_min`, it is important you change this in the `fxmanifest.lua`, so the minified files are loaded.<br>
I would recommend adding `client_min/` to your `.gitignore`
### <u>This will not protect your code</u>
It will only make it harder to read for the average player
```lua
-- before
RegisterNUICallback("spawnVehicle", function(data)
    if IsPedInAnyVehicle(PlayerPedId(), false) then
        TriggerEvent("ui:notification", "error", "You are already in a vehicle")
        return
    end
    PlaySound(-1, "SELECT", "HUD_FRONTEND_DEFAULT_SOUNDSET", 0, 0, 1)
    TriggerServerEvent("arena:spawnVehicle", data.spawncode)
end)

-- after
RegisterNUICallback("spawnVehicle",function(a)if IsPedInAnyVehicle(PlayerPedId(),false)then TriggerEvent("ui:notification","error","You are already in a vehicle")return end;PlaySound(-1,"SELECT","HUD_FRONTEND_DEFAULT_SOUNDSET",0,0,1)TriggerServerEvent("arena:spawnVehicle",a.spawncode)end)
```
