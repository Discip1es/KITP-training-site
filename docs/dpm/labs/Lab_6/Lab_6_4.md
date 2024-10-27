# Перегрузка методов в C#.

**Перегрузка методов** (Method Overloading) в C# — это возможность создания нескольких методов с одинаковым именем, но с разными параметрами. Компилятор выбирает подходящую версию метода, исходя из количества, типов и порядка параметров, переданных при вызове. Это позволяет реализовывать разные вариации логики в зависимости от переданных данных, сохраняя при этом удобочитаемость и единообразие кода.

### Основные правила перегрузки методов

1. Методы должны иметь одинаковое имя.
2. Методы должны отличаться по типам, количеству или порядку параметров.
3. Возвращаемый тип **не участвует** в выборе перегруженного метода, то есть методы, различающиеся только возвращаемым типом, не будут считаться перегруженными.

## Пример базовой перегрузки методов

Рассмотрим класс `Calculator`, в котором реализована перегрузка метода `Add`:

```csharp
using System;

class Calculator
{
    // Метод для сложения двух целых чисел
    public int Add(int a, int b)
    {
        return a + b;
    }

    // Перегруженный метод для сложения трех целых чисел
    public int Add(int a, int b, int c)
    {
        return a + b + c;
    }

    // Перегруженный метод для сложения двух чисел с плавающей запятой
    public double Add(double a, double b)
    {
        return a + b;
    }
}

class Program
{
    static void Main()
    {
        Calculator calc = new Calculator();

        Console.WriteLine(calc.Add(2, 3));         // Вызов метода Add(int, int)
        Console.WriteLine(calc.Add(2, 3, 4));      // Вызов метода Add(int, int, int)
        Console.WriteLine(calc.Add(2.5, 3.5));     // Вызов метода Add(double, double)
    }
}
```

### Вывод программы:
```
5
9
6.0
```

В этом примере компилятор сам выбирает нужный метод `Add`, основываясь на параметрах, переданных при вызове. 

## Перегрузка с различными типами параметров

Можно также создать перегрузки, принимающие параметры разных типов:

```csharp
using System;

class Printer
{
    public void Print(string message)
    {
        Console.WriteLine("String message: " + message);
    }

    public void Print(int number)
    {
        Console.WriteLine("Integer number: " + number);
    }

    public void Print(double number)
    {
        Console.WriteLine("Double number: " + number);
    }
}

class Program
{
    static void Main()
    {
        Printer printer = new Printer();

        printer.Print("Hello");     // Вызов метода Print(string)
        printer.Print(42);          // Вызов метода Print(int)
        printer.Print(3.14);        // Вызов метода Print(double)
    }
}
```

### Вывод программы:
```
String message: Hello
Integer number: 42
Double number: 3.14
```

## Перегрузка с разным порядком параметров

Также можно использовать перегрузку, изменяя порядок параметров:

```csharp
using System;

class MathOperations
{
    public void Multiply(int a, double b)
    {
        Console.WriteLine("Multiply(int, double): " + (a * b));
    }

    public void Multiply(double a, int b)
    {
        Console.WriteLine("Multiply(double, int): " + (a * b));
    }
}

class Program
{
    static void Main()
    {
        MathOperations mathOps = new MathOperations();

        mathOps.Multiply(2, 3.5);    // Вызов метода Multiply(int, double)
        mathOps.Multiply(3.5, 2);    // Вызов метода Multiply(double, int)
    }
}
```

### Вывод программы:
```
Multiply(int, double): 7
Multiply(double, int): 7
```

## Перегрузка с параметрами по умолчанию

C# не позволяет перегружать методы, только меняя значения по умолчанию параметров. Рассмотрим пример, где перегрузка по умолчанию не работает:

```csharp
using System;

class Demo
{
    // ОШИБКА: нельзя перегружать только за счет параметров по умолчанию
    public void ShowMessage(string message = "Default")
    {
        Console.WriteLine("Message: " + message);
    }

    public void ShowMessage()
    {
        Console.WriteLine("No message provided.");
    }
}
```

В данном примере будет ошибка компиляции. Параметры по умолчанию не создают новую сигнатуру метода, а значит, не поддерживают перегрузку.

## Перегрузка с `params`

Можно перегрузить метод, используя параметр `params`, который позволяет передавать переменное число аргументов:

```csharp
using System;

class ArrayOperations
{
    public void Sum(params int[] numbers)
    {
        int sum = 0;
        foreach (int num in numbers)
        {
            sum += num;
        }
        Console.WriteLine("Sum of numbers: " + sum);
    }

    public void Sum(double a, double b)
    {
        Console.WriteLine("Sum of two doubles: " + (a + b));
    }
}

class Program
{
    static void Main()
    {
        ArrayOperations arrayOps = new ArrayOperations();

        arrayOps.Sum(1, 2, 3, 4);        // Вызов метода Sum(params int[])
        arrayOps.Sum(2.5, 3.5);          // Вызов метода Sum(double, double)
    }
}
```

### Вывод программы:
```
Sum of numbers: 10
Sum of two doubles: 6.0
```

## Полиморфизм и перегрузка методов

Перегрузка методов часто используется в комбинации с **полиморфизмом**. Например, если в классе-наследнике требуется изменить поведение перегруженного метода, можно использовать **виртуальные методы** (`virtual`) и **переопределение** (`override`):

```csharp
using System;

class Animal
{
    public virtual void Speak()
    {
        Console.WriteLine("Animal speaks");
    }

    public void Speak(string message)
    {
        Console.WriteLine("Animal says: " + message);
    }
}

class Dog : Animal
{
    public override void Speak()
    {
        Console.WriteLine("Dog barks");
    }
}

class Program
{
    static void Main()
    {
        Dog dog = new Dog();

        dog.Speak();              // Вызов переопределенного метода Dog.Speak()
        dog.Speak("Hello");        // Вызов метода Animal.Speak(string)
    }
}
```

### Вывод программы:
```
Dog barks
Animal says: Hello
```

## Преимущества перегрузки методов

1. **Повышает читаемость**: Одно имя метода позволяет реализовать разные действия в зависимости от параметров, делая код понятным.
2. **Сокращает код**: Нет необходимости создавать несколько методов с похожей функциональностью и разными именами.
3. **Гибкость**: Поддержка различных вариантов вызова метода, что упрощает использование библиотеки или API.

## Заключение

Перегрузка методов в C# — это мощный инструмент, позволяющий создавать методы с одинаковым именем, но разными параметрами. 