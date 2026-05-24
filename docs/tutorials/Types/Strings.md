A string is a Lua value that represents a sequence of characters.

Strings are not interpreted as code and are treated as literally being characters.

## String Creation

Strings are most often created with quotation marks ("):

```lua
"hello" -- this is a string, as identified by the quotes bracketing it
hello -- not a string
```

But what if you need to include a quotation mark in the string itself? You have two options.
The first option is to use a backslash to "cancel" the quotation mark. Putting a backslash before a special character will
instead interpret that character in its context (in this case, inside a string) instead of its typical code usage (which would end the string).

```lua
"Figura is an \"awesome\" mod!"
```

However, this looks bad and can be hard to read. There is an easier way to make strings with quotation marks in them, and that's by
using a bounding character that is not itself a quotation mark. Lua actually has 3 ways to denote strings: <code>"</code>, <code>'</code>, and <code>\[\[</code> (more on that last one later). Knowing this, we can make a string with quotation marks much easier:

```lua
'Figura is an "awesome" mod!'
```

This is especially useful in circumstances where you need to write a [JSON string](../../globals/Nameplate#using-json), which uses quotation marks.

The final character that makes a string is <code>\[\[</code>. This operator, while more verbose, is useful when you either have a ton of characters like quotation marks and apostrophes that you don't want to prematurely end the string, or when you need a multi-line string. For its former purpose of not being terminated early, <code>=</code> signs can go between the brackets to further distinguish the string. Because of these special properties, backslashes do not escape other characters in these strings.

```lua
local string1 = [['Wow'! It's a "string" with square brackets around it. Extraordinary.]]
local string2 =
    [[
        This string has multiple lines
        and would be displayed as such across multiple lines.
        No other string operator supports this behavior without special characters.
    ]]
local string3 = [=====[This, too, is valid, as long as you use the same number of = symbols.]=====]
local string4 = [[These \'backslashes\' are also in the string, and don't change anything!]]
```

## String Manipulation

The most common method of manipulating string is concatenation, which is the combination of multiple string. In Lua, this is achieved through the <code>..</code> operator. For example:

```lua
local a = 81
local b = 235
print("The equation " .. a .. " + " .. b .. " is equal to " .. a + b)
```

Strings can only be concatenated with other strings and numbers. Other types will error when concatenated with a string.

Lua's <code>string</code> library also comes with a variety of useful function for the manipulation of strings. These functions can be called by directly invoking <code>string.func(args)</code>, but if you call a function on a string with <code>:</code> or <code>.</code> it will use a corresponding string library function (if it exists)—just make sure to wrap string literals in parentheses for this behavior. Some of the most useful functions follow.

-   <code>string.sub(str, pos1, pos2)</code> returns a substring between the given bounds (inclusive)
    -   <code>("ASDFGHIJKL"):sub(2, 4)</code> → <code>SDF</code>
-   <code>string.lower(str)</code> returns a lowercase version of the string
-   <code>string.upper(str)</code> returns an uppercase version of the string
-   <code>string.len(str)</code> returns the length of the string, equivalent to <code>#str</code>
-   <code>string.find(str, pattern)</code> returns either nil or the starting index, ending index, and capture if it is successful
    -   A third argument (number) may be passed for the beginning index to search
    -   A fourth argument (boolean) may be passed to disable special pattern characters in the pattern
-   <code>string.gsub(str, pattern, repl)</code> returns a copy of the string with all instances of <code>pattern</code> replaced by <code>repl</code>
-   <code>string.match(str, pattern)</code> looks for the first match of pattern in the nil, returning the match/capture if successful or nil if unsuccessful
    -   <code>string.gmatch</code> returns an iterator of all matches if you want to capture multiple
-   <code>string.format(str, ...)</code> replaces all "directives" with their corresponding arguments.
    -   Directives are formed with % and a letter: <code>d</code> for decimal, <code>f</code> for floating-point number, and <code>s</code> for string.
    -   <code>string.format("%02d/%02d/%04d", 5, 11, 1990)</code> → 05/11/1990
    -   Note that combinations of numbers function to tell the string how many digits and how much padding are desired

You may have observed use of the term "pattern" in these. While these patterns can simply be plain strings, Lua also has a versatile pattern-matching system similar to regex. To learn more about this, see [PIL](https://www.lua.org/pil/20.2.html).
