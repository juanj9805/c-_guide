# Guía de Fundamentos de C#: De JavaScript a C#

## Tabla de Contenidos
1. [Descripción General del Lenguaje](#descripción-general-del-lenguaje)
2. [Sistema de Tipos](#sistema-de-tipos)
3. [Variables y Constantes](#variables-y-constantes)
4. [Tipos de Datos](#tipos-de-datos)
5. [Operadores](#operadores)
6. [Control de Flujo](#control-de-flujo)
7. [Funciones y Métodos](#funciones-y-métodos)
8. [Programación Orientada a Objetos](#programación-orientada-a-objetos)
9. [Colecciones](#colecciones)
10. [Diferencias Clave: JavaScript vs C#](#diferencias-clave-javascript-vs-c)
11. [Errores Comunes](#errores-comunes)

---

## Descripción General del Lenguaje

### ¿Qué es C#?
C# es un lenguaje de programación moderno, orientado a objetos y seguro en tipos desarrollado por Microsoft. Se ejecuta en el framework .NET y está diseñado para ser simple, potente y seguro en tipos.

**Características Clave:**
- **Fuertemente tipado**: Las variables deben tener un tipo declarado
- **Compilado**: El código se compila a lenguaje intermedio (IL) antes de su ejecución
- **Orientado a objetos**: Todo es un objeto
- **Recolección de basura**: Gestión automática de memoria
- **Moderno**: Incluye características como async/await, LINQ, operadores null-condicionales

### Donde JavaScript es Dinámico, C# es Estático
```javascript
// JavaScript - Tipado dinámico
let x = 5;
x = "hola"; // Esto funciona bien
```

```csharp
// C# - Tipado estático
int x = 5;
x = "hola"; // Error de compilación
```

---

## Sistema de Tipos

### Declaración Explícita de Tipos
C# requiere que declares el tipo de cada variable, propiedad y parámetro.

```csharp
// Sintaxis básica
string nombre = "Juan";
int edad = 30;
double salario = 50000.50;
bool activo = true;
```

### Inferencia de Tipos con `var`
C# tiene inferencia de tipos usando la palabra clave `var` (similar a `let`/`const` de JavaScript, pero aún fuertemente tipado):

```csharp
var nombre = "Juan";         // Se infiere como string
var edad = 30;               // Se infiere como int
var items = new List<string>(); // Se infiere como List<string>

// ¡El tipo es fijo en tiempo de compilación!
// Esto causaría un error de compilación:
// nombre = 123; // Error: no se puede convertir int a string
```

---

## Variables y Constantes

### Declaración de Variables

```csharp
// Variable local
int contador = 10;

// Múltiples declaraciones
int x = 1, y = 2, z = 3;

// Con palabra clave var
var mensaje = "Hola";

// Tipos nullable (pueden ser nulos)
string? cadena_nula = null; // El ? significa que puede ser null
int? entero_nulo = null;
```

### Constantes

```csharp
// Constante en tiempo de compilación
const int MAX_USUARIOS = 100;

// Constante en tiempo de ejecución (no puede ser cambiada después)
readonly string UrlBaseDatos = "cadena_conexión";

// Constante a nivel de clase
public const double PI = 3.14159;
```

**Diferencia Clave de JavaScript:**
- JavaScript tiene `const`, pero solo previene reasignación. Las constantes de C# son verdaderamente inmutables.

---

## Tipos de Datos

### Tipos Primitivos

```csharp
// Tipos numéricos
int numero = 42;              // Entero de 32-bit
long numeroGrande = 9999999999;  // Entero de 64-bit
float precio = 19.99f;        // Punto flotante de 32-bit (necesita sufijo 'f')
double salario = 50000.50;    // Punto flotante de 64-bit
decimal dinero = 99.99m;      // Precisión alta (para dinero)
byte numeroPequeno = 255;     // Sin signo de 8-bit

// Booleano
bool activo = true;

// Carácter
char letra = 'A';

// Cadena
string nombre = "Juan Pérez";
```

### Tipos de Referencia

```csharp
// String (tipo de referencia, no primitivo)
string texto = "Hola";

// Object (tipo base para todas las clases)
object obj = "cualquier cosa";

// Array (tamaño fijo)
int[] numeros = new int[5];
int[] puntuaciones = { 10, 20, 30 };

// List (tamaño dinámico, de System.Collections.Generic)
using System.Collections.Generic;
List<int> lista = new List<int> { 1, 2, 3 };

// Diccionario
Dictionary<string, int> edades = new Dictionary<string, int>
{
    { "Juan", 30 },
    { "Jane", 28 }
};
```

### Tipos Nullable

```csharp
// C# 8.0+ tipos de referencia nullable
string? cadenaNula = null;
int? enteroNulo = null;

// Operador null-coalescing
string nombre = cadenaNula ?? "Desconocido"; // "Desconocido" si es null
```

---

## Operadores

### Operadores Aritméticos
```csharp
int a = 10, b = 3;
int suma = a + b;        // 13
int resta = a - b;       // 7
int producto = a * b;    // 30
int cociente = a / b;    // 3 (división entera)
int residuo = a % b;     // 1
```

### Operadores de Comparación
```csharp
5 == 5    // true
5 != 3    // true
5 > 3     // true
5 >= 5    // true
```

### Operadores Lógicos
```csharp
bool x = true && false;  // false (Y)
bool y = true || false;  // true (O)
bool z = !true;          // false (NO)
```

### Null-Conditional y Null-Coalescing
```csharp
string? texto = null;

// Operador null-condicional (?.)
string? resultado = texto?.ToUpper();  // Retorna null en lugar de lanzar error

// Operador null-coalescing (??)
string nombre = valorNulo ?? "Predeterminado";

// Asignación null-coalescing (??=)
string? valor = null;
valor ??= "Predeterminado";  // valor ahora es "Predeterminado"
```

---

## Control de Flujo

### Sentencias If-Else
```csharp
int edad = 20;

if (edad < 13)
{
    Console.WriteLine("Niño");
}
else if (edad < 18)
{
    Console.WriteLine("Adolescente");
}
else
{
    Console.WriteLine("Adulto");
}

// Operador ternario (igual que JavaScript)
string categoria = edad >= 18 ? "Adulto" : "Menor";
```

### Sentencias Switch
```csharp
int dia = 3;

switch (dia)
{
    case 1:
        Console.WriteLine("Lunes");
        break;
    case 2:
        Console.WriteLine("Martes");
        break;
    default:
        Console.WriteLine("Otro día");
        break;
}

// Expresión switch moderna (C# 8.0+)
string nombreDia = dia switch
{
    1 => "Lunes",
    2 => "Martes",
    3 => "Miércoles",
    _ => "Otro"
};
```

### Bucles

```csharp
// Bucle for
for (int i = 0; i < 5; i++)
{
    Console.WriteLine(i);
}

// Bucle while
int contador = 0;
while (contador < 5)
{
    Console.WriteLine(contador);
    contador++;
}

// Bucle do-while
do
{
    Console.WriteLine(contador);
} while (contador < 5);

// Bucle foreach
int[] numeros = { 1, 2, 3, 4, 5 };
foreach (int num in numeros)
{
    Console.WriteLine(num);
}

// Foreach con interpolación de cadenas
foreach (var item in items)
{
    Console.WriteLine($"Elemento: {item}");
}
```

---

## Funciones y Métodos

### Definición Básica de Método

```csharp
// Tipo de retorno, nombre del método, parámetros
public string Saludar(string nombre)
{
    return $"¡Hola, {nombre}!";
}

// Sin valor de retorno (void)
public void ImprimirMensaje(string mensaje)
{
    Console.WriteLine(mensaje);
}

// Múltiples parámetros
public int Sumar(int a, int b)
{
    return a + b;
}

// Parámetros por defecto
public void Log(string mensaje, NivelLog nivel = NivelLog.Info)
{
    // implementación
}

// Parámetros out (retorna múltiples valores)
public bool TryParse(string entrada, out int resultado)
{
    return int.TryParse(entrada, out resultado);
}

// Uso
if (TryParse("123", out int numero))
{
    Console.WriteLine(numero);
}
```

### Parámetros Nombrados y Opcionales

```csharp
public void Ordenar(string articulo, int cantidad = 1, string tamaño = "Mediano")
{
    Console.WriteLine($"{cantidad} {tamaño} {articulo}(s)");
}

// Uso
Ordenar("Café");                                    // Usa valores predeterminados
Ordenar("Café", 2);                                 // cantidad = 2
Ordenar("Café", tamaño: "Grande");                  // Parámetro nombrado
Ordenar(articulo: "Café", cantidad: 3, tamaño: "Grande"); // Todos nombrados
```

### Sobrecarga de Métodos

```csharp
// Mismo nombre de método, parámetros diferentes
public void Imprimir(int valor)
{
    Console.WriteLine("Int: " + valor);
}

public void Imprimir(string valor)
{
    Console.WriteLine("String: " + valor);
}

public void Imprimir(double valor)
{
    Console.WriteLine("Double: " + valor);
}

// C# determina cuál llamar basándose en los tipos de argumentos
Imprimir(42);         // Llama a Imprimir(int)
Imprimir("hola");     // Llama a Imprimir(string)
Imprimir(3.14);       // Llama a Imprimir(double)
```

---

## Programación Orientada a Objetos

### Clases

```csharp
public class Persona
{
    // Campos (privados por defecto)
    private string _nombre;
    private int _edad;

    // Propiedades (auto-implementadas)
    public string Nombre { get; set; }
    public int Edad { get; set; }

    // Propiedad con getter/setter personalizado
    public string Email
    {
        get { return _email; }
        set { _email = value; }
    }

    // Constructor
    public Persona(string nombre, int edad)
    {
        Nombre = nombre;
        Edad = edad;
    }

    // Método
    public void Presentar()
    {
        Console.WriteLine($"Hola, me llamo {Nombre} y tengo {Edad} años");
    }

    // Método estático
    public static Persona CrearPredeterminado()
    {
        return new Persona("Juan", 30);
    }
}

// Uso
var persona = new Persona("Alicia", 25);
persona.Presentar();
```

### Propiedades

```csharp
public class Usuario
{
    // Auto-propiedad (getter y setter generados automáticamente)
    public string NombreUsuario { get; set; }

    // Propiedad con lógica
    private int _edad;
    public int Edad
    {
        get { return _edad; }
        set
        {
            if (value >= 0)
                _edad = value;
        }
    }

    // Propiedad de solo lectura
    public string IdUsuario { get; private set; }

    // Propiedad con cuerpo de expresión (C# 6.0+)
    public string InfoCompleta => $"{NombreUsuario} (Edad: {Edad})";

    public Usuario(string nombreUsuario)
    {
        NombreUsuario = nombreUsuario;
        IdUsuario = Guid.NewGuid().ToString();
    }
}
```

### Herencia

```csharp
public class Animal
{
    public string Nombre { get; set; }

    public virtual void HacerSonido()
    {
        Console.WriteLine("Algún sonido genérico de animal");
    }
}

public class Perro : Animal
{
    // Sobrescribir método del padre
    public override void HacerSonido()
    {
        Console.WriteLine("¡Guau!");
    }

    public void Traer()
    {
        Console.WriteLine("Trayendo la pelota");
    }
}

// Uso
Animal perro = new Perro { Nombre = "Buddy" };
perro.HacerSonido(); // Salida: ¡Guau!
```

### Interfaces

```csharp
public interface IRegistrador
{
    void Registrar(string mensaje);
    void Error(string mensaje);
}

public class RegistradorConsola : IRegistrador
{
    public void Registrar(string mensaje)
    {
        Console.WriteLine(mensaje);
    }

    public void Error(string mensaje)
    {
        Console.ForegroundColor = ConsoleColor.Red;
        Console.WriteLine(mensaje);
        Console.ResetColor();
    }
}

// Uso
IRegistrador registrador = new RegistradorConsola();
registrador.Registrar("Aplicación iniciada");
```

### Clases Abstractas

```csharp
public abstract class Forma
{
    public abstract double ObtenerArea();

    public void Mostrar()
    {
        Console.WriteLine($"Área: {ObtenerArea()}");
    }
}

public class Circulo : Forma
{
    private double _radio;

    public Circulo(double radio)
    {
        _radio = radio;
    }

    public override double ObtenerArea()
    {
        return Math.PI * _radio * _radio;
    }
}
```

---

## Colecciones

### Arrays

```csharp
// Colección de tamaño fijo
int[] numeros = new int[5];
int[] puntuaciones = { 10, 20, 30, 40, 50 };

// Multi-dimensional
int[,] matriz = new int[3, 3];
int[][] dentada = new int[3][]; // Array dentado

// Acceder a elementos
int primero = puntuaciones[0];
puntuaciones[1] = 25;
```

### List<T> (Lista Genérica)

```csharp
using System.Collections.Generic;

List<int> numeros = new List<int> { 1, 2, 3 };
numeros.Add(4);
numeros.Remove(2);
numeros.Insert(0, 0);

// Iteración
foreach (int num in numeros)
{
    Console.WriteLine(num);
}

// LINQ
var numerospares = numeros.Where(x => x % 2 == 0).ToList();
```

### Dictionary<K, V>

```csharp
Dictionary<string, int> edades = new Dictionary<string, int>
{
    { "Alicia", 30 },
    { "Bob", 25 }
};

// Agregar/Acceder
edades["Carlos"] = 35;
int edadAlicia = edades["Alicia"];

// Verificar si la clave existe
if (edades.ContainsKey("Alicia"))
{
    Console.WriteLine(edades["Alicia"]);
}

// Iterar
foreach (var kvp in edades)
{
    Console.WriteLine($"{kvp.Key}: {kvp.Value}");
}
```

### Métodos LINQ Útiles

```csharp
using System.Linq;

List<int> numeros = new List<int> { 1, 2, 3, 4, 5 };

// Filtrar
var pares = numeros.Where(x => x % 2 == 0);

// Transformar
var duplicados = numeros.Select(x => x * 2);

// Agregar
int suma = numeros.Sum();
int maximo = numeros.Max();
int minimo = numeros.Min();
int cantidad = numeros.Count();

// Ordenar
var ordenado = numeros.OrderBy(x => x);
var descendente = numeros.OrderByDescending(x => x);

// Verificar condiciones
bool tienepar = numeros.Any(x => x % 2 == 0);
bool todosPositivos = numeros.All(x => x > 0);
```

---

## Diferencias Clave: JavaScript vs C#

| Característica | JavaScript | C# |
|---------|-----------|-----|
| **Sistema de Tipos** | Dinámico (débilmente tipado) | Estático (fuertemente tipado) |
| **Compilación** | Interpretado | Compilado a IL |
| **Sintaxis de Clase** | Clases ES6 o prototipos | Sintaxis completa de clase |
| **Modificadores de Acceso** | No se aplican | public, private, protected |
| **Sobrecarga de Métodos** | No soportado | Soportado |
| **Herencia** | Basada en prototipo | Basada en clase |
| **Interfaces** | No incorporado | Soporte completo de interfaz |
| **Genéricos** | No nativo | Soporte completo de genéricos |
| **Async/Await** | Callbacks/Promises/async-await | async/await (similar) |
| **Manejo de Null** | undefined/null | null, tipos de referencia nullable |
| **Sintaxis de Función** | `function` o `=>` | `public/private` + sintaxis de tipo |
| **Gestión de Paquetes** | npm | NuGet |
| **Sistema de Módulos** | Módulos ES | Espacios de nombres |

### Comparación Lado a Lado

#### Declaración de Variables
```javascript
// JavaScript
let nombre = "Juan";
const edad = 30;
var correo = "juan@ejemplo.com";
```

```csharp
// C#
string nombre = "Juan";
int edad = 30;
string correo = "juan@ejemplo.com";
```

#### Definición de Función
```javascript
// JavaScript
function sumar(a, b) {
    return a + b;
}

const multiplicar = (a, b) => a * b;
```

```csharp
// C#
public int Sumar(int a, int b)
{
    return a + b;
}

public int Multiplicar(int a, int b) => a * b;
```

#### Definición de Clase
```javascript
// JavaScript
class Persona {
    constructor(nombre, edad) {
        this.nombre = nombre;
        this.edad = edad;
    }

    saludar() {
        return `Hola, soy ${this.nombre}`;
    }
}
```

```csharp
// C#
public class Persona
{
    public string Nombre { get; set; }
    public int Edad { get; set; }

    public Persona(string nombre, int edad)
    {
        Nombre = nombre;
        Edad = edad;
    }

    public string Saludar()
    {
        return $"Hola, soy {Nombre}";
    }
}
```

#### Operaciones con Arrays/Lists
```javascript
// JavaScript
const numeros = [1, 2, 3, 4, 5];
const pares = numeros.filter(x => x % 2 === 0);
const duplicados = numeros.map(x => x * 2);
```

```csharp
// C#
List<int> numeros = new List<int> { 1, 2, 3, 4, 5 };
var pares = numeros.Where(x => x % 2 == 0);
var duplicados = numeros.Select(x => x * 2);
```

#### Literales de Objeto vs Objetos
```javascript
// JavaScript - Literal de objeto
const persona = {
    nombre: "Juan",
    edad: 30,
    saludar: function() { return "¡Hola!"; }
};
```

```csharp
// C# - Instancia de una clase
var persona = new Persona { Nombre = "Juan", Edad = 30 };
persona.Saludar();
```

---

## Errores Comunes

### 1. **Los Punto y Coma son Requeridos**
```csharp
// Esto causará un error de compilación
string nombre = "Juan"  // ¡Falta punto y coma!

// Correcto
string nombre = "Juan";
```

### 2. **Sensibilidad a Mayúsculas en Sentencias Switch**
```csharp
// Debe incluir 'break' para prevenir caída
switch (dia)
{
    case 1:
        Console.WriteLine("Lunes");
        break;  // ¡Requerido!
    case 2:
        Console.WriteLine("Martes");
        break;
}
```

### 3. **String vs string**
```csharp
// string (minúsculas) es un alias para System.String
string texto = "hola";
String texto2 = "hola";  // Ambos son lo mismo

// Convención: usar minúsculas 'string'
```

### 4. **Tipos de Valor vs Tipos de Referencia**
```csharp
// Tipo de valor (copiado)
int x = 5;
int y = x;
y = 10;
Console.WriteLine(x); // Aún es 5

// Tipo de referencia (referencia copiada)
List<int> lista1 = new List<int> { 1, 2, 3 };
List<int> lista2 = lista1;
lista2.Add(4);
Console.WriteLine(lista1.Count); // 4 - ¡ambas se refieren a la misma lista!
```

### 5. **Comparación de Igualdad**
```csharp
// Para tipos de referencia, == verifica igualdad de referencia
string a = new string(new[] { 'a' });
string b = new string(new[] { 'a' });
Console.WriteLine(a == b);        // true (string sobrescribe ==)
Console.WriteLine(a.Equals(b));   // true

// Para tipos de referencia sin == sobrescrito
object obj1 = new object();
object obj2 = obj1;
Console.WriteLine(obj1 == obj2);  // true (misma referencia)
```

### 6. **Excepción de Referencia Nula**
```csharp
string? texto = null;
// Esto lanzará NullReferenceException
// int longitud = texto.Length;

// Usar operador null-condicional
int? longitud = texto?.Length;  // null en lugar de excepción
```

### 7. **Sentencias Using (Disposición de Recursos)**
```csharp
// Debe disponer los recursos apropiadamente
using (FileStream fs = new FileStream("archivo.txt", FileMode.Open))
{
    // Usar fs
} // fs se dispone automáticamente

// Declaración using moderna (C# 8.0+)
using FileStream fs = new FileStream("archivo.txt", FileMode.Open);
// Usar fs
// fs se dispone automáticamente al final del alcance
```

### 8. **Compilación Requerida**
```csharp
// JavaScript - Verificación de tipos en tiempo de ejecución
let x = "hola";
x = 123;  // Sin error hasta que lo uses como string

// C# - Verificación de tipos en tiempo de compilación
string x = "hola";
x = 123;  // ¡Error de compilación inmediatamente!
```

---

## Consejos Esenciales para Desarrolladores de JavaScript

1. **Espera Tipado Estricto**: Cada variable debe tener un tipo. Si no estás seguro, usa `var` y deja que C# lo infiera.

2. **Usa Convenciones de Nombres**:
   - Clases: `PascalCase` (e.g., `GestorUsuarios`)
   - Métodos: `PascalCase` (e.g., `ObtenerNombreUsuario`)
   - Propiedades: `PascalCase` (e.g., `Nombre`)
   - Variables: `camelCase` (e.g., `nombre`)
   - Constantes: `MAYUSCULAS` o `PascalCase`

3. **Entiende Modificadores de Acceso**: C# aplica encapsulamiento con `public`, `private`, `protected`.

4. **Usa Propiedades en lugar de Getters/Setters**: Las propiedades de C# son más idiomáticas que métodos getter/setter.

5. **Aprovecha LINQ**: LINQ de C# es extremadamente potente para consultar y transformar colecciones.

6. **Async/Await Funciona Similarmente**: Si conoces async/await de JavaScript, el de C# te resultará familiar.

7. **Lee Mensajes de Error**: Los errores de compilación de C# atraparán muchos bugs que JavaScript solo encontraría en tiempo de ejecución.

---

## Referencia Rápida

### Clases y Métodos Comunes
```csharp
// Métodos de string
string texto = "Hola Mundo";
texto.ToUpper();
texto.ToLower();
texto.Length;
texto.Contains("Mundo");
texto.Replace("Mundo", "C#");
texto.Split(' ');

// Salida de consola
Console.WriteLine("mensaje");
Console.Write("sin nueva línea");
Console.ReadLine(); // Leer entrada del usuario

// Math
Math.Abs(-5);
Math.Round(3.14);
Math.Max(5, 10);
Math.Min(5, 10);
Math.Pow(2, 3); // 2^3

// DateTime
DateTime ahora = DateTime.Now;
DateTime fecha = new DateTime(2026, 3, 30);
TimeSpan duracion = new TimeSpan(hours: 1, minutes: 30, seconds: 0);
```

---

## Próximos Pasos

- Practica escribiendo clases y métodos
- Aprende sobre espacios de nombres y organización de código
- Explora async/await para programación asincrónica
- Estudia LINQ para manipulación de datos
- Aprende sobre inyección de dependencias
- Explora el ecosistema .NET y frameworks populares (ASP.NET Core, Entity Framework)

