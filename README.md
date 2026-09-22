# KEA Syntax

KEA is a structured data format designed to remain simple and readable while providing additional syntax and built-in functions.

KEA files use the `.kea` extension.

---

## 1. File Structure

Every KEA file starts with the following header:

```kea
[keafile]
```

A standard KEA document is enclosed between `_ENTRY_` and `_END_`:

```kea
[keafile]

_ENTRY_

name: "My application",
version: "1.0",
enabled: true

_END_
```

The general structure is:

```text
[keafile]

_ENTRY_

key: value
key: value
key: value

_END_
```

---

## 2. Header

The `[keafile]` header identifies a file as a KEA document.

```kea
[keafile]
```

It must appear at the beginning of the file.

---

## 3. Entries

The `_ENTRY_` marker starts the main KEA entry.

```kea
_ENTRY_
```

The `_END_` marker terminates it.

```kea
_END_
```

Example:

```kea
[keafile]

_ENTRY_

name: "Example",
version: "1.0"

_END_
```

A KEA document currently contains one main entry block.

---

## 4. Keys

Keys identify values.

A key can be an unquoted identifier:

```kea
name: "KEA"
version: "1.0"
enabled: true
```

Keys may contain letters, numbers and underscores.

```kea
application_name: "My App"
version_2: "2.0"
```

A key can also be written as a quoted string:

```kea
"application name": "My App"
"version number": "1.0"
```

This is useful when a key contains spaces or other characters that are not normally valid in an identifier.

---

## 5. Key-Value Separator

The `:` character separates a key from its value.

```kea
name: "KEA"
version: "1.0"
count: 42
```

The general syntax is:

```text
key: value
```

---

# 6. Values

KEA supports several basic value types.

### String

```kea
name: "KEA"
description: "A structured data format"
```

Strings are enclosed in double quotes.

### Integer

```kea
count: 42
port: 8080
```

### Floating-point number

```kea
frequency: 14.074
temperature: 21.5
```

### Boolean

KEA supports two boolean values:

```kea
enabled: true
disabled: false
```

### Null

A value can explicitly contain no value:

```kea
value: null
```

---

# 7. Strings

Strings use double quotes:

```kea
name: "Hello world"
```

They can contain spaces:

```kea
message: "This is a KEA string"
```

Special characters can be escaped using backslashes.

```kea
message: "Hello \"world\""
```

---

# 8. Arrays

Arrays are enclosed in square brackets:

```kea
values: [
    "one",
    "two",
    "three"
]
```

Arrays can contain different types of values:

```kea
values: [
    "KEA",
    42,
    3.14,
    true,
    null
]
```

Arrays can also contain objects:

```kea
users: [
    {
        name: "Alice",
        id: 1
    },
    {
        name: "Bob",
        id: 2
    }
]
```

---

## 8.1 Array Separators

Array elements can be separated using commas:

```kea
values: [
    one,
    two,
    three
]
```

Semicolons are also supported:

```kea
values: [
    one;
    two;
    three
]
```

Trailing separators are allowed:

```kea
values: [
    one,
    two,
    three,
]
```

The same applies when using semicolons:

```kea
values: [
    one;
    two;
    three;
]
```

---

# 9. Objects

Objects are enclosed in curly braces:

```kea
application: {
    name: "KEA",
    version: "1.0",
    enabled: true
}
```

Objects contain key-value pairs using the same `:` syntax as the main entry.

Objects can be nested:

```kea
application: {
    name: "KEA",
    version: {
        major: 1,
        minor: 0,
        patch: 0
    }
}
```

---

## 9.1 Object Separators

Object properties can be separated with commas:

```kea
application: {
    name: "KEA",
    version: "1.0",
    enabled: true
}
```

Or semicolons:

```kea
application: {
    name: "KEA";
    version: "1.0";
    enabled: true
}
```

Trailing separators are allowed:

```kea
application: {
    name: "KEA",
    version: "1.0",
    enabled: true,
}
```

---

# 10. Separators

KEA accepts both `,` and `;` as separators between entries.

For example:

```kea
_ENTRY_

name: "KEA",
version: "1.0",
enabled: true

_END_
```

The same structure can be written using semicolons:

```kea
_ENTRY_

name: "KEA";
version: "1.0";
enabled: true

_END_
```

They can also be mixed:

```kea
_ENTRY_

name: "KEA",
version: "1.0";
enabled: true,

_END_
```

Trailing separators are allowed.

---

# 11. KEA Functions

KEA provides built-in functions that can be used directly as values.

The current built-in functions are:

* `range()`
* `random()`
* `rr()`

Functions use parentheses:

```kea
value: function(...)
```

---

# 12. `range()`

`range()` generates a random integer inside a specified range.

Syntax:

```kea
range("MIN-MAX")
```

Example:

```kea
number: range("10-250")
```

This generates an integer between `10` and `250`, inclusive.

For example, the result could be:

```text
42
```

or:

```text
173
```

but never below `10` or above `250`.

---

# 13. `random()`

`random()` randomly selects one value from the provided arguments.

Syntax:

```kea
random(value1, value2, value3)
```

Example:

```kea
mode: random("FM", "AM", "USB", "LSB")
```

Possible results include:

```text
FM
```

```text
AM
```

```text
USB
```

or:

```text
LSB
```

`random()` can be used with different value types:

```kea
value: random("hello", "world", 42, true)
```

The function returns one of the supplied values.

---

# 14. `rr()`

`rr()` generates a random integer between two numeric values.

Syntax:

```kea
rr(MIN, MAX)
```

Example:

```kea
number: rr(12, 500)
```

The result is an integer between `12` and `500`, inclusive.

The arguments may also be written as strings representing numbers:

```kea
number: rr("12", "500")
```

---

# 15. Functions Inside Arrays

KEA functions can be used inside arrays.

```kea
values: [
    rr(1, 100),
    random("FM", "AM", "USB"),
    range("100-200")
]
```

Each function is evaluated when the document is parsed.

---

# 16. Functions Inside Objects

Functions can also be used inside objects:

```kea
radio: {
    mode: random("FM", "AM", "USB", "LSB"),
    frequency: rr(1000, 2000),
    signal: range("10-100")
}
```

---

# 17. Nested Structures

Arrays and objects can be nested together.

```kea
application: {
    name: "KEA",
    versions: [
        {
            major: 1,
            minor: 0
        },
        {
            major: 1,
            minor: 1
        }
    ]
}
```

A function can also appear at any supported value position:

```kea
configuration: {
    mode: random("FM", "AM", "USB"),
    values: [
        rr(10, 100),
        range("100-500")
    ]
}
```

---

# 18. Complete Example

A complete KEA document can combine all of these features:

```kea
[keafile]

_ENTRY_

id: "wbnaql",
name: "NameOfApp",
version: "1.10",
client: 1,

enabled: true,
debug: false,
optional: null,

random_number: range("10-250"),
random_mode: random("FM", "AM", "USB", "LSB"),
random_frequency: rr(12, 500),

"random in range": rr("12", "500"),

"multiple entries": [
    "one",
    "two",
    "three",
    "a lot of entries",
],

configuration: {
    name: "Main configuration",
    version: 1,
    enabled: true,

    values: [
        rr(1, 100),
        random("A", "B", "C"),
        range("100-500"),
    ],
}

_END_
```

---

# 19. Minimal KEA File

The smallest basic KEA document is:

```kea
[keafile]

_ENTRY_

_END_
```

---

# 20. Syntax Overview

| Syntax      | Description                        |
| ----------- | ---------------------------------- |
| `[keafile]` | KEA file header                    |
| `_ENTRY_`   | Starts the main entry              |
| `_END_`     | Ends the main entry                |
| `:`         | Separates keys and values          |
| `,`         | Value/entry separator              |
| `;`         | Alternative value/entry separator  |
| `"`         | String delimiter                   |
| `[]`        | Array                              |
| `{}`        | Object                             |
| `()`        | Function arguments                 |
| `true`      | Boolean true                       |
| `false`     | Boolean false                      |
| `null`      | Null value                         |
| `range()`   | Random integer from a string range |
| `random()`  | Randomly selects a value           |
| `rr()`      | Random integer between two values  |

---

# 21. Design Philosophy

KEA is intentionally permissive.

The syntax is designed to be:

* **Human-readable**
* **Easy to write**
* **Easy to parse**
* **More expressive than plain JSON**
* **Suitable for configuration and structured data**
* **Flexible with separators**
* **Capable of evaluating built-in functions**

For example, these are all valid separator styles:

```kea
name: "KEA",
version: "1.0",
enabled: true
```

```kea
name: "KEA";
version: "1.0";
enabled: true
```

and:

```kea
name: "KEA",
version: "1.0";
enabled: true,
```

The goal is to keep KEA convenient to write without requiring excessive punctuation.

---

# 22. File Extension

KEA files use:

```text
.kea, .keaos, .keams and .keafile
```

Example:

```text
config.kea
settings.keaos
application.keams
data.keafile
```

The `[keafile]` header identifies the content as a KEA document regardless of the filename.
