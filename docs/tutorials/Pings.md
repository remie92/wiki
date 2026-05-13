Information on pings

## Unsynced Behavior

With many mods, there is communication between the Minecraft Server and its clients which allows everything to stay in sync. Your client will send certain information to the server, then the server will send that information out to the other connected clients.<br/>
Figura's scripts and models, however, are entirely client-side and not connected to the server.

What does this mean for you, the user? It means that certain information that your client doesn't share with others won't be synchronized for other players.
Some examples:

-   Keybinds
    -   If other clients received all of your keystrokes, it would be a major security issue. The exact keystrokes are never sent, only the result of those keystrokes.
-   Action Wheel
    -   The Action Wheel is a feature added by Figura. Remember how Figura never communicates with the Minecraft Server? It should be obvious why the Action Wheel isn't synced.
-   HostAPI
    -   The HostAPI exclusively contains variables that only you—the owner of the avatar and the owner of the machine running Minecraft—have access to. All functions contained within are vanilla variables that are not synced with the Minecraft Server. They are wrapped in a nice, explicit package stating that they are never synced. This is unlike the PlayerAPI, which you can assume is always synced (except certain cases of things in <code>player:getNbt()</code>)

So how can we sync information with other players if we cannot do it through the Minecraft Server? The answer is Pings.

## General Pings

Pings utilize Figura's Backend to sync information with other clients.
Pings are functions that when called, triggers all other clients to call the same function for their instance of your avatar.

### Ping Rate Limiting

The backend restricts you on how much data you can send over a period of time.
The developer given limits are:

-   1024 bytes per second
-   32 pings per second

If either of these are reached, the backend will ignore any communication from you for some amount of time.

### Pingable Values

Pings can send most primitive types and some userdata types. If you pass in a userdata type that is not listed below, such as [ModelPart](../globals/Models/Models.md), it will turn into <code>nil</code>.
All pingable types use a single byte to represent the type of data that is being sent. This byte is not included in the listed byte totals.

-   <code>nil</code> - 0 Bytes
    -   if a type that is not supported is used as a parameter, it will be replaced with <code>nil</code>.
-   <code>boolean</code> - 0 Bytes
-   <code>integer</code> - 1-4 Bytes
    -   <code>integers</code> only take up as many bytes as it needs.
    -   <code>integers</code> are signed. For example, to only use a single byte the value must be between -128 and 127.
-   <code>double</code> - 8 Bytes
    -   If the number has a decimal at all, or is outside the range of a 4 byte <code>integer</code>, it will be sent as a <code>double</code>.
-   <code>string</code> - 2+n Bytes
    -   <code>strings</code> will always use 2 bytes to store the length.
    -   Ascii characters will be a single byte each.
    -   UTF-8 characters will be multiple bytes per character.
    -   The absolute maximum size of string you can send is <code>65535</code> characters. If a larger string is sent, it will be truncated.
-   <code>table</code> - Too Many Bytes
    -   Every key and value is send as data, resulting in high byte costs.
    -   It is recommended to never send a table over pings.
-   <code>VectorN</code> - 1+8\*N Bytes
    -   Vectors have a single byte that stores the size of the Vector.
    -   Vectors are always assumed to store <code>doubles</code>. If you have a Vector of integers, I recommend sending them as 3 separate arguments instead.
-   <code>MatrixN</code> - 2+8\*W\*H Bytes
    -   Matrices store both the width and height of the matrix, then every value as a <code>double</code>.

### Ping

Below is an example ping.

```lua
function pings.pingName(thing) -- `thing` means that this function accepts a value, which it will refer to as `thing`, as a parameter
    print("Ping")
    print(".")
    print("Data Received:", thing)
    print(".")
    print("Pong")
end
```

It accepts a single variable, which it will print to the chat as an example.

To call it, just call it like any other lua [function](Types/Functions.md).

```lua
pings.pingName("This is a string wooooooooooooooooo")
```

When you as the host call the ping, the function will execute for all other clients with whatever data was passed in, regardless of their current state.<br/>
This means that if you pass in a host-only value to a ping, other clients will also execute that ping given that host-only information.

Do note that if a non-host client reaches a line where a ping gets called, it is completely ignored. No data is sent to the backend, and the contents of the ping will not be executed.

Ping functions can be passed into functions that expect a function as a parameter, such as Action <code>onToggle</code>.

```lua
actionVariable:onToggle(pings.pingName)
```

Remember that we are passing the function itself as a variable. The below would be passing the _return result_ of the ping function, which is nigh guaranteed to be <code>nil</code> as Pings _should never_ return a value.

```lua
--do not do
actionVariable:onToggle(pings.pingName())
```

## Advanced Pings

Situational techniques that may be handy, depending on the use case.

### Ping on Init

Calling a ping function when the script is first loaded is a horrible idea. The ping will only ever execute for other clients when you, the host, load the avatar. It may never be executed on other clients if they haven't loaded your avatar by that time, and it's also unnecessary; if you're doing something when your avatar first starts, there's no unsynced behavior around that, so you can use a normal function.

How do we get around this? Well, when you assign a function to an index in the <code>pings</code> table, the Lua Function gets replaced with a Java Function. Functions cannot be modified, so if we store the function before assigning it to the <code>pings</code> table, we can use it like a regular function, and use the same code as a ping function.

```lua
local function doThing(state)
    models.modelA:setVisible(state)
    models.modelB:setVisible(not state)
end
pings.doThing = doThing
-- doThing and pings.doThing are 2 completely separate values at this point, as the pings table has replaced the index at pings.doThing with a Java Function that wraps the doThing Lua Function.

local keybindState = false
-- I call the local doThing instead of pings.doThing, as pings.doThing is a function that invokes network code.
-- This ensures that the default state is set correctly. If this was a ping function, both models will be visible for other clients until you press the keybind.
doThing(keybindState)
local keyA = keybinds:newKeybind("KeybindName", "key.keyboard.k")
function keyA.press()
    keybindState = not keybindState
    -- We still need to call the ping function in the keybind.
    pings.doThing(keybindState)
end
```

The alternative is to reiterate the <code>models.modelA:setVisible(state) models.modelB:setVisible(not state)</code> part of the ping.<br/>
For larger pings it will be cumbersome to rewrite code that is already defined, which is why this technique is useful.

### Byte Array

There are some situations where you will want to send a large amount of raw bytes, and you need to do it efficiently. The most efficient way is to send a string.

Aside from the 2 constant bytes for the length, a string will always be 1 byte per ascii character (UTF-8 characters are multiple ascii characters, interpreted as a single character). This makes it very consistent in terms of bytes, making it easy to predict and avoid being rate limited.

Below is a basic conversion of a byte array to a string, ready to be pinged and converted back into a byte array on the client's end.

```lua
function pings.receiveData(str)
    local byteArray = table.pack(string.byte(str))
    printTable(byteArray)
end

local packet={}
for i=1,20 do
    table.insert(packet, math.random(0,255))
end
local keyA = keybinds:newKeybind("KeybindName", "key.keyboard.k")
function keyA.press()
    local packedString = string.char(table.unpack(packet))
    pings.receiveData(packedString)
end

```
