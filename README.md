# Typr
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
Typr statically scripting language 
## Content
* [Oveerview](-Overview)
* [Installation](Installation)
* [Features](Features)
* [Syntax Guide](Syntax-Guide)
* [Report Issues](Report-Issues)

### Overview
Typr is a modern, statically typed scripting language featuring robust type inference, Object-Oriented Programming (OOP) capabilities, exception handling, and modular imports. It combines the safety of static typing with the ease of use of a scripting language.

### Installation
We automate native, standalone builds for macOS, Linux, and Windows using GitHub Actions and PyInstaller.
- Download file from release by github action
- Make file executable `chmod +x [file_name]` that download
- To execute `./typr [file.typr]`
-----------------------------------------------------------------------------------------------------------------------
To build a standalone executable locally, run PyInstaller:
```bash
pip install -r requirements.txt
pyinstaller exec.spec --clean
```
The compiled executable will be placed in `dist/typr`.

>[!Important]
>If you use macOS run this command before execute `xattr com.apple.quarantine [file_name]`

### Features 
* **Static Type System** Typr support static type system and type inference
* **Functions & Lambdas** Typr Fully support closure anonymous function with function and explicit return type
* **Object Oriented Programming** Typr support class constructor method and inheritance using `extend` `parent` and `this` keywords
* **Standard Module** Typr have growing standard module `std_math.typr` | `std_array.typr` | `std_request`
* **Error Handling** Typr support error handling and exception with keywords `try`, `expect error`, `final`
* **Modular Import** Typr support modular import so you can create your own module and import with keyword `source`, `as`
* **Multi platform** Typr support in macOS, Window and Linux

### Syntax Guide 
- Variable and Constant : Variable and constant are declared using the `init` or `let` and `const` keywords
  - `init` keyword is used to declare and initialized a variable
  - `let` keyword is used to declare a variable or expression
  - `const` keyword is used to declare a constant variable (constant variable name use UPPERCASE)
>[!Note]
>`Semicolon;` is an `optional` at the end of all statement
```Example
init int:x = 5        >>>>> declared and initailized a variable x type intwith value 5
let int:x             >>>>> declared a variable x type int
const float:PI = 3.14 >>>>> declared a constant variable PI type float with value 3.14
*** Also you can declare with type inference *** 
let x = 5             >>>>> declared a variable x with value 5 >> will infer type int
let greeting = "Hello">>>>> declared a variable greeting with value "Hello" >> will infer type str
```
- Control Flow and Loop : Typr supports control flow and loop statements `if` , `else`, `for` and `while` keywords
  - `if` keyword followed by a condition and a block of code to be executed if the condition is `true`
  - `else` keyword followed by a block of code to be executed if `if` condition is `false`
  - `for` keyword followed by a initialize variable and increment expression or condition or iteration and a block of code to be
    executed for each iteration or condition
  - `while` keyword followed by a condition and block of code to be executed while the condition is `true` can cause infinite loop

```Example
>>>>> If Else if condition is true then execute if block else execute else block
let int:x = 0
if x > 0 {
    disp(x);
} else {
    x = x+1;
    disp(x);
}
>>>>> For loop will display 0 to 9 on the console
for (init int:i = 0; i<10l i++){
    disp(i);
}

>>>>> While loop check if condition is true execute block until false can cause infinite loop
while (x<10) {
    disp(x);
    x = x+1;
}
```
> [!IMPORTANT]
> Use `cont` instead of `continue` in loops. The `break` keyword behaves normally.

- Function and Lambda Functions : Typr supports function and lambda function with explicit return with return type check 
    - `fnc` Function keyword followed by a colon type of return and function name then followed by parameters and a block of code to be executed 
    - `fnc?` Lamda function keyworf followed by a colon type of parameters and block of code
```Example
>>>>> Declare a function parameter and return 
        - fnc sum return type int 
        - parameter int:a and int:b
fnc  sum:int(int:a, int:b) {
    return a + b;
}

>>>>> Declare a lambda function
        - fnc? anonymous 
        - parameter int:y
fnc? int:y -> y = y + 1;

>>>>> Declare default parameter value
        - fnc sum return type int
        - parameter int a and int b
        - default value of b = 10 (if u not specified value of b when call function b will be 10)

fnc sum:int(int:a, int:b=10) {
    return a + b
}
```
>[!Note]
>To call function `function_name(parameters)`

- Class and Inheritance : Typr support class and inheritance system define fields, constructors and extend from parent class
    - `extend` Keyword followed by parent class name to inherit fnc and properties from parent to child class
    - `parent` keyword followed by parent method name to call method from parent class
```Example
>>>>> Define parent class then use extend keyword to use fnc of parent class in child class
class Animal{
    init str: name

    fnc Animal(name:str){
        this.name = name
    }
    
    fnc speak(){
        disp(this.name + " is speaking")
    }
}

class Dog extend Animal{
    fnc Dog(name:str) {
        parent.Animal(name)    
    }

    fnc speak() {
        disp(this.name + " is barking")
    }

}
let pet = Dog("Buddy")
pet.speak() >> "Buddy is speaking"
```
- Exception Handling : Typr support try, expect and finally to handle exceptions and debug program
    - `try` keyword followed by a block of code to be try to execute
    - `expect` keyword followed by an exception type and a block of code that will execute when error or exception is thrown
    - `finally` keyword followed by block of code that will always execute either when error or exception is thrown or not
```Example
try {
    let result = 10 / 0
} expect error {
    disp("Error caught: " + error)
} final { 
    disp("Execution Completed")
}
```
## Standard Library Modules

Typr includes a growing collection of core modules. They are imported via the `source` keyword.

### `std_math.typr`
Includes algebraic operations, range conversions, trigonometry, and statistical utilities.

| Function | Signature | Detail |
| :--- | :--- | :--- |
| `area` | `area(radius: float) -> float` | Returns the area of a circle. |
| `deg_to_rad` | `deg_to_rad(deg: float) -> float` | Converts degrees to radians. |
| `rad_to_deg` | `rad_to_deg(rad: float) -> float` | Converts radians to degrees. |
| `hypot` | `hypot(a: float, b: float) -> float` | Calculates the hypotenuse $\sqrt{a^2 + b^2}$. |
| `factorial` | `factorial(n: int) -> int` | Computes the factorial of a positive integer. |
| `gcd` | `gcd(a: int, b: int) -> int` | Computes the Greatest Common Divisor. |
| `sin` | `sin(x: float) -> float` | Standard sine trigonometric approximation. |
| `cos` | `cos(x: float) -> float` | Standard cosine trigonometric approximation. |
| `tan` | `tan(x: float) -> float` | Standard tangent trigonometric approximation. |
| `fibonacci` | `fibonacci(n: int) -> int` | Computes the Fibonacci sequence. |
| `exp` | `exp(x: float) -> float` | Exponential function $e^x$. |
| `ln` | `ln(x: float) -> float` | Natural logarithm $\ln(x)$. |
| `log` | `log(x: float, base: float) -> float` | Logarithm with arbitrary base. |
| `sinh` / `cosh` / `tanh` | `sinh(x: float) -> float` | Hyperbolic trig functions. |
| `lcm` | `lcm(a: int, b: int) -> int` | Least Common Multiple. |
| `is_prime` | `is_prime(n: int) -> bool` | Primality check. |
| `mean` | `mean(array) -> float` | Arithmetic mean of an array. |

```Example
source "std_math.typr" as math

let x = math.fibonacci(3) // 2
let y = math.factorial(3) // 6
let z = math.area(4.0) // 50.26544
```

### `std_array.typr`
Generic utility module for manipulating list-like collections.
|Function     | Signature      | Detail |
| :--------   |:---------------|:-------|
|`contains` | `contains(array, target) -> bool`| Searches for `target` in the `array`.|
|`find_index`| `find_index(array, target) -> int`| Returns the zero-based index of `target` or `-1` if not found.|
|`sum`       | `sum(array) -> float`| Returns the mathematical sum of all numeric array elements.|
|`reverse`   | `reverse(array) -> arr`| Returns a reversed copy of the array.|
|`map_arr`   | `map_arr(array, fn) -> arr`| Maps a function over each element of the array.|
|`filter`    | `filter(array, fn) -> arr`| Filters elements matching the predicate function.|
|`reduce`    | `reduce(array, fn, initial) -> int`| Reducer function.|
|`minimum`   | `minimum(array) -> int`| Returns the minimum value in the array.|
|`maximum`   | `maximum(array) -> int`| Returns the maximum value in the array.|

```Example
source "std_array.typr" as array_util

let numbers = [1, 2, 3, 4, 5]
let found = array_util.contains(numbers, 3) // true
let index = array_util.find_index(numbers, 4) // 3
```
### `std_request` 
Generic Uitility for http post, get, put and delete

|Function     |Signature         | Detail   |
|:------------|:------------------|:--------|
| `post`      | post [str, map, map] | Request post with url, headers, params|
| `get`       | get [str, map, map] | Request get with url, headers, params|
| `put`       | put [str, str, map, map] | Request put |
| `delete`    | delete [str, map, map] | Requst delete |

```Example
source "std_request" as http
try {
  init map[str, str]: headers = ("Authoriazation" : "Bearer 123")
  init map[str, str]: params = ("q" : "test")
  let res = http.get("http://invalid-domain-xxxx.com", params, headers)
} expect error {
  disp("Caught Network Error:" + error) 
}
```
>[!Note]
> This module use `source std_request as ...` <br>
---

### Report Issues 
report issues parsing or syntax error 
[report](https://github.com/Bennnto/Typr/issues/new)
