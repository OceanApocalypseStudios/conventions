# C# Conventions
<img src="https://raw.githubusercontent.com/vscode-icons/vscode-icons/refs/heads/master/icons/file_type_csharp.svg" alt="C#" align=right width="80" />

List of C# conventions used at OceanApocalypseStudios.

> Made by MF366.

----

## Naming
| Element                          | Naming Convention                                                                | Example
| -------------------------------- | -------------------------------------------------------------------------------- | -------
| Interfaces                       | PascalCase With `I` prefix                                                       | `interface IMyInterface { }`
| Classes                          | [PascalCase](https://wiki.c2.com/?PascalCase)                                    | `class MyClass { }`
| Structs                          | PascalCase                                                                       | `struct MyStruct { }`
| Enums                            | PascalCase                                                                       | `enum MyEnum { }`
| Async Methods                    | PascalCase With `Async` suffix (suffix not mandatory on async-heavy logic)       | `async Task MyMethodAsync { }`
| Methods, Events and Delegates    | PascalCase                                                                       | `void HelloWorld() { }`
| Properties                       | PascalCase                                                                       | `string MyProperty { get; set; }`
| Type parameters / Generics       | PascalCase With `T` prefix (or just `T`)                                         | `void MyMethod<TMyParam>() { }`
| Constants                        | [CONSTANT_CASE](https://stringcase.org/cases/constant/)                          | `const int MY_CONSTANT = 1;`
| Fields, Variables and Parameters | [camelCase](https://en.wikipedia.org/wiki/Camel_case)                            | `int myInteger;`
| Namespaces                       | PascalCase (never file-scoped, always block-scoped)                              | `namespace MyProject.MyNamespace { }`
| Attributes (inheriting from one) | PascalCase With Optional `Attribute` suffix                                      | `class MyAttribute : Attribute`
| Filenames (optional)             | PascalCase (if C#, asset or configuration file)                                  | `MyAwesomeFile.cs` or `MyImage.png` or `MyConfig.json` or `not_a_csharp_file.py`

----

## `this.`
- Do **not** qualify ANY type of access (properties, fields, methods, etc) with `this` (`capacity` instead of `this.capacity`)

----

## Predefined types
- Prefer predefined type (`int`, `string` instead of `System.Int32`, `System.String`) for locals, parameters and members
```c#
int capacity = 0; // instead of Int32
string data = "Hello"; // instead of String
```

- Prefer framework type (`System.Int32`, `System.String` instead of `int`, `string`) for member access expressions
```c#
var value = Int32.MaxValue; // instead of int.MaxValue
var emptyString = String.Empty; // instead of string.Empty
```

----

## `var`
- Indifferent, although `var` is prefered when the type is apparent.
- Prefer using `<type> someVar = new()` instead of `var someVar = new <type>()`
```c#
// Prefer:
XDocument doc = new();

// Over:
var doc = new XDocument();
```

----

## TODO
- [ ] Add more coding conventions
