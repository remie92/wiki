A number is a Lua value that represents a real number.

Although Lua doesn't have an integer type, some methods may ask for integers, meaning they want a whole number.

```lua
local myNumber = 5
local anotherNumber = 72.3
```

Lua supports math operators and follows a standard order of operations, meaning the following code will output -13.

```lua
local result = 8 - 8 * 3 + 3
```

One common operator that you may not be familiar with is <code>%</code>, which is the modulo operator. This operator can essentially be thought of as a remainder function. A typical approach to run something every few ticks uses this operator:

```lua
function events.tick()
    if world.getTime() % 20 == 0 then -- read: if the amount of passed ticks is divisible by 20 (so every 20 ticks), do something.
        -- do something
    end
end
```

Lua also comes with a <code>math</code> library which contains many helpful functions for manipulating numbers (plus a few added by figura).
It's important to note that all trigonometric functions intake and output radians, whereas many Figura functions work in degrees.
