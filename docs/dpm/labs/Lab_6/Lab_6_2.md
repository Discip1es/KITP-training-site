# Создание методов C# с параметрами

## Введение
Методы способны выполнять операции над входными данными. Передача параметров в методы позволяет выполнять задачу метода с различными входными значениями. Использование параметров метода позволяет расширить код, сохраняя при этом организованность и читабельность программы. Если рассматривать метод как «черный ящик», принимающий входные данные и выполняющий единственную задачу, можно быстро разделить большую проблему на выполнимые части.  

Предположим, вам нужно написать код, выполняющий одну и ту же операцию над разными наборами входных данных. У вас может быть три разных массива, и вам нужно отобразить содержимое каждого из них. Вы можете создать метод `DisplayArray`, который принимает на вход один массив и выводит его содержимое. Вместо того чтобы писать код для отображения каждого отдельного массива, вы можете вызвать один и тот же метод и предоставить в качестве входных данных разные массивы.  

Параметры могут сделать ваши методы более надежными, выполняя при этом одну и ту же общую задачу. В этом модуле вы узнаете больше о работе с параметрами и закрепите свое понимание методов.

## Цели обучения  

В этом модуле вы узнаете:  

- Узнаете больше об использовании параметров
- Поймете область видимости метода
- Разберетесь в типах параметров pass-by-reference и pass-by-value
- Узнаете, как использовать необязательные и именованные аргументы

## Использование параметров в методах

При создании методов часто возникает необходимость предоставить методу некоторую информацию для использования. Информация, используемая методом, называется параметром. Вы можете предоставить столько параметров, сколько необходимо для выполнения задачи, или не предоставлять их вовсе.Термины «параметр» и «аргумент» часто используются как взаимозаменяемые. Однако «параметр» означает переменную в сигнатуре метода. «Аргумент» - это значение, передаваемое при вызове метода.

### Добавьте параметры в методы

Параметры в методе работают аналогично переменным. Параметр определяется путем указания типа данных, за которым следует имя параметра. Параметры объявляются в сигнатуре метода, а значения параметров предоставляются вызывающей стороной метода, а не инициализируются в самом методе. Рассмотрим следующий код:

```cs
CountTo(5);

	void CountTo(int max) 
	{
		for (int i = 0; i < max; i++)
		{
			Console.Write($"{i}, ");
		}
	}
```
В этом примере метод `CountTo` принимает целочисленный параметр с именем `max`. На этот параметр ссылаются в цикле `for` метода. При вызове `CountTo` в качестве аргумента передается целое число `5`.  

В этом упражнении вы узнаете, как создавать и использовать собственные параметры метода.

### Создайте метод с параметрами

В этом задании вы создадите метод, который будет корректировать запланированное время в соответствии с другим часовым поясом GMT. Метод должен принимать список времен, текущий часовой пояс и новый часовой пояс. Давайте начнем!

1. Введите следующий код в редактор кода Visual Studio
```cs
int[] schedule = {800, 1200, 1600, 2000};
```
2. Чтобы создать метод с параметрами, введите следующий код в новой пустой строке:
```cs
void DisplayAdjustedTimes(int[] times, int currentGMT, int newGMT) 
{

}
```
Обратите внимание, что параметры объявляются аналогично тому, как объявляются переменные: с указанием типа данных, за которым следует имя переменной. Вы можете использовать параметры любого типа данных, например string, bool, int, массивы и многое другое! Несколько параметров в методе всегда разделяются запятыми.
3. Введите следующий код в метод `DisplayAdjustedTimes`:
```cs
int diff = 0;
if (Math.Abs(newGMT) > 12 || Math.Abs(currentGMT) > 12)
{
    Console.WriteLine("Invalid GMT");
}
```
Обратите внимание, что вам не нужно объявлять переменные `newGMT` и `currentGMT`, поскольку они уже объявлены в сигнатуре метода. Вы также не инициализируете переменные, поскольку метод предполагает, что вызывающая сторона предоставит эти аргументы с присвоенными значениями.  

На этом шаге вы создаете `int diff` для хранения разницы во времени, а затем проверяете, что предоставленные значения GMT находятся между -12 и 12. Использование `Math.Abs` позволяет получить абсолютное значение числа, поэтому значения GMT недействительны, если они больше 12.
4. Чтобы вычислить разницу во времени, обновите метод `DisplayAdjustedTimes` следующим образом:
```cs
int diff = 0;
if (Math.Abs(newGMT) > 12 || Math.Abs(currentGMT) > 12)
{
    Console.WriteLine("Invalid GMT");
}
else if (newGMT <= 0 && currentGMT <= 0 || newGMT >= 0 && currentGMT >= 0) 
{
    diff = 100 * (Math.Abs(newGMT) - Math.Abs(currentGMT));
} 
else 
{
    diff = 100 * (Math.Abs(newGMT) + Math.Abs(currentGMT));
}
```
В этом коде вы проверяете, нужно ли складывать или вычитать абсолютные значения часовых поясов по Гринвичу, чтобы получить разницу в часах. Если значения GMT имеют одинаковый знак (оба положительные или оба отрицательные), то разница в часах равна разнице между этими двумя числами. Если значения GMT имеют противоположные знаки, то разница равна сумме этих двух чисел. Поскольку часы представлены в сотнях, умножьте полученный результат на 100.
5. Чтобы отобразить результаты, введите следующий код в конце метода `DisplayAdjustedTimes`:
```cs
for (int i = 0; i < times.Length; i++) 
{
    int newTime = ((times[i] + diff)) % 2400;
    Console.WriteLine($"{times[i]} -> {newTime}");
}
```
6. Чтобы вызвать метод, введите следующий код после объявления переменной `int[] schedule`:
```cs
DisplayAdjustedTimes(schedule, 6, -6);
```
Обратите внимание, что в качестве аргументов метода могут использоваться как переменные, так и литералы. Используя входные параметры, метод не ограничивается использованием значений глобальных переменных.

7. Запустите приложение, убедитесь что вывод соответствует следующему:
```
800 -> 2000
1200 -> 0
1600 -> 400
2000 -> 800
```
Если ваш код показывает другие результаты, вам нужно пересмотреть код, чтобы найти ошибку и внести обновления. Запустите код снова, чтобы проверить, устранили ли вы проблему. Продолжайте обновлять и запускать код до тех пор, пока он не даст ожидаемые результаты.

## Область применения метода

Циклы `for`, операторы `if-else` и методы - все они представляют собой различные типы блоков кода. У каждого блока кода есть своя «область видимости». Область видимости» - это область программы, в которой доступны определенные данные. Переменные, объявленные внутри метода или любого блока кода, доступны только в этой области. По мере усложнения программ этот паттерн помогает программистам последовательно использовать переменные с четкими именами и поддерживать легко читаемый код.  

В этом упражнении вы узнаете больше об области видимости метода, работая с различными типами методов и переменных.

### Область действия тестовой переменной

Операторы, объявленные вне любого блока кода, называются операторами верхнего уровня. Переменные, объявленные в операторах верхнего уровня, называются «глобальными переменными». Глобальные переменные не ограничены какой-либо областью видимости и могут использоваться в любом месте программы. Глобальные переменные могут быть полезны для различных методов, которым требуется доступ к одним и тем же данным. Однако важно обращать внимание на имена переменных в разных областях видимости.

1. В редакторе кода Visual Studio удалите весь существующий код из предыдущих упражнений
2. Введите следующий код в редактор кода Visual Studio:
```cs
string[] students = {"Jenna", "Ayesha", "Carlos", "Viktor"};

DisplayStudents(students);
DisplayStudents(new string[] {"Robert","Vanya"});

void DisplayStudents(string[] students) 
{
    foreach (string student in students) 
    {
        Console.Write($"{student}, ");
    }
    Console.WriteLine();
}
```
В этом коде вы создаете глобальный массив `students` и метод `DisplayStudents`, который принимает одноименный параметр.

3. Сохраните и запустите код, чтобы увидеть следующий результат:
```
Jenna, Ayesha, Carlos, Viktor, 
Robert, Vanya,
```
Обратите внимание, что параметр метода `student` имеет приоритет над глобальным массивом `student`. Важно обдуманно подходить к выбору глобальных переменных, которые вы хотите использовать в своих методах.
4. Удалите предыдущий код. 
5. Введите в редактор следующий код:
```cs
PrintCircleArea(12);

void PrintCircleArea(int radius)
{
    double pi = 3.14159;
    double area = pi * (radius * radius);
    Console.WriteLine($"Area = {area}");
}
```
Этот код вычисляет и выводит на экран площадь круга. 
6. Попробуйте сослаться на переменные внутри метода `PrintCircleArea`, изменив код следующим образом:
```cs
PrintCircleArea(12);
double circumference = 2 * pi * radius;
```
Появляются сообщения об ошибках, сообщающие, что имена `pi` и `radius` не существуют в текущей области видимости. Эти переменные существуют только в области видимости метода `PrintCircleArea`.
7. Удалите неправильный код и добавьте следующий:
```cs
void PrintCircleCircumference(int radius)
{
    double pi = 3.14159;
    double circumference = 2 * pi * radius;
    Console.WriteLine($"Circumference = {circumference}");
}
```
Поскольку переменная `pi` устанавливается в одно и то же фиксированное значение и используется в обоих методах, это значение - хороший кандидат на роль глобальной переменной. В этом примере `radius` не является глобальной переменной, поэтому вы можете вызывать методы с разными значениями `radius`, не обновляя каждый раз переменную.
8. Обновите свой код следующим образом:
```cs
double pi = 3.14159;

void PrintCircleArea(int radius)
{
    double area = pi * (radius * radius);
    Console.WriteLine($"Area = {area}");
}

void PrintCircleCircumference(int radius)
{
    double circumference = 2 * pi * radius;
    Console.WriteLine($"Circumference = {circumference}");
}
```
Теперь оба метода могут ссылаться на одно и то же значение pi без необходимости его определения. Вы, наверное, уже догадались, что методы могут вызывать другие методы. Как правило, если метод определен в пределах области видимости вашей программы, он может быть вызван где угодно.
9. Добавьте в свой код новый метод следующим образом:
```cs
double pi = 3.14159;
PrintCircleInfo(12);
PrintCircleInfo(24);

void PrintCircleInfo(int radius) 
{
    Console.WriteLine($"Circle with radius {radius}");
    PrintCircleArea(radius);
    PrintCircleCircumference(radius);
}
```
В этом коде вы создаете новый метод `PrintCircleInfo` для вызова существующих методов. Значение радиуса также передается в каждый метод. Создание модульных методов поможет сохранить код организованным и легко читаемым.
10. Сохраните и запустите код, чтобы увидеть следующий результат:
```
Circle with radius 12
Area = 452.38896
Circumference = 75.39815999999999
Circle with radius 24
Area = 1809.55584
Circumference = 150.79631999999998
```
### Резюме
- Переменные, объявленные внутри метода, доступны только этому методу. 
- Переменные, объявленные в операторах верхнего уровня, доступны всей программе. 
- Методы не имеют доступа к переменным, определенным в других методах. 
- Методы могут вызывать другие методы.

## Используйте параметры значения и ссылочного типа

В C# переменные можно разделить на два основных типа: типы значений и ссылочные типы. Эти типы описывают, как переменные хранят свои значения.  

Типы значений, такие как `int`, `bool`, `float`, `double` и `char`, непосредственно содержат значения. Ссылочные типы, такие как `string`, `array` и объекты (например, экземпляры `Random`), не хранят свои значения напрямую. Вместо этого ссылочные типы хранят адрес, по которому хранится их значение.

### Параметры, передаваемые по значению и передаваемые по ссылке

Когда аргумент передается в метод, переменные типа value копируют свои значения в метод. Каждая переменная имеет свою собственную копию значения, поэтому исходная переменная не изменяется. 

При использовании ссылочных типов в метод передается адрес значения. Переменная, переданная методу, ссылается на значение по этому адресу, поэтому операции над этой переменной влияют на значение, на которое ссылается другая.

### Тест по значению

1. В редакторе кода Visual Studio удалите весь существующий код из предыдущих упражнений. 
2. Введите следующий код в редактор кода Visual Studio:
```cs
int a = 3;
int b = 4;
int c = 0;

Multiply(a, b, c);
Console.WriteLine($"global statement: {a} x {b} = {c}");

void Multiply(int a, int b, int c) 
{
    c = a * b;
    Console.WriteLine($"inside Multiply method: {a} x {b} = {c}");
}
```
В метод `Multiply` передаются переменные `a`, `b` и `c`. Значения переменных выводятся во время выполнения метода, а после его завершения - снова.  

Целые числа - это типы значений, значения которых копируются при передаче в методы. Как вы думаете, каким будет вывод `c`?

3. Сохраните и запустите код, чтобы увидеть следующий результат:
```
inside Multiply method: 3 x 4 = 12
global statement: 3 x 4 = 0
```
Обратите внимание, что значение `c` изменяется только внутри метода `Multiply`. За пределами метода `c` сохраняет свое первоначальное значение.

### Тест по ссылке

1. Удалите предыдущий код из редактора кода Visual Studio. 
2. Введите следующий код в редактор кода Visual Studio:
```cs
int[] array = {1, 2, 3, 4, 5};

PrintArray(array);
Clear(array);
PrintArray(array);

void PrintArray(int[] array) 
{
    foreach (int a in array) 
    {
        Console.Write($"{a} ");
    }
    Console.WriteLine();
}

void Clear(int[] array) 
{
    for (int i = 0; i < array.Length; i++) 
    {
        array[i] = 0;
    }
}
```
Код начинается с инициализации `массива`, содержащего несколько целочисленных значений. Значения выводятся на экран с помощью метода `PrintArray`. Для массива вызывается метод `Clear`, после чего массив снова выводится на печать.  

Массивы являются ссылочными типами. Ссылочные типы хранят адрес своих значений в памяти. Как вы думаете, что будет выведено на экран?

3. Сохраните и запустите код, чтобы увидеть следующий результат:
```
1 2 3 4 5 
0 0 0 0 0
```
Обратите внимание, что массив остается измененным за пределами области действия метода `Clear`. Это происходит потому, что метод `Clear` обновил значения, хранящиеся по каждому адресу.

### Тест со строками

Ранее вы узнали, что строки - это *неизменяемый* тип. Несмотря на то, что строка является ссылочным типом, в отличие от массива, ее значение не может быть изменено после присвоения. Вы могли заметить это, если использовали такие методы, как `string.Replace` или `string.ToUpper`. В этом задании вы научитесь исправлять распространенную ошибку, встречающуюся при работе со строками.

1. В редакторе кода Visual Studio удалите весь существующий код из предыдущих упражнений. 
2. Введите следующий код в редактор кода Visual Studio:
```cs
string status = "Healthy";

Console.WriteLine($"Start: {status}");
SetHealth(status, false);
Console.WriteLine($"End: {status}");

void SetHealth(string status, bool isHealthy) 
{
    status = (isHealthy ? "Healthy" : "Unhealthy");
    Console.WriteLine($"Middle: {status}");
}
```
3. Сохраните и запустите код, чтобы увидеть следующий результат:
```
Start: Healthy
Middle: Unhealthy
End: Healthy
```
Если метод `SetHealth` не вывел статус, можно было предположить, что метод выполнился некорректно. Вместо этого была создана новая строка со значением «Unhealthy», которая затем была потеряна в области видимости метода.  

Чтобы исправить эту проблему, вы можете изменить `SetHealth` так, чтобы вместо нее использовалась глобальная переменная состояния.

4. Обновите код следующим образом:
```cs
string status = "Healthy";

Console.WriteLine($"Start: {status}");
SetHealth(false);
Console.WriteLine($"End: {status}");

void SetHealth(bool isHealthy) 
{
    status = (isHealthy ? "Healthy" : "Unhealthy");
    Console.WriteLine($"Middle: {status}");
}
```
В этом коде вы перезаписываете глобальную переменную `status` новым строковым значением.

Сохраните и запустите код, чтобы увидеть следующий результат:
```
Start: Healthy
Middle: Unhealthy
End: Unhealthy
```
Теперь обновленная строка захватывается и сохраняется правильно.

### Резюме
- Переменные можно разделить на типы значений и ссылочные типы.
- Типы значений непосредственно содержат значения, а ссылочные типы хранят адрес значения.
- Методы, использующие аргументы типа значения, создают собственную копию значений.
- Методы, изменяющие параметр массива, влияют на исходный входной массив.
- String - неизменяемый ссылочный тип.
- Методы, изменяющие строковый параметр, не влияют на исходную строку.

## Методы с необязательными параметрами

Язык C# позволяет использовать именованные и необязательные параметры. Эти типы параметров позволяют вам выбирать, какие аргументы вы хотите передать методу, поэтому вы не ограничены структурой, определенной в сигнатуре метода.
Именованные аргументы позволяют указать значение параметра, используя его имя, а не позицию. Необязательные параметры позволяют опустить эти аргументы при вызове метода.

В этом упражнении вы узнаете, как использовать именованные и необязательные параметры.

### Создайте приложение RSVP
В контексте приглашений на мероприятия, RSVP — это запрос подтверждения от приглашённого человека или людей. RSVP — это акроним французской фразы Répondez s’il vous plaît, означающей буквально «Будьте добры ответить» или «Пожалуйста, ответьте»

В этом задании вы создадите короткое приложение для гостей, чтобы они могли оставить свой отзыв о мероприятии. Гости будут указывать размер своей компании и наличие аллергии. Вы также добавите возможность ограничить список приглашенных только приглашенными.

1. В редакторе кода Visual Studio удалите весь существующий код из предыдущих упражнений. 
2. Введите следующий код в редактор кода Visual Studio:
```cs
string[] guestList = {"Rebecca", "Nadia", "Noor", "Jonte"};
string[] rsvps = new string[10];
int count = 0;

void RSVP(string name, int partySize, string allergies, bool inviteOnly) 
{
    if (inviteOnly)
    {
        // search guestList before adding rsvp
    }

    rsvps[count] = $"Name: {name}, \tParty Size: {partySize}, \tAllergies: {allergies}";
    count++;
}

void ShowRSVPs()
{
    Console.WriteLine("\nTotal RSVPs:");
    for (int i = 0; i < count; i++)
    {
        Console.WriteLine(rsvps[i]);
    }
}
```
В этом коде вы создаете переменные для хранения списка приглашенных и списка rsvps. Метод `RSVP` добавляет информацию о гостях в список, а метод `ShowRSVPs` отображает общее количество RSVP, используя последовательность символов табуляции для разделения информации о гостях.
3. Введите следующий код в методе `RSVP`, чтобы найти список гостей:
```cs
if (inviteOnly)
{
    bool found = false;
    foreach (string guest in guestList)
    {
        if (guest.Equals(name)) {
            found = true;
            break;
        }
    }
    if (!found)
    {
        Console.WriteLine($"Sorry, {name} is not on the guest list");
        return;
    }
}
```
В этом коде вы проверяете, совпадает ли заданное имя с любым из имен в списке гостей. Если совпадение найдено, вы устанавливаете значение `found` в true и выходите из цикла `foreach`. Если значение `found` равно false, вы выводите сообщение и используете ключевое слово `return` для завершения метода.

4. Вызовите свой метод, добавив следующий код над сигнатурой метода `RSVP`:
```cs
RSVP("Rebecca", 1, "none", true);
RSVP("Nadia", 2, "Nuts", true);
RSVP("Linh", 2, "none", false);
RSVP("Tony", 1, "Jackfruit", true);
RSVP("Noor", 4, "none", false);
RSVP("Jonte", 2, "Stone fruit", false);
ShowRSVPs();
```
5. Сохраните и запустите код, чтобы увидеть следующий результат:
```
Sorry, Tony is not on the guest list

Total RSVPs:
Name: Rebecca,  Party Size: 1,  Allergies: none
Name: Nadia,    Party Size: 2,  Allergies: Nuts
Name: Linh,     Party Size: 2,  Allergies: none
Name: Noor,     Party Size: 4,  Allergies: none
Name: Jonte,    Party Size: 2,  Allergies: Stone fruit
```
### Используйте именованные аргументы

При вызове метода, принимающего множество параметров, бывает сложно понять, что представляют собой аргументы. Использование именованных аргументов может улучшить читаемость вашего кода. Используйте именованный аргумент, указывая имя параметра, за которым следует значение аргумента. В этом задании вы попрактикуетесь в использовании именованных аргументов.

1. Найдите следующую строку кода: RSVP("Linh", 2, "none", false); 
2. Обновите вызов метода следующим образом:
```cs
RSVP(name: "Linh", partySize: 2, allergies: "none", inviteOnly: false);
```
Обратите внимание, что вы указываете имя параметра, за которым следует двоеточие и значение. Этот синтаксис определяет именованный аргумент. Необязательно называть все аргументы. Например, следующий синтаксис также подходит:  

`RSVP(«Linh», 2, аллергия: «none», inviteOnly: false);` `RSVP(«Linh», partySize: 2, «none», false);`  

Именованные аргументы, используемые вместе с позиционными аргументами, действительны, если они используются в правильной позиции. Именованные аргументы также действительны, если за ними не следуют никакие позиционные аргументы. Например, включение `"Linh` » и `2` в конце будет недействительным:  

`RSVP(allergies: «none», inviteOnly: false, «Linh», 2);`  

Если бы вы ввели этот код, то получили бы следующую ошибку: `Именованный аргумент 'allergies' используется не по назначению, но за ним следует неименованный аргумент`

3. Найдите следующую строку кода: `RSVP(«Tony», 1, «Jackfruit», true);`
4. Обновите вызов метода следующим образом:
```cs
RSVP("Tony", inviteOnly: true, allergies: "Jackfruit",  partySize: 1);
```
Обратите внимание, что именованные аргументы не обязательно должны отображаться в исходном порядке. Однако неименованный аргумент Tony - это позиционный аргумент, и он должен появиться в соответствующей позиции.
5. Сохраните и запустите код, чтобы увидеть следующий результат:
```
Sorry, Tony is not on the guest list

Total RSVPs:
Name: Rebecca,  Party Size: 1,  Allergies: none
Name: Nadia,    Party Size: 2,  Allergies: Nuts
Name: Linh,     Party Size: 2,  Allergies: none
Name: Noor,     Party Size: 4,  Allergies: none
Name: Jonte,    Party Size: 2,  Allergies: Stone fruit
```
Обратите внимание, что использование именованных аргументов не меняет вывода.

### Объявление необязательных параметров

Параметр становится необязательным, когда ему присваивается значение по умолчанию. Если необязательный параметр опущен в аргументах, при выполнении метода используется значение по умолчанию. В этом шаге вы сделаете необязательными параметры `PartySize`, `allergies` и `inviteOnly`.

1. Чтобы определить необязательные параметры, обновите сигнатуру метода `RSVP` следующим образом:
```cs
void RSVP(string name, int partySize = 1, string allergies = "none", bool inviteOnly = true)
```
Обратите внимание на синтаксис. Параметры по-прежнему разделяются запятыми, но параметрам `partySize`, `allergies` и `inviteOnly` присвоено значение.  

Далее вы обновите вызовы `RSVP`, чтобы применить необязательные параметры.

2. Обновите свой код следующим образом:
```cs
RSVP("Rebecca");
RSVP("Nadia", 2, "Nuts");
RSVP(name: "Linh", partySize: 2, inviteOnly: false);
RSVP("Tony", allergies: "Jackfruit", inviteOnly: true);
RSVP("Noor", 4, inviteOnly: false);
RSVP("Jonte", 2, "Stone fruit", false);
```
Обратите внимание, что в каждом вызове метода имя никогда не опускается. При вызове метода все обязательные аргументы всегда должны быть включены. Однако любые необязательные аргументы могут быть опущены.  

В этом коде вы удалили аргументы `1, «none», true` из rsvp Ребекки. Поскольку эти аргументы соответствуют значению по умолчанию, результат rsvp Ребекки будет таким же.  

Вы удалили аргумент `inviteOnly` из rsvp Нади. Поскольку значение по умолчанию для `inviteOnly` равно `true`, результат rsvp Нади будет таким же.  

Вы удалили аргумент `PartySize` из rsvp Тони. Если бы у Тони было приглашение, в RSVP использовалось бы значение `partySize` по умолчанию.  

Вы удалили аргумент `allergies` из rsvp Линь и Нур. В их приглашениях будет отображаться значение по умолчанию `none` для «Аллергии».

3. Сохраните и запустите код, чтобы увидеть следующий результат:
```
Sorry, Tony is not on the guest list

Total RSVPs:
Name: Rebecca,  Party Size: 1,  Allergies: none
Name: Nadia,    Party Size: 2,  Allergies: Nuts
Name: Linh,     Party Size: 2,  Allergies: none
Name: Noor,     Party Size: 4,  Allergies: none
Name: Jonte,    Party Size: 2,  Allergies: Stone fruit
```
Обратите внимание, что вместо опущенных аргументов, таких как `partySize `и `allergies`, используются значения по умолчанию.

### Резюме
- Параметры становятся необязательными, задавая значение по умолчанию в сигнатуре метода.
- Именованные аргументы указываются с помощью имени параметра, за которым следует двоеточие и значение аргумента. 
- При комбинировании именованных и позиционных аргументов необходимо использовать правильный порядок следования параметров.

## Общее задание. Задача по отображению адресов электронной почты

### Отображение адресов электронной почты

Ваша задача - создать метод, который будет отображать правильный адрес электронной почты для внутренних и внешних сотрудников. Вам даны списки имен внутренних и внешних сотрудников. Адрес электронной почты сотрудника состоит из его имени пользователя и доменного имени компании.  

Формат имени пользователя - это первые два символа имени сотрудника, за которыми следует его фамилия. Например, сотрудник по имени «Роберт Бавин» будет иметь имя пользователя «robavin». Домен для внутренних сотрудников - «contoso.com».  

В этой задаче вам дается начальный код. Вы должны решить, как создать и вызвать метод для отображения адресов электронной почты.

### Задача кода: Добавьте метод для отображения адресов электронной почты

В коде, с которого вы начали, есть два массива для внутренних и внешних сотрудников. Помните, что домен для внутренних сотрудников - это «contoso.com», а имя пользователя для всех сотрудников - это первые два символа их имени, за которыми следует их полная фамилия.

Ваша задача - создать метод, который будет отображать адреса электронной почты внутренних и внешних сотрудников. Метод должен включать необязательный параметр для доменного имени внешних сотрудников.

1. Убедитесь, что в Visual Studio открыт пустой файл Program.cs.
2. Скопируйте и вставьте следующий код в редактор кода Visual Studio.
```cs
string[,] corporate = 
{
    {"Robert", "Bavin"}, {"Simon", "Bright"},
    {"Kim", "Sinclair"}, {"Aashrita", "Kamath"},
    {"Sarah", "Delucchi"}, {"Sinan", "Ali"}
};

string[,] external = 
{
    {"Vinnie", "Ashton"}, {"Cody", "Dysart"},
    {"Shay", "Lawrence"}, {"Daren", "Valdes"}
};

string externalDomain = "hayworth.com";

for (int i = 0; i < corporate.GetLength(0); i++) 
{
    // display internal email addresses
}

for (int i = 0; i < external.GetLength(0); i++) 
{
    // display external email addresses
}
```
3. Обновите код, чтобы использовать метод для отображения адресов электронной почты в соответствии со спецификациями задачи. Используйте полученные знания об использовании параметров и необязательных аргументов для завершения обновления.
4. Убедитесь, что ваш код выдает следующий результат:
```
robavin@contoso.com
sibright@contoso.com
kisinclair@contoso.com
aakamath@contoso.com
sadelucchi@contoso.com
siali@contoso.com
viashton@hayworth.com
codysart@hayworth.com
shlawrence@hayworth.com
davaldes@hayworth.com
```
## Заключение
Вашей целью было узнать больше об использовании параметров в методах и понять область видимости метода. Вы узнали о типах значений и ссылок и о том, как влияют на данные внутри метода. Вы также узнали, как использовать именованные и необязательные аргументы для расширения возможностей метода.