# C# Conventions
<img src="https://raw.githubusercontent.com/vscode-icons/vscode-icons/refs/heads/master/icons/file_type_csharp.svg" alt="C#" align=right width="80" />

List of C# conventions used at OceanApocalypseStudios.

> Made by MF366.

----

## .editorconfig
In this very same directory, you'll find a ready-for-use `.editorconfig` file.

----

## Naming
| Element                          | Naming Convention                                                                | Example
| -------------------------------- | -------------------------------------------------------------------------------- | -------
| Interfaces                       | [PascalCase](https://wiki.c2.com/?PascalCase) With `I` prefix                    | `interface IMyInterface { }`
| Classes                          | PascalCase                                                                       | `class MyClass { }`
| Structs                          | PascalCase                                                                       | `struct MyStruct { }`
| Enums                            | PascalCase                                                                       | `enum MyEnum { }`
| Async Methods                    | PascalCase With `Async` suffix (suffix not mandatory on async-heavy logic)       | `async Task MyMethodAsync { }`
| Methods, Events and Delegates    | PascalCase                                                                       | `void HelloWorld() { }`
| Properties                       | PascalCase                                                                       | `string MyProperty { get; set; }`
| Type parameters / Generics       | PascalCase With `T` prefix (or just `T`)                                         | `void MyMethod<TMyParam>() { }`
| Constants                        | [CONSTANT_CASE](https://stringcase.org/cases/constant/)                          | `const int MY_CONSTANT = 1;`
| Fields, Variables and Parameters | [camelCase](https://en.wikipedia.org/wiki/Camel_case)                            | `int myInteger;`
| Namespaces                       | PascalCase                                                                       | `namespace MyProject.MyNamespace { }`
| Attributes (inheriting from one) | PascalCase With Optional `Attribute` suffix                                      | `class MyAttribute : Attribute`
| Filenames (optional)             | PascalCase (if C#, asset or configuration file)                                  | `MyAwesomeFile.cs` or `MyImage.png` or `MyConfig.json` or `not_a_csharp_file.py`

----

## `this.`
- Do **not** qualify ANY type of access (properties, fields, methods, events, etc) with `this`, unless absolutely necessary

```c#
// Prefer:
capacity = 1;
DoAction();

// Over:
this.capacity = 1;
this.DoAction();

// Does not apply when necessary:
internal class MyClass
{

    int val = 0;
    
    public MyClass(int val)
    {
    
        this.val = val;
        // necessary or else you'd be assigning local val to local val
    
    }
    
}    
```

----

## Predefined types
- Prefer predefined type (`int`, `string` instead of `System.Int32`, `System.String`) for locals, parameters and members
```c#
int capacity = 0; // instead of Int32
string data = "Hello"; // instead of String
```

- Prefer framework type (`System.Int32`, `System.String` instead of `int`, `string`) for member access expressions
```c#
using System;

var value = Int32.MaxValue; // instead of int.MaxValue
var emptyString = String.Empty; // instead of string.Empty
```

----

## `var`
- Indifferent, although explicit type is prefered over `var` when the type is apparent.
- Prefer using `<type> someVar = new()` instead of `var someVar = new <type>()`
```c#
// Prefer:
XDocument doc = new();

// Over:
var doc = new XDocument();
```

----

## Code Block
- Braces are prefered, but usually it's indifferent.
```c#
// Prefer:
if (val)
{

    Console.WriteLine("Hello, World!");
    
}

// Over:
if (val)
    Console.WriteLine("Hello, World!");
    
// but mostly indifferent
```

- Namespace declarations **ALWAYS** block-scoped, **NEVER** file-scoped.
```c#
// Prefer:
namespace A.B.C
{ ... }

// Over:
namespace A.B.C;
...
```

- The use of auto properties is indifferent.
```c#
public string MyProperty { get; set; }

public string myValue;
public string MyOther
{

    get => myValue;
    set => myValue = value;
    
}
```

- The use of "simple" `using` versus block `using` is indifferent.
```c#
using var foo = GetValue();
DoSomething(foo);

using (var foo = GetValue())
{ DoSomething(foo); }
```

- Prefer `System.HashCode` in `GetHashCode` if applicable
```c#
// Prefer (requires System.HashCode):
public override int GetHashCode() => System.HashCode.Combine(a, b, c);

// Over:
public override int GetHashCode()
{

    var hashCode = 339610899;
    var val = -1521134295;
    hashCode = hashCode * val + a.GetHashCode();
    hashCode = hashCode * val + b.GetHashCode();
    hashCode = hashCode * val + c.GetHashCode();
    return hashCode;
    
}
```

- Prefer method group conversion.
```c#
// Prefer:
Action<object> writeObject = Console.Write;

// Over:
Action<object> writeObject = obj => Console.Write(obj);
```

- Do **NOT** prefer top-level statements.
```c#
// Prefer:
using System;


internal class Program
{

    public static void Main(string[] args)
    {
    
        Console.WriteLine("Hello, World!");
        
    }
    
}

// Over:
using System;
Console.WriteLine("Hello, World!"); // what is this? PYTHON?!
```

- Braces need to breathe.
```
// Prefer 1 empty line after each brace:
public class A
{

    public int B()
    {
    
        return 0;
        
    }
    
}

// Over:
public class A
{
    public int B()
    {
        return 0;
    }
}
```

----

## Parentheses
- The use of redundant parentheses for the sake of clarity in arithmetic operators (`*`, `/`, `+`, `%`, `-`, `<<`, `>>`, `&`, `^`, `|`), binary operators (`&&`, `||`, `??`, `or`, `and`), relational operators (`<`, `>`, `==`, `!=`, `<=`, `>=`, `is`, `as`) and others is indifferent.

----

## TODO
- [ ] Add more coding conventions
