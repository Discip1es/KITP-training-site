# Классы в C#.

## Цель работы
Ознакомиться с основными концепциями объектно-ориентированного программирования (ООП) в C#, изучить принципы работы с классами, конструкторами, методами, свойствами, инкапсуляцией и наследованием. Научиться создавать и использовать классы на практике.

## Теоретическая часть

### 1. Основные понятия и структура класса

Класс — это один из ключевых понятий объектно-ориентированного программирования (ООП). Он представляет собой шаблон для создания объектов, определяющий свойства (данные) и методы (функции), которые может иметь объект.

**Пример 1: Простейший класс**
```csharp
public class Person
{
    // Поля
    public string Name;
    public int Age;

    // Метод
    public void SayHello()
    {
        Console.WriteLine($"Hello, my name is {Name} and I am {Age} years old.");
    }
}
```
Этот пример демонстрирует создание класса `Person`, который содержит два поля `Name` и `Age`, а также метод `SayHello()`, который выводит приветствие.

### 2. Инкапсуляция

Инкапсуляция — это принцип ООП, заключающийся в ограничении доступа к данным и методам внутри класса. Обычно поля класса делаются приватными (private), а доступ к ним осуществляется через публичные свойства (public properties) или методы.

**Пример 2: Инкапсуляция с использованием свойств**
```csharp
public class Person
{
    // Приватные поля
    private string name;
    private int age;

    // Публичные свойства
    public string Name
    {
        get { return name; }
        set { name = value; }
    }

    public int Age
    {
        get { return age; }
        set
        {
            if (value >= 0)
                age = value;
        }
    }

    // Метод
    public void SayHello()
    {
        Console.WriteLine($"Hello, my name is {Name} and I am {Age} years old.");
    }
}
```
В этом примере поле `age` доступно только внутри класса, и его значение может быть установлено через свойство `Age`, которое проверяет, что возраст не отрицательный.

### 3. Конструкторы

Конструктор — это специальный метод, который вызывается при создании объекта класса. Конструкторы обычно используются для инициализации полей объекта.

**Пример 3: Использование конструктора**
```csharp
public class Person
{
    private string name;
    private int age;

    // Конструктор
    public Person(string name, int age)
    {
        this.name = name;
        this.age = age;
    }

    public void SayHello()
    {
        Console.WriteLine($"Hello, my name is {name} and I am {age} years old.");
    }
}

// Создание объекта класса
Person person = new Person("John", 30);
person.SayHello();
```
В этом примере создается объект класса `Person` с помощью конструктора, который инициализирует поля `name` и `age`.

### 4. Наследование

Наследование позволяет создавать новый класс на основе существующего, добавляя новые поля и методы или изменяя существующие. Это один из ключевых принципов ООП, который способствует повторному использованию кода.

**Пример 4: Наследование**
```csharp
public class Employee : Person
{
    private string position;

    // Конструктор
    public Employee(string name, int age, string position) : base(name, age)
    {
        this.position = position;
    }

    // Новый метод
    public void Work()
    {
        Console.WriteLine($"{Name} is working as a {position}.");
    }
}
```
В этом примере класс `Employee` наследует класс `Person`, добавляя новое поле `position` и метод `Work()`. Конструктор `Employee` использует базовый конструктор `Person` для инициализации общих полей.

### 5. Полиморфизм

Полиморфизм позволяет использовать один и тот же интерфейс для работы с разными типами объектов. В C# полиморфизм обычно достигается через виртуальные методы и их переопределение в производных классах.

**Пример 5: Полиморфизм**
```csharp
public class Person
{
    public string Name { get; set; }

    // Виртуальный метод
    public virtual void Greet()
    {
        Console.WriteLine("Hello!");
    }
}

public class Student : Person
{
    // Переопределение метода
    public override void Greet()
    {
        Console.WriteLine("Hello, I am a student.");
    }
}

public class Teacher : Person
{
    // Переопределение метода
    public override void Greet()
    {
        Console.WriteLine("Hello, I am a teacher.");
    }
}
```
В этом примере `Student` и `Teacher` — это классы, наследующие `Person` и переопределяющие метод `Greet()`. Вызов метода `Greet()` на объекте типа `Person` приведет к вызову соответствующей версии метода, в зависимости от фактического типа объекта.

### 6. Абстракция

Абстракция — это принцип ООП, который позволяет скрыть сложные детали реализации и показывать только важные для использования аспекты. В C# абстракция может быть реализована с помощью абстрактных классов и интерфейсов.

**Пример 6: Абстрактный класс**
```csharp
public abstract class Animal
{
    // Абстрактный метод (должен быть реализован в производных классах)
    public abstract void MakeSound();

    public void Sleep()
    {
        Console.WriteLine("Sleeping...");
    }
}

public class Dog : Animal
{
    // Реализация абстрактного метода
    public override void MakeSound()
    {
        Console.WriteLine("Woof!");
    }
}

public class Cat : Animal
{
    // Реализация абстрактного метода
    public override void MakeSound()
    {
        Console.WriteLine("Meow!");
    }
}
```
В этом примере `Animal` — это абстрактный класс, который содержит абстрактный метод `MakeSound()`. Классы `Dog` и `Cat` реализуют этот метод по-разному, предоставляя конкретные звуки для разных животных.

### 7. Интерфейсы

Интерфейсы определяют набор методов и свойств, которые класс должен реализовать. В отличие от абстрактных классов, интерфейсы не могут содержать реализацию методов.

**Пример 7: Интерфейс**
```csharp
public interface IMovable
{
    void Move();
}

public class Car : IMovable
{
    public void Move()
    {
        Console.WriteLine("The car is moving.");
    }
}

public class Bicycle : IMovable
{
    public void Move()
    {
        Console.WriteLine("The bicycle is moving.");
    }
}
```
В этом примере интерфейс `IMovable` определяет метод `Move()`, который должен быть реализован в классах `Car` и `Bicycle`. Эти классы реализуют интерфейс по-своему.

## Практическая часть

### Задание 1: Создание базового класса

1. Создайте класс `Product`, который будет содержать следующие поля:
    - `name` (название продукта);
    - `price` (цена продукта).
2. Добавьте конструктор для инициализации полей.
3. Создайте свойства для доступа к полям.
4. Добавьте метод `PrintInfo`, который будет выводить информацию о продукте.

### Задание 2: Наследование и полиморфизм

1. Создайте класс `ElectronicProduct`, который будет наследовать класс `Product`.
2. Добавьте поле `warrantyPeriod` (гарантийный период) и свойство для него.
3. Переопределите метод `PrintInfo`, чтобы он выводил информацию о гарантии.

### Задание 3: Работа с объектами и коллекциями

1. Создайте массив объектов класса `ElectronicProduct`.
2. Заполните массив данными о нескольких электронных продуктах (например, телефон, ноутбук, телевизор).
3. Выведите информацию обо всех продуктах из массива, используя метод `PrintInfo`.

### Индивидуальное задание №1: Работа с классами

Каждое задание предусматривает реализацию дополнения к основной части лабораторной работы с применением различных аспектов ООП.

**Вариант 1:**
Создайте класс `ClothingProduct`, наследующий `Product`. Добавьте поле `size` (размер) и метод `GetDiscountedPrice`, который возвращает цену с учетом скидки (например, 10%). Реализуйте вывод информации о продукте с учетом скидки.

**Вариант 2:**
Создайте класс `BookProduct`, наследующий `Product`. Добавьте поле `author` (автор) и метод `GetAge`, который рассчитывает возраст книги (например, по году издания). Реализуйте вывод информации о продукте с указанием возраста книги.

**Вариант 3:**
Создайте класс `FoodProduct`, наследующий `Product`. Добавьте поле `expirationDate` (срок годности) и метод `IsExpired`, который возвращает `true`, если продукт просрочен. Реализуйте вывод информации о продукте с проверкой на срок годности.

**Вариант 4:**
Создайте класс `FurnitureProduct`, наследующий `Product`. Добавьте поле `material` (материал) и метод `CalculateShippingCost`, который рассчитывает стоимость доставки в зависимости от веса (например, 10 долларов за кг). Реализуйте вывод информации о продукте с расчетом стоимости доставки.

**Вариант 5:**
Создайте класс `SoftwareProduct`, наследующий `Product`. Добавьте поле `licenseKey` (лицензионный ключ) и метод `ValidateLicense`, который проверяет правильность лицензионного ключа (например, должен состоять из 16 символов). Реализуйте вывод информации о продукте с проверкой лицензии.

### Индивидуальное задание №2: Работа с абстрактными классами и наследованием

**Вариант 1:**
Создайте абстрактный класс `Shape`, представляющий геометрическую фигуру, с абстрактными методами `CalculateArea()` и `CalculatePerimeter()`. Реализуйте два класса, наследующих `Shape`: `Circle` и `Rectangle`. В классе `Circle` реализуйте методы для расчета площади и периметра круга, а в классе `Rectangle` — для прямоугольника. Реализуйте метод, который будет выводить информацию о фигуре, её площади и периметре.

**Вариант 2:**
Создайте абстрактный класс `Animal`, представляющий животное, с абстрактными методами `MakeSound()` и `Move()`. Реализуйте два класса, наследующих `Animal`: `Dog` и `Bird`. В классе `Dog` реализуйте методы, которые будут выводить звук собаки и описание её передвижения, а в классе `Bird` — звук птицы и описание её полета. Реализуйте метод для вывода информации о каждом животном.

**Вариант 3:**
Создайте абстрактный класс `Appliance`, представляющий бытовой прибор, с абстрактным методом `TurnOn()`. Реализуйте два класса, наследующих `Appliance`: `WashingMachine` и `Refrigerator`. В классе `WashingMachine` реализуйте метод, имитирующий включение стиральной машины, а в классе `Refrigerator` — включение холодильника. Реализуйте метод, который будет выводить информацию о включении каждого прибора.

**Вариант 4:**
Создайте абстрактный класс `Payment`, представляющий платеж, с абстрактным методом `ProcessPayment()`. Реализуйте два класса, наследующих `Payment`: `CreditCardPayment` и `PayPalPayment`. В классе `CreditCardPayment` реализуйте метод, имитирующий обработку платежа через кредитную карту, а в классе `PayPalPayment` — обработку платежа через PayPal. Реализуйте метод для вывода информации о процессе каждого платежа.

**Вариант 5:**
Создайте абстрактный класс `Employee`, представляющий сотрудника, с абстрактными методами `CalculateSalary()` и `GetPosition()`. Реализуйте два класса, наследующих `Employee`: `Manager` и `Developer`. В классе `Manager` реализуйте методы для расчета зарплаты менеджера и получения его должности, а в классе `Developer` — методы для расчета зарплаты разработчика и получения его должности. Реализуйте метод для вывода информации о зарплате и должности каждого сотрудника.

### Индивидуальное задание №3: Использование интерфейсов и реализации различных классов

**Вариант 1:**
Создайте интерфейс `IDriveable`, представляющий транспортное средство, с методами `Start()` и `Stop()`. Реализуйте два класса: `Car` и `Bike`, которые будут реализовывать интерфейс `IDriveable`. В классе `Car` реализуйте методы для запуска и остановки автомобиля, а в классе `Bike` — для запуска и остановки велосипеда. Реализуйте метод, который будет выводить информацию о запуске и остановке каждого транспортного средства.

**Вариант 2:**
Создайте интерфейс `IPayable`, представляющий объект, за который можно заплатить, с методом `Pay()`. Реализуйте два класса: `Invoice` и `Subscription`, которые будут реализовывать интерфейс `IPayable`. В классе `Invoice` реализуйте метод для оплаты счета, а в классе `Subscription` — метод для оплаты подписки. Реализуйте метод для вывода информации об оплате каждого объекта.

**Вариант 3:**
Создайте интерфейс `IPlayable`, представляющий играемый объект, с методами `Play()` и `Pause()`. Реализуйте два класса: `Song` и `Video`, которые будут реализовывать интерфейс `IPlayable`. В классе `Song` реализуйте методы для воспроизведения и паузы песни, а в классе `Video` — для воспроизведения и паузы видео. Реализуйте метод для вывода информации о воспроизведении и паузе каждого объекта.

**Вариант 4:**
Создайте интерфейс `ICookable`, представляющий объект, который можно приготовить, с методами `Prepare()` и `Cook()`. Реализуйте два класса: `Pizza` и `Soup`, которые будут реализовывать интерфейс `ICookable`. В классе `Pizza` реализуйте методы для подготовки и приготовления пиццы, а в классе `Soup` — для подготовки и приготовления супа. Реализуйте метод для вывода информации о подготовке и приготовлении каждого блюда.

**Вариант 5:**
Создайте интерфейс `IBookable`, представляющий объект, который можно забронировать, с методами `Book()` и `CancelBooking()`. Реализуйте два класса: `HotelRoom` и `Flight`, которые будут реализовывать интерфейс `IBookable`. В классе `HotelRoom` реализуйте методы для бронирования и отмены бронирования гостиничного номера, а в классе `Flight` — для бронирования и отмены бронирования авиарейса. Реализуйте метод для вывода информации о бронировании и отмене бронирования каждого объекта.


## Оформление отчета

1. **Титульный лист**: название лабораторной работы, фамилия, имя, отчество, группа студента, дата выполнения.
2. **Ход работы**: описание выполнения каждого задания с исходным кодом.
3. **Выводы**: что было изучено и выполнено в ходе работы, какие сложности возникли и как они были решены.

## Критерии оценки

1. **Полнота выполнения**: правильное выполнение всех заданий.
2. **Качество кода**: читаемость, структурированность, использование комментариев.
3. **Отчет**: правильное и полное оформление всех разделов отчета.
4. **Тестирование**: правильность работы программы на примерах, отсутствие ошибок.