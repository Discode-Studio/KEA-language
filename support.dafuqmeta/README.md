# DAFUQMETA Syntax

DAFUQMETA is a lightweight metadata and configuration format designed to remain simple, readable, and flexible.

DAFUQMETA files use the `.dafuqmeta` extension.

The format can represent metadata, configuration values, lists, nested structures, and free-form text.

---

# 1. File Structure

Every DAFUQMETA file starts with:

```dafuqmeta
_FILE_START_
```

and ends with:

```dafuqmeta
_FILE_END_
```

A basic DAFUQMETA document has the following structure:

```text
_FILE_START_

document content

_FILE_END_
```

For example:

```dafuqmeta
_FILE_START_

(
    Name: "Example";
    Version: "1.0";
)

_FILE_END_
```

The `_FILE_START_` and `_FILE_END_` markers define the boundaries of the file.

---

# 2. File Markers

## 2.1 `_FILE_START_`

`_FILE_START_` marks the beginning of a DAFUQMETA document.

```dafuqmeta
_FILE_START_
```

It is normally placed at the beginning of the file.

---

## 2.2 `_FILE_END_`

`_FILE_END_` marks the end of a DAFUQMETA document.

```dafuqmeta
_FILE_END_
```

It is normally placed after the document content.

---

# 3. Keys

DAFUQMETA uses keys to identify values.

A key is followed by a colon:

```dafuqmeta
Name: "Example";
Version: "1.0";
Enabled: True;
```

The general syntax is:

```text
Key: Value
```

Examples of generic keys include:

```dafuqmeta
Name
Version
Description
Enabled
Identifier
Path
URL
Count
```

Keys may also contain characters such as underscores:

```dafuqmeta
Profile_Name: "Example";
File_Path: "/example/file.txt";
```

---

# 4. Key-Value Separator

The `:` character separates a key from its value.

```dafuqmeta
Name: "Example";
Version: "1.0";
Count: 42;
```

The general form is:

```text
key: value
```

---

# 5. Separators

The semicolon (`;`) is used to separate properties.

```dafuqmeta
(
    Name: "Example";
    Version: "1.0";
    Enabled: True;
)
```

The same syntax can be used inside nested structures:

```dafuqmeta
{
    Name: "Example";
    Version: "1.0";
}
```

---

# 6. Strings

Strings are enclosed in double quotes.

```dafuqmeta
Name: "Example";
Description: "This is an example";
Version: "1.0";
```

Strings can contain spaces:

```dafuqmeta
Title: "An example title";
```

They can also contain various special characters:

```dafuqmeta
Message: "Hello, world!";
```

---

# 7. Empty Strings

An empty string is represented using two double quotes:

```dafuqmeta
Description: "";
```

This represents a string containing no characters.

---

# 8. Boolean Values

Boolean values can be represented using:

```dafuqmeta
True
```

and:

```dafuqmeta
False
```

For example:

```dafuqmeta
Enabled: True;
Debug: False;
```

Boolean values are written without quotation marks.

---

# 9. Numeric Values

Numbers can be written directly as values.

For example:

```dafuqmeta
Count: 42;
Views: 100;
Offset: 0;
```

A numeric value differs syntactically from a string:

```dafuqmeta
Count: 42;
```

versus:

```dafuqmeta
Count: "42";
```

The first contains a numeric literal, while the second contains a string.

---

# 10. Objects

Curly braces (`{}`) can be used to group structured data.

Example:

```dafuqmeta
{
    Name: "Example";
    Version: "1.0";
    Enabled: True;
}
```

An object can contain multiple key-value pairs:

```dafuqmeta
{
    ID: "12345";
    Name: "Example";
    Count: 10;
}
```

Objects can also be assigned to keys:

```dafuqmeta
Configuration: {
    Name: "Example";
    Version: "1.0";
    Enabled: True;
};
```

---

# 11. Parenthesized Structures

Parentheses (`()`) can be used as a container for a group of properties.

Example:

```dafuqmeta
_FILE_START_

(
    Name: "Example";
    Version: "1.0";
    Enabled: True;
)

_FILE_END_
```

A parenthesized structure may contain multiple key-value pairs:

```dafuqmeta
(
    Name: "Example";
    Version: "1.0";
    Description: "Example data";
)
```

Parenthesized structures can also contain nested structures.

---

# 12. Arrays

Square brackets (`[]`) are used for list-like structures.

Example:

```dafuqmeta
Values: [
    "One";
    "Two";
    "Three";
];
```

An array can contain multiple values.

For example:

```dafuqmeta
Numbers: [
    1;
    2;
    3;
];
```

Arrays can also contain structured values:

```dafuqmeta
Items: [
    {
        ID: "001";
        Name: "First";
    };

    {
        ID: "002";
        Name: "Second";
    };
];
```

---

# 13. Empty Arrays

An empty array can be represented as:

```dafuqmeta
Items: [

];
```

This can be used when a field exists but currently contains no elements.

---

# 14. Nested Structures

DAFUQMETA supports nested structures.

For example:

```dafuqmeta
Application: {
    Name: "Example";
    Version: "1.0";
    Settings: {
        Enabled: True;
        Debug: False;
    };
};
```

Arrays can also contain nested structures:

```dafuqmeta
Items: [
    {
        Name: "First";
        Settings: {
            Enabled: True;
        };
    };

    {
        Name: "Second";
        Settings: {
            Enabled: False;
        };
    };
];
```

---

# 15. Arrays of Structured Data

A list can contain multiple structured entries.

```dafuqmeta
Users: [
    {
        ID: "001";
        Name: "User One";
    };

    {
        ID: "002";
        Name: "User Two";
    };

    {
        ID: "003";
        Name: "User Three";
    };
];
```

This makes arrays useful for storing collections of metadata.

---

# 16. Free-Form Text

DAFUQMETA can also contain text that is not necessarily represented as a conventional quoted string.

For example:

```dafuqmeta
Description: [
    This is an example description.
    It can contain multiple lines.
    Additional information can be placed here.
];
```

This can be useful for long descriptions, notes, documentation, or other human-readable metadata.

The exact parsing behavior of free-form text depends on the implementation.

---

# 17. URLs

URLs can be stored as strings:

```dafuqmeta
Website: "https://example.com/";
```

They may also appear inside free-form text:

```dafuqmeta
Description: [
    Website:
    https://example.com/
];
```

---

# 18. File Paths

File paths can be stored as strings.

For example:

```dafuqmeta
Path: "/example/assets/image.png";
```

A path containing spaces can also be represented:

```dafuqmeta
Path: "/example/assets/my image.png";
```

Windows-style paths can similarly be stored as strings:

```dafuqmeta
Path: "C:/Example/Assets/Image.png";
```

---

# 19. Nested Arrays

Arrays can contain other arrays.

```dafuqmeta
Values: [
    [
        "A";
        "B";
    ];

    [
        "C";
        "D";
    ];
];
```

This allows multidimensional or grouped data to be represented.

---

# 20. Nested Objects

Objects can contain other objects.

```dafuqmeta
Configuration: {
    Application: {
        Name: "Example";
        Version: "1.0";
    };

    Settings: {
        Enabled: True;
        Debug: False;
    };
};
```

---

# 21. Mixed Structures

Arrays and objects can be combined.

For example:

```dafuqmeta
Application: {
    Name: "Example";

    Modules: [
        {
            Name: "Module A";
            Enabled: True;
        };

        {
            Name: "Module B";
            Enabled: False;
        };
    ];
};
```

This allows more complex metadata structures to be represented.

---

# 22. Multiple Properties on a Line

Multiple properties can appear on the same line when separated correctly.

For example:

```dafuqmeta
Name: "Example"; Version: "1.0"; Enabled: True;
```

The same information can be formatted across multiple lines:

```dafuqmeta
Name: "Example";
Version: "1.0";
Enabled: True;
```

Whitespace and line breaks can therefore be used to improve readability.

---

# 23. Whitespace and Formatting

DAFUQMETA examples can be formatted with indentation and line breaks.

For example:

```dafuqmeta
Application: {
    Name: "Example";
    Version: "1.0";

    Settings: {
        Enabled: True;
        Debug: False;
    };
};
```

The indentation is primarily intended for human readability.

A compact representation can also be used:

```dafuqmeta
Application: { Name: "Example"; Version: "1.0"; Enabled: True; };
```

---

# 24. Metadata Example

A simple metadata document could look like:

```dafuqmeta
_FILE_START_
{
    ID: "123456";
    Title: "Example title";
    Description: "";
    Date: "01/01/2026";
    Count: 42;
    Enabled: True;
    Tags: [
        "Example";
        "Test";
        "Metadata";
    ];
}
_FILE_END_
```

All values in this example are fictional.

---

# 25. Configuration Example

DAFUQMETA can also represent configuration data:

```dafuqmeta
_FILE_START_
(
    Format: "Example";
    Version: "1.0";
    Settings: {
        Enabled: True;
        Debug: False;
        Path: "/example/data";
    };
)
_FILE_END_
```

---

# 26. Structured Collection Example

A larger collection can be represented using nested structures:

```dafuqmeta
_FILE_START_
(
    Items: [
        {
            ID: "001";
            Name: "Item One";
            Enabled: True;
        };

        {
            ID: "002";
            Name: "Item Two";
            Enabled: False;
        };

        {
            ID: "003";
            Name: "Item Three";
            Enabled: True;
        };
    ];
)
_FILE_END_
```

---

# 27. Minimal DAFUQMETA File

The minimal file structure is:

```dafuqmeta
_FILE_START_

_FILE_END_
```

A minimal file containing a parenthesized structure is:

```dafuqmeta
_FILE_START_

(

)

_FILE_END_
```

---

# 28. Complete Example

A complete generic DAFUQMETA document can combine strings, numbers, booleans, arrays, objects, and nested structures:

```dafuqmeta
_FILE_START_

(
    Name: "Example Application";
    Version: "1.0.0";
    Enabled: True;

    Description: [
        This is a generic example.
        No real-world metadata is used here.
    ];

    Configuration: {
        Debug: False;
        Path: "/example/data";

        Options: [
            "Option A";
            "Option B";
            "Option C";
        ];
    };

    Items: [
        {
            ID: "001";
            Name: "First Item";
            Count: 10;
        };

        {
            ID: "002";
            Name: "Second Item";
            Count: 20;
        };
    ];
)

_FILE_END_
```

---

# 29. Syntax Overview

| Syntax         | Description                           |
| -------------- | ------------------------------------- |
| `_FILE_START_` | Starts a DAFUQMETA file               |
| `_FILE_END_`   | Ends a DAFUQMETA file                 |
| `:`            | Separates a key from a value          |
| `;`            | Separates properties or values        |
| `"`            | String delimiter                      |
| `()`           | Parenthesized structure               |
| `[]`           | Array / list-like structure           |
| `{}`           | Object / structured data              |
| `True`         | Boolean true                          |
| `False`        | Boolean false                         |
| `""`           | Empty string                          |
| `123`          | Numeric value                         |
| `==`           | Comparison operator, where supported  |
| `&`            | Expression separator, where supported |

---

# 30. File Extension

DAFUQMETA files use:

```text
.dafuqmeta
```

Examples:

```text
metadata.dafuqmeta
config.dafuqmeta
video.dafuqmeta
channel.dafuqmeta
```

The `_FILE_START_` and `_FILE_END_` markers define the DAFUQMETA document structure.

---

# 31. VS Code Integration

A DAFUQMETA project can provide a VS Code language configuration for `.dafuqmeta` files.

For example, a project may contain:

```text
.vscode/
└── settings.json
```

The VS Code configuration can associate `.dafuqmeta` files with a custom language definition.

Syntax highlighting, autocomplete, formatting, and validation depend on the language configuration or extension used by the project.

---

# 32. Design Philosophy

DAFUQMETA is designed to be:

* **Human-readable**
* **Lightweight**
* **Easy to edit**
* **Suitable for metadata**
* **Suitable for configuration**
* **Flexible**
* **Nestable**
* **Readable without specialized tools**

The format allows simple metadata:

```dafuqmeta
Name: "Example";
Version: "1.0";
```

as well as more complex structures:

```dafuqmeta
Application: {
    Name: "Example";
    Settings: {
        Enabled: True;
    };
};
```

and longer human-readable content:

```dafuqmeta
Description: [
    This is an example.
    Additional information can be written here.
];
```

The goal is to provide a practical format for storing structured metadata while keeping the syntax easy to understand and manually edit.

---

# 33. Syntax Summary

A DAFUQMETA document generally follows this pattern:

```text
_FILE_START_

container

_FILE_END_
```

Inside the container, properties use:

```text
Key: Value;
```

Values can include basic literals such as:

```text
"string"
123
True
False
```

as well as structured values:

```text
[]
{}
()
```

These structures can be nested to represent more complex metadata.

DAFUQMETA is intentionally designed around a simple syntax so that metadata remains readable both as raw text and when processed by software.
