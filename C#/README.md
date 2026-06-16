# C# Conventions
<img src="https://raw.githubusercontent.com/vscode-icons/vscode-icons/refs/heads/master/icons/file_type_csharp.svg" alt="C#" align=right width="80" />

List of C# conventions used at OceanApocalypseStudios. These conventions are an adaptation of [Microsoft's own coding conventions for .NET](https://learn.microsoft.com/en-us/dotnet/standard/design-guidelines/).

> Made by MF366.

----

# .editorconfig _(to be updated)_
In this very same directory, you'll find a ready-for-use `.editorconfig` file. Keep in mind it only contains the strict rules, not the recommendations.

----

# Naming
> _Following a consistent set of naming conventions in developing a framework can be a major contribution to the framework’s usability. It allows the framework to be used by many developers on widely separated projects. Beyond consistency of form, the names of framework elements must be easily understood and convey each element's function._
> 
> \- Microsoft

## Capitalization
When writing C#, we only apply [**PascalCase**](https://wiki.c2.com/?PascalCase) and [**camelCase**](https://en.wikipedia.org/wiki/Camel_case). Previously, we applied [**CONSTANT_CASE**](https://stringcase.org/cases/constant/) for private constants, but we no longer do so, and are renaming type members that previously followed this capitalization.

### When to apply each capitalization
* **DO** use PascalCase for namespaces, types and the following members: methods, properties, types, events and enum values.
* **DO** use camelCase for parameters, variables and non-constant fields.

* **NEVER** prefix names with non-alphanumeric characters (this includes common patterns like `_privateField` that are strictly forbidden by this guideline), **UNLESS** the names are for a testing method
* **DO** use the `ShortClassName_Method_TestSubject` rule for naming test methods (e.g.: `Service_Save_ThrowsWhenNull`, `Terminal_ToggleInvisibleText_PrintsStringsStill` or `Cache_Init_ThrowsOnSizeExceeded`).

### Case-sensitivity
> [!NOTE]
> This only applies if your code is supposed to be executed from other .NET languages that are not C#.

Even though C# is a case-sensitive language, other .NET languages, such as Visual Basic (VB.NET), are case-insensitive, meaning names **SHOULD NOT** differ only by case on shared assemblies.

> E.g.: `currentFile` and `CurrentFile` differ only by case, meaning they are not good choices for names on shared assemblies; better choices would be `currentFile` and `OpenedFile` or `curFile` and `CurrentFile`.

### Compound words and Common terms
Same as [Microsoft's guideline](https://learn.microsoft.com/en-us/dotnet/standard/design-guidelines/capitalization-conventions#capitalizing-compound-words-and-common-terms), with the following addition:
* **DO** use words such as `If`, `When` and `On` when naming occurences that should be triggered by a given element (e.g.: `ThrowIfNull`, `StopWhenSizeLimitReached`, `CloseOnSave`). Additionally, the `On` pattern should be a programmer's best friend when naming events (e.g.: `OnClick`, `OnSave`, `OnEdit`, `OnSizeChanged`, `OnColorChanged`, etc).
* When using a name that refers to C#, **DO** write it as `CSharp` or `cSharp` (whether it's PascalCase or camelCase) **UNLESS** it's in comments (where you should always prefer `C#`) or strings.

### Word Choice
* **DO** favor readability, even if it leads to longer names. E.g.: choose `SecondaryViewport` over `ViewportSecondary` and `SecVPort`.
* **DO NOT** apply Hungarian notation (`iCount`, `szName` and `fnMyFunction` are all examples of forbidden names).
* **AVOID** using identifiers that conflict with C#'s keywords and reserved names. If it's of utmost necessity, you may use those identifiers, as long as you use the `@` escape character.

### Abbreviations and Acronyms
* **KEEP** abbreviations, contractions and acronyms to a minimum. E.g.: order of preference should be `CloseMainWindow` > `CloseMainWin` > `CloseMW`.
* **AVOID** acronyms that are niche or not widely accepted.

### Prefixes and Suffixes
> [!NOTE]
> This does not apply to unit tests.

* **DO** use the `Async` suffix if it's necessary to distinguish from non-async methods. E.g.: inside a class that has a `Save` method, it might be a good idea to name the async version of that method `SaveAsync`.
* When dealing with async-heavy context (e.g.: almost every method is async), the rule above **SHOULD** be broken, for the sake of readability.
* **DO NOT** use the `Ex` suffix or similar suffixes to indicate components of previous API versions.
* **DO NOT** use your project's name as a prefix or suffix (e.g.: `MyAwesomeTextEditorSettingsService`). Instead, use namespaces.

### Namespaces
* **ALWAYS** respect file hierarchy when naming namespaces (e.g.: a file located in `src/MyProject/Services/Settings/JsonSettingsService.cs` that belongs to solution `MySolution` should **strictly** have namespace `MySolution.MyProject.Services.Settings`).

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
- No braces is prefered when possible.
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

- The use of auto properties is recommended.
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
Console.WriteLine("Hello, World!"); // what is this? PYTHON??!!
```

- Braces need to breathe.
```c#
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

// Exceptions to the rule:
try
{
	// no empty lines unless more than one line
}
catch (Exception)
{
	// same here
}
```

----

## Parentheses
- The use of redundant parentheses for the sake of clarity in arithmetic operators (`*`, `/`, `+`, `%`, `-`, `<<`, `>>`, `&`, `^`, `|`), binary operators (`&&`, `||`, `??`, `or`, `and`), relational operators (`<`, `>`, `==`, `!=`, `<=`, `>=`, `is`, `as`) and others is indifferent.

----

## Expressions
- The use of object initializers is recommended.
```c#
// This:
Customer c = new()
{

	Age = 21

};

// Or this:
Customer c = new();
c.Age = 21;
```

- Prefer collection initializers.
```c#
// Prefer:
List<int> list = new() { 1, 2, 3 };
// and
List<int> list = [1, 2, 3]; // is this Python now?!

// Over:
List<int> list = new();
list.Add(1);
list.Add(2);
list.Add(3);
```

- Prefer simplified boolean expressions.
```c#
// Prefer:
var x = A() && B();

// Over:
var x = A() && B() ? true : false;
```

- Prefer `switch` expression.
```c#
// Prefer:
return num switch
{

	1 => 1,
	_ => 2

}

// Over:
switch (num)
{

	case 1:
		return 1;
		
	default:
		return 2;

}
```

- Prefer ternary operator over `if` with assignments.
```c#
// Prefer:
string s = v ? "hello" : "world";

// Over:
string s;

if (v)
	s = "hello";
	
else
	s = "world";
```

- Prefer ternary operator over `if` with returns.
```c#
// Prefer:
return v ? "hello" : "world";

// Over:
if (v)
	return "hello";
	
return "world";
```

- Prefer explicit tuple name.
```c#
// Prefer:
(string Name, int Age) customer = GetCustomer();
var name = customer.Name;
var age = customer.Age;

// Over:
(string Name, int Age) customer = GetCustomer();
var name = customer.Item1;
var age = customer.Item2;
```

- Prefer simple `default` expression.
```c#
// Prefer:
void F(CancellationToken cancellationToken = default) { }

// Over:
void F(CancellationToken cancellationToken = default(CancellationToken)) { }
```

- Prefer infered tuple element names.
```c#
// Prefer:
var tuple = (age, name);

// Over:
var tuple = (age: age, name: name);
```

- Prefer inferred anonymous type member names.
```c#
// Prefer:
var anon = new { age, name };

// Over:
var anon = new { age = age, name = name };
```

- Prefer local _(inner)_ function over anonymous function.
```c#
// Prefer:
int RecursiveFibonacci(int n) => n <= 1 ? n : fibonacci(n - 1) + fibonacci(n - 2);

var result = RecursiveFibonacci(num);

// Over:
Func<int, int>? fibonacci = null;
fibonacci = (int n) => n <= 1 ? n : fibonacci(n - 1) + fibonacci(n - 2);

var result = fibonacci?.Invoke(num);
```

- Prefer compound assignments.
```c#
// Prefer:
value += 10;

// Over:
value = value + 10;
```

- **ALWAYS** prefer implicit object creation when type is apparent.
```c#
// Prefer:
private readonly List<Order> orders = new();

// Over:
private readonly List<Order> orders = new List<Order>(); // unnecessary repetition
```

- Prefer index operator.
```c#
// Prefer:
var ch = value[^1];

// Over:
var ch = value[value.Length - 1];
```

- Prefer range operator.
```c#
// Prefer:
var sub = value[1..^1]; // literal life saver

// Over:
var sub = value.Substring(1, value.Length - 2);
```

- Prefer tuple swap.
```c#
// Prefer:
(args[1], args[0]) = (args[0], args[1]);

// Over:
var temp = args[0];
args[0] = args[1];
args[1] = temp;
```

- Use expression body for methods, local functions, properties, lambdas, operators and indexers when possible.
```c#
class Customer
{

	private int Age;
	
	// Single line - Expression Body
	public int GetAge() => Age;
	
	// Multiple lines
	public int F()
	{
	
		Console.WriteLine($"I'm {Age} years old.");
		return GetAge();
	
	}

}
```

- Use expression body for accessors when possible.
```c#
class Customer
{

	private int age;
	
	// Expression body is possible
	public int Age
	{
	
		get => age;
		set => age = value;
	
	}

}
```

- Use expression body for constructors when on single line.
```c#
class Customer
{

	private int Age;
	
	// Single line - does not matter
	public Customer(int age)
	{
	
		Age = age;
	
	}

}
```

- Explicitly discard unused value assignments and statements that implicitly ignore value, whenever possible.
```c#
// Prefer:
_ = Computation; // value is discarded
int x = 1;

// Over:
int x = Computation(); // value is never used
x = 1;
```

----

## TODO
- [ ] Add more coding conventions
