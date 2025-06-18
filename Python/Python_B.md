# Python Conventions (Version B)
<img src="https://raw.githubusercontent.com/vscode-icons/vscode-icons/refs/heads/master/icons/file_type_python.svg" alt="Python 3" align=right width="80" />

List of Python conventions used at OceanApocalypseStudios.

> Made by MF366.

----

## Naming
| Element                          | Naming Convention                                                                | Example
| -------------------------------- | -------------------------------------------------------------------------------- | -------
| Classes                          | [PascalCase](https://wiki.c2.com/?PascalCase)                                    | `class MyClass:`
| Async Methods                    | [snake_case](https://stringcase.org/cases/snake/) With optional `async` suffix       | `async def my_method_async():`
| Methods and Functions   | snake_case                                                                    | `def hello_world():`
| Properties                       | [**camelCase**](https://en.wikipedia.org/wiki/Camel_case) or **snake_case**                                                                      | `@property` ... `def myProperty():`
| Constants                        | [CONSTANT_CASE](https://stringcase.org/cases/constant/)                          | `MY_CONSTANT = 1`
| Fields, Variables and Parameters | snake_case                            | `my_var = 5`
| Filenames (optional)             | snake_case (if Python, asset or configuration file)                                  | `my_file.py` or `img.png` or `my_config.json` or `notPython.cs`

----

## TODO
- [ ] Add more coding conventions