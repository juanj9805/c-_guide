# C# Fundamentals Guide: From JavaScript to C#

## Table of Contents
1. [Language Overview](#language-overview)
2. [Type System](#type-system)
3. [Variables and Constants](#variables-and-constants)
4. [Data Types](#data-types)
5. [Operators](#operators)
6. [Control Flow](#control-flow)
7. [Functions and Methods](#functions-and-methods)
8. [Object-Oriented Programming](#object-oriented-programming)
9. [Collections](#collections)
10. [Key Differences: JavaScript vs C#](#key-differences-javascript-vs-c)
11. [Common Gotchas](#common-gotchas)

---

## Language Overview

### What is C#?
C# is a modern, object-oriented, and type-safe programming language developed by Microsoft. It runs on the .NET framework and is designed to be simple, powerful, and type-safe.

**Key Characteristics:**
- **Strongly-typed**: Variables must have a declared type
- **Compiled**: Code is compiled to intermediate language (IL) before execution
- **Object-oriented**: Everything is an object
- **Garbage collected**: Automatic memory management
- **Modern**: Includes features like async/await, LINQ, null-conditional operators

### Where JavaScript is Dynamic, C# is Static
```javascript
// JavaScript - Dynamic typing
let x = 5;
x = "hello"; // This works fine
```

```csharp
// C# - Static typing
int x = 5;
x = "hello"; // Compilation error!
```

---

## Type System

### Explicit Type Declaration
C# requires you to declare the type of every variable, property, and parameter.

```csharp
// Basic syntax
string name = "John";
int age = 30;
double salary = 50000.50;
bool isActive = true;
```

### Type Inference with `var`
C# has type inference using the `var` keyword (similar to JavaScript's `let`/`const`, but still strongly-typed):

```csharp
var name = "John";      // Inferred as string
var age = 30;           // Inferred as int
var items = new List<string>(); // Inferred as List<string>

// The type is fixed at compile time!
// This would cause a compile error:
// name = 123; // Error: cannot convert int to string
```

---

## Variables and Constants

### Variable Declaration

```csharp
// Local variable
int count = 10;

// Multiple declarations
int x = 1, y = 2, z = 3;

// With var keyword
var message = "Hello";

// Nullable types (can be null)
string? nullable_string = null; // The ? means it can be null
int? nullable_int = null;
```

### Constants

```csharp
// Compile-time constant
const int MAX_USERS = 100;

// Runtime constant (cannot be changed after assignment)
readonly string DatabaseUrl = "connection_string";

// Class-level constant
public const double PI = 3.14159;
```

**Key Difference from JavaScript:**
- JavaScript has `const`, but it only prevents reassignment. C# constants are truly immutable.

---

## Data Types

### Primitive Types

```csharp
// Numeric types
int number = 42;              // 32-bit integer
long bigNumber = 9999999999;  // 64-bit integer
float price = 19.99f;         // 32-bit floating point (needs 'f' suffix)
double salary = 50000.50;     // 64-bit floating point
decimal money = 99.99m;       // High precision (for money)
byte smallNum = 255;          // 8-bit unsigned

// Boolean
bool isActive = true;

// Character
char letter = 'A';

// String
string name = "John Doe";
```

### Reference Types

```csharp
// String (reference type, not primitive like in some languages)
string text = "Hello";

// Object (base type for all classes)
object obj = "anything";

// Array (fixed size)
int[] numbers = new int[5];
int[] scores = { 10, 20, 30 };

// List (dynamic size, from System.Collections.Generic)
using System.Collections.Generic;
List<int> list = new List<int> { 1, 2, 3 };

// Dictionary
Dictionary<string, int> ages = new Dictionary<string, int>
{
    { "John", 30 },
    { "Jane", 28 }
};
```

### Nullable Types

```csharp
// C# 8.0+ nullable reference types
string? nullableString = null;
int? nullableInt = null;

// Null-coalescing operator
string name = nullableString ?? "Unknown"; // "Unknown" if null
```

---

## Operators

### Arithmetic Operators
```csharp
int a = 10, b = 3;
int sum = a + b;      // 13
int diff = a - b;     // 7
int product = a * b;  // 30
int quotient = a / b; // 3 (integer division)
int remainder = a % b; // 1
```

### Comparison Operators
```csharp
5 == 5    // true
5 != 3    // true
5 > 3     // true
5 >= 5    // true
```

### Logical Operators
```csharp
bool x = true && false;  // false (AND)
bool y = true || false;  // true (OR)
bool z = !true;          // false (NOT)
```

### Null-Conditional & Null-Coalescing
```csharp
string? text = null;

// Null-conditional operator (?.)
string? result = text?.ToUpper();  // Returns null instead of throwing error

// Null-coalescing operator (??)
string name = nullValue ?? "Default";

// Null-coalescing assignment (??=)
string? value = null;
value ??= "Default";  // value is now "Default"
```

---

## Control Flow

### If-Else Statements
```csharp
int age = 20;

if (age < 13)
{
    Console.WriteLine("Child");
}
else if (age < 18)
{
    Console.WriteLine("Teenager");
}
else
{
    Console.WriteLine("Adult");
}

// Ternary operator (same as JavaScript)
string category = age >= 18 ? "Adult" : "Minor";
```

### Switch Statements
```csharp
int day = 3;

switch (day)
{
    case 1:
        Console.WriteLine("Monday");
        break;
    case 2:
        Console.WriteLine("Tuesday");
        break;
    default:
        Console.WriteLine("Other day");
        break;
}

// Modern switch expression (C# 8.0+)
string dayName = day switch
{
    1 => "Monday",
    2 => "Tuesday",
    3 => "Wednesday",
    _ => "Other"
};
```

### Loops

```csharp
// For loop
for (int i = 0; i < 5; i++)
{
    Console.WriteLine(i);
}

// While loop
int count = 0;
while (count < 5)
{
    Console.WriteLine(count);
    count++;
}

// Do-while loop
do
{
    Console.WriteLine(count);
} while (count < 5);

// Foreach loop
int[] numbers = { 1, 2, 3, 4, 5 };
foreach (int num in numbers)
{
    Console.WriteLine(num);
}

// Foreach with string interpolation
foreach (var item in items)
{
    Console.WriteLine($"Item: {item}");
}
```

---

## Functions and Methods

### Basic Method Definition

```csharp
// Return type, method name, parameters
public string Greet(string name)
{
    return $"Hello, {name}!";
}

// No return value (void)
public void PrintMessage(string message)
{
    Console.WriteLine(message);
}

// Multiple parameters
public int Add(int a, int b)
{
    return a + b;
}

// Default parameters
public void Log(string message, LogLevel level = LogLevel.Info)
{
    // implementation
}

// Out parameters (returns multiple values)
public bool TryParse(string input, out int result)
{
    return int.TryParse(input, out result);
}

// Usage
if (TryParse("123", out int number))
{
    Console.WriteLine(number);
}
```

### Named and Optional Parameters

```csharp
public void Order(string item, int quantity = 1, string size = "Medium")
{
    Console.WriteLine($"{quantity} {size} {item}(s)");
}

// Usage
Order("Coffee");                                    // Uses defaults
Order("Coffee", 2);                                 // quantity = 2
Order("Coffee", size: "Large");                     // Named parameter
Order(item: "Coffee", quantity: 3, size: "Large"); // All named
```

### Method Overloading

```csharp
// Same method name, different parameters
public void Print(int value)
{
    Console.WriteLine("Int: " + value);
}

public void Print(string value)
{
    Console.WriteLine("String: " + value);
}

public void Print(double value)
{
    Console.WriteLine("Double: " + value);
}

// C# determines which to call based on argument types
Print(42);         // Calls Print(int)
Print("hello");    // Calls Print(string)
Print(3.14);       // Calls Print(double)
```

---

## Object-Oriented Programming

### Classes

```csharp
public class Person
{
    // Fields (private by default)
    private string _name;
    private int _age;

    // Properties (auto-implemented)
    public string Name { get; set; }
    public int Age { get; set; }

    // Property with custom getter/setter
    public string Email
    {
        get { return _email; }
        set { _email = value; }
    }

    // Constructor
    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }

    // Method
    public void Introduce()
    {
        Console.WriteLine($"Hi, I'm {Name} and I'm {Age} years old");
    }

    // Static method
    public static void CreateDefault()
    {
        return new Person("John", 30);
    }
}

// Usage
var person = new Person("Alice", 25);
person.Introduce();
```

### Properties

```csharp
public class User
{
    // Auto-property (getter and setter generated automatically)
    public string Username { get; set; }

    // Property with logic
    private int _age;
    public int Age
    {
        get { return _age; }
        set
        {
            if (value >= 0)
                _age = value;
        }
    }

    // Read-only property
    public string UserId { get; private set; }

    // Expression-bodied property (C# 6.0+)
    public string FullInfo => $"{Username} (Age: {Age})";

    public User(string username)
    {
        Username = username;
        UserId = Guid.NewGuid().ToString();
    }
}
```

### Inheritance

```csharp
public class Animal
{
    public string Name { get; set; }

    public virtual void MakeSound()
    {
        Console.WriteLine("Some generic animal sound");
    }
}

public class Dog : Animal
{
    // Override parent method
    public override void MakeSound()
    {
        Console.WriteLine("Woof!");
    }

    public void Fetch()
    {
        Console.WriteLine("Fetching the ball");
    }
}

// Usage
Animal dog = new Dog { Name = "Buddy" };
dog.MakeSound(); // Outputs: Woof!
```

### Interfaces

```csharp
public interface ILogger
{
    void Log(string message);
    void Error(string message);
}

public class ConsoleLogger : ILogger
{
    public void Log(string message)
    {
        Console.WriteLine(message);
    }

    public void Error(string message)
    {
        Console.ForegroundColor = ConsoleColor.Red;
        Console.WriteLine(message);
        Console.ResetColor();
    }
}

// Usage
ILogger logger = new ConsoleLogger();
logger.Log("Application started");
```

### Abstract Classes

```csharp
public abstract class Shape
{
    public abstract double GetArea();

    public void Display()
    {
        Console.WriteLine($"Area: {GetArea()}");
    }
}

public class Circle : Shape
{
    private double _radius;

    public Circle(double radius)
    {
        _radius = radius;
    }

    public override double GetArea()
    {
        return Math.PI * _radius * _radius;
    }
}
```

---

## Collections

### Arrays

```csharp
// Fixed-size collection
int[] numbers = new int[5];
int[] scores = { 10, 20, 30, 40, 50 };

// Multi-dimensional
int[,] matrix = new int[3, 3];
int[][] jagged = new int[3][]; // Jagged array

// Access elements
int first = scores[0];
scores[1] = 25;
```

### List<T> (Generic List)

```csharp
using System.Collections.Generic;

List<int> numbers = new List<int> { 1, 2, 3 };
numbers.Add(4);
numbers.Remove(2);
numbers.Insert(0, 0);

// Iteration
foreach (int num in numbers)
{
    Console.WriteLine(num);
}

// LINQ
var evenNumbers = numbers.Where(x => x % 2 == 0).ToList();
```

### Dictionary<K, V>

```csharp
Dictionary<string, int> ages = new Dictionary<string, int>
{
    { "Alice", 30 },
    { "Bob", 25 }
};

// Add/Access
ages["Charlie"] = 35;
int aliceAge = ages["Alice"];

// Check if key exists
if (ages.ContainsKey("Alice"))
{
    Console.WriteLine(ages["Alice"]);
}

// Iterate
foreach (var kvp in ages)
{
    Console.WriteLine($"{kvp.Key}: {kvp.Value}");
}
```

### Useful LINQ Methods

```csharp
using System.Linq;

List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

// Filter
var even = numbers.Where(x => x % 2 == 0);

// Transform
var doubled = numbers.Select(x => x * 2);

// Aggregate
int sum = numbers.Sum();
int max = numbers.Max();
int min = numbers.Min();
int count = numbers.Count();

// Sort
var sorted = numbers.OrderBy(x => x);
var descending = numbers.OrderByDescending(x => x);

// Check conditions
bool hasEven = numbers.Any(x => x % 2 == 0);
bool allPositive = numbers.All(x => x > 0);
```

---

## Key Differences: JavaScript vs C#

| Feature | JavaScript | C# |
|---------|-----------|-----|
| **Type System** | Dynamic (weakly typed) | Static (strongly typed) |
| **Compilation** | Interpreted | Compiled to IL |
| **Class Syntax** | ES6 classes or prototypes | Full class syntax |
| **Access Modifiers** | Not enforced | public, private, protected |
| **Method Overloading** | Not supported | Supported |
| **Inheritance** | Prototype-based | Class-based |
| **Interfaces** | Not built-in | Full interface support |
| **Generics** | Not native | Full generic support |
| **Async/Await** | Callbacks/Promises/async-await | async/await (similar) |
| **Null Handling** | undefined/null | null, nullable reference types |
| **Function Syntax** | `function` or `=>` | `public/private` + type syntax |
| **Package Management** | npm | NuGet |
| **Module System** | ES modules | Namespaces |

### Side-by-Side Comparison

#### Variable Declaration
```javascript
// JavaScript
let name = "John";
const age = 30;
var email = "john@example.com";
```

```csharp
// C#
string name = "John";
int age = 30;
string email = "john@example.com";
```

#### Function Definition
```javascript
// JavaScript
function add(a, b) {
    return a + b;
}

const multiply = (a, b) => a * b;
```

```csharp
// C#
public int Add(int a, int b)
{
    return a + b;
}

public int Multiply(int a, int b) => a * b;
```

#### Class Definition
```javascript
// JavaScript
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    greet() {
        return `Hello, I'm ${this.name}`;
    }
}
```

```csharp
// C#
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }

    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }

    public string Greet()
    {
        return $"Hello, I'm {Name}";
    }
}
```

#### Array/List Operations
```javascript
// JavaScript
const numbers = [1, 2, 3, 4, 5];
const even = numbers.filter(x => x % 2 === 0);
const doubled = numbers.map(x => x * 2);
```

```csharp
// C#
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };
var even = numbers.Where(x => x % 2 == 0);
var doubled = numbers.Select(x => x * 2);
```

#### Object Literals vs Objects
```javascript
// JavaScript - Object literal
const person = {
    name: "John",
    age: 30,
    greet: function() { return "Hi!"; }
};
```

```csharp
// C# - Instance of a class
var person = new Person { Name = "John", Age = 30 };
person.Greet();
```

---

## Common Gotchas

### 1. **Semicolons are Required**
```csharp
// This will cause a compile error
string name = "John"  // Missing semicolon!

// Correct
string name = "John";
```

### 2. **Case Sensitivity in Switch Statements**
```csharp
// Must include 'break' to prevent fall-through
switch (day)
{
    case 1:
        Console.WriteLine("Monday");
        break;  // Required!
    case 2:
        Console.WriteLine("Tuesday");
        break;
}
```

### 3. **String vs string**
```csharp
// string (lowercase) is an alias for System.String
string text = "hello";
String text2 = "hello";  // Both are the same

// Convention: use lowercase 'string'
```

### 4. **Reference Types vs Value Types**
```csharp
// Value type (copied)
int x = 5;
int y = x;
y = 10;
Console.WriteLine(x); // Still 5

// Reference type (reference copied)
List<int> list1 = new List<int> { 1, 2, 3 };
List<int> list2 = list1;
list2.Add(4);
Console.WriteLine(list1.Count); // 4 - both refer to same list!
```

### 5. **Equality Comparison**
```csharp
// For reference types, == checks reference equality
string a = new string(new[] { 'a' });
string b = new string(new[] { 'a' });
Console.WriteLine(a == b);        // true (string overrides ==)
Console.WriteLine(a.Equals(b));   // true

// For reference types without overridden ==
object obj1 = new object();
object obj2 = obj1;
Console.WriteLine(obj1 == obj2);  // true (same reference)
```

### 6. **Null Reference Exception**
```csharp
string? text = null;
// This will throw NullReferenceException
// int length = text.Length;

// Use null-conditional operator
int? length = text?.Length;  // null instead of exception
```

### 7. **Using Statements (Disposing Resources)**
```csharp
// Must dispose resources properly
using (FileStream fs = new FileStream("file.txt", FileMode.Open))
{
    // Use fs
} // fs is automatically disposed

// Modern using declaration (C# 8.0+)
using FileStream fs = new FileStream("file.txt", FileMode.Open);
// Use fs
// fs is automatically disposed at end of scope
```

### 8. **Compilation Required**
```csharp
// JavaScript - Type checking happens at runtime
let x = "hello";
x = 123;  // No error until runtime if you try to use it as string

// C# - Type checking happens at compile time
string x = "hello";
x = 123;  // Compile error immediately!
```

---

## Essential Tips for JavaScript Developers

1. **Expect Strict Typing**: Every variable must have a type. If you're unsure, use `var` and let C# infer it.

2. **Use Naming Conventions**:
   - Classes: `PascalCase` (e.g., `UserManager`)
   - Methods: `PascalCase` (e.g., `GetUserName`)
   - Properties: `PascalCase` (e.g., `FirstName`)
   - Variables: `camelCase` (e.g., `firstName`)
   - Constants: `UPPER_CASE` or `PascalCase`

3. **Understand Access Modifiers**: C# enforces encapsulation with `public`, `private`, `protected`.

4. **Use Properties Instead of Getters/Setters**: C# properties are more idiomatic than getter/setter methods.

5. **Leverage LINQ**: C# LINQ is extremely powerful for querying and transforming collections.

6. **Async/Await Works Similarly**: If you know JavaScript async/await, C# async/await will feel familiar.

7. **Read Error Messages**: C# compile-time errors will catch many bugs that JavaScript would only find at runtime.

---

## Quick Reference

### Common Classes and Methods
```csharp
// String methods
string text = "Hello World";
text.ToUpper();
text.ToLower();
text.Length;
text.Contains("World");
text.Replace("World", "C#");
text.Split(' ');

// Console output
Console.WriteLine("message");
Console.Write("no newline");
Console.ReadLine(); // Read user input

// Math
Math.Abs(-5);
Math.Round(3.14);
Math.Max(5, 10);
Math.Min(5, 10);
Math.Pow(2, 3); // 2^3

// DateTime
DateTime now = DateTime.Now;
DateTime date = new DateTime(2026, 3, 30);
TimeSpan duration = new TimeSpan(hours: 1, minutes: 30, seconds: 0);
```

---

## Next Steps

- Practice writing classes and methods
- Learn about namespaces and organizing code
- Explore async/await for asynchronous programming
- Study LINQ for data manipulation
- Learn about dependency injection
- Explore the .NET ecosystem and popular frameworks (ASP.NET Core, Entity Framework)

