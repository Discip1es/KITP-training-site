# Выберите правильный тип данных в коде C#.

## Введение
Язык программирования C# в значительной степени опирается на типы данных. Типы данных ограничивают типы значений, которые могут храниться в данной переменной, что может быть полезно при создании безошибочного кода. Как разработчик, вы можете с уверенностью выполнять операции с переменными, поскольку заранее знаете, что в них хранятся только допустимые значения.

Предположим, вам предстоит создать новое приложение, которое должно получать, обрабатывать и хранить множество различных типов данных, включая отдельные числовые значения и последовательности числовых и текстовых значений. Выбор правильных типов данных имеет решающее значение для успеха ваших усилий по разработке программного обеспечения. Но каковы ваши возможности и какие критерии следует использовать, когда вы сталкиваетесь с несколькими типами данных, которые кажутся похожими?

В этом модуле вы узнаете, как ваше приложение хранит и обрабатывает данные. Вы узнаете, что существует два вида типов данных, которые соответствуют двум способам обработки данных. Вы напишете код, определяющий максимальные и минимальные значения, которые можно хранить в определенном числовом типе данных. Кроме того, вы узнаете, какие критерии следует использовать при выборе между несколькими числовыми типами данных для вашего приложения.

К концу этого модуля вы будете уверены в себе при работе с различными типами данных в C# и сможете выбрать правильный тип данных для конкретного приложения.

## Цели обучения 
В этом модуле вы узнаете: 
- фундаментальные различия между типами значений и ссылочными типами. 
- опишите свойства многих новых числовых типов данных, включая новые интегральные типы и типы с плавающей точкой. 
- напишите код, возвращающий максимальные и минимальные значения, которые могут хранить числовые типы данных. 
- используйте ключевое слово new для создания новых экземпляров ссылочного типа. 
- определите, какой тип данных следует выбрать для конкретного приложения.

## Откройте для себя типы значений и ссылочные типы

Поскольку в C# доступно множество типов данных, выбор правильного из них означает, что вам нужно понять, когда вы можете предпочесть один тип данных другому. 

Прежде чем обсуждать, почему вы можете предпочесть один тип данных другому, вам нужно больше узнать о типах данных. Вам также нужно знать, как данные и типы данных работают в C# и .NET.

### Что такое данные?
Ответ на вопрос «что такое данные» зависит от того, кого вы спрашиваете, и в каком контексте вы его задаете.

При разработке программного обеспечения данные - это, по сути, значение, которое хранится в памяти компьютера в виде серии битов. Бит - это простой двоичный переключатель, представленный в виде 0 или 1, или, скорее, «выключено» и «включено». Одиночный бит не кажется полезным, однако если объединить 8 битов в последовательность, они образуют байт. При использовании байта каждый бит приобретает определенное значение в последовательности. На самом деле, используя двоичную систему счисления (основание-2), вы можете представить 256 различных комбинаций с помощью всего 8 бит.

Например, в двоичной системе счисления число 195 можно представить как 11000011. Следующая таблица поможет вам представить, как это работает. В первой строке восемь столбцов, которые соответствуют позиции в байте. Каждая позиция представляет собой отдельное числовое значение. Вторая строка может хранить значение отдельного бита - 0 или 1.

| 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1   | 1   | 0   | 0   | 0   | 0   | 1   | 1   |

Если сложить числа из каждого столбца первой строки, которым соответствует 1 во второй строке, то получится десятичный эквивалент представления двоичной системы счисления. В данном случае это будет 128 + 64 + 2 + 1 = 195.

Чтобы работать с большими значениями, чем 255, ваш компьютер хранит больше байт (обычно 32- или 64-битных). Если вы работаете с миллионами больших чисел в научной среде, вам, возможно, придется более тщательно выбирать типы данных, которые вы используете. Для выполнения вашего кода может потребоваться больше памяти.

### А как насчет текстовых данных?
Если компьютер понимает только 0 и 1, то как он позволяет работать с текстом? Используя такую систему, как ASCII (American Standard Code for Information Interchange), вы можете использовать один байт для представления заглавных и строчных букв, цифр, табуляции, пробела, новой строки и многих математических символов.

Например, если бы вы хотели сохранить строчную букву a в качестве значения в моем приложении, компьютер понял бы только двоичную форму этого значения. Чтобы лучше понять, как строчная буква a обрабатывается компьютером, мне нужно найти таблицу ASCII, в которой представлены значения ASCII и их десятичные эквиваленты. Вы можете найти такой ресурс в Интернете по запросу «ASCII lookup decimal».

В данном случае строчная буква a эквивалентна десятичному значению 97. Затем вы можете использовать ту же двоичную систему счисления в обратном порядке, чтобы найти, как буква ASCII a хранится в компьютере.

| 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 0   | 1   | 1   | 0   | 0   | 0   | 0   | 1   |

Поскольку 64 + 32 + 1 = 97, 8-битный двоичный код ASCII для a будет 01100001. 

Скорее всего, вам никогда не придется самостоятельно выполнять подобные преобразования, но понимание того, как компьютер воспринимает данные, является основополагающей концепцией, особенно при изучении типов данных.

### Что такое тип данных? 
Тип данных - это способ, с помощью которого язык программирования определяет, сколько памяти нужно сохранить для значения. В языке C# существует множество типов данных, которые можно использовать для различных приложений и размеров данных. Для большинства приложений, которые вы будете создавать в своей карьере, вы остановитесь на небольшом подмножестве всех доступных типов данных. Однако все равно важно знать, какие типы существуют и почему.

### Значения и ссылочные типы
В этом модуле рассматриваются два вида типов в C#: ссылочные типы и типы значений. 

Переменные ссылочных типов хранят ссылки на свои данные (объекты), то есть они указывают на значения данных, хранящиеся где-то еще. В отличие от этого, переменные типов значений непосредственно содержат свои данные. По мере изучения C# появляются новые подробности, связанные с фундаментальным различием между типами значений и ссылок.

### Простые типы значений

Простые типы значений - это набор предопределенных типов, предоставляемых C# в виде ключевых слов. Эти ключевые слова являются псевдонимами (псевдонимами) для предопределенных типов, определенных в библиотеке классов .NET. Например, ключевое слово int в C# является псевдонимом типа значения, определенного в библиотеке классов .NET как System.Int32. 

К простым типам значений относятся многие типы данных, которые вы, возможно, уже использовали, например char и bool. Также существует множество интегральных типов и типов значений с плавающей точкой для представления широкого спектра целых и дробных чисел.

### Выводы
- Значения хранятся в виде битов, которые представляют собой простые переключатели "вкл/выкл". Комбинируя достаточное количество таких переключателей, можно хранить практически любые возможные значения. - Существует две основные категории типов данных: типы значений и ссылочные типы. Разница заключается в том, как и где значения хранятся компьютером во время выполнения вашей программы. 
- Простые типы значений используют ключевое слово псевдоним для представления формальных имен типов в библиотеке .NET.

## Откройте для себя интегральные типы

В этом упражнении вы работаете с интегральными типами. Интегральный тип - это простой тип значений, который представляет целые числа без дробей (например, -1, 0, 1, 2, 3). Самым популярным в этой категории является тип данных int.

Существует две подкатегории интегральных типов: знаковые и беззнаковые интегральные типы.

Знаковый тип использует свои байты для представления равного количества положительных и отрицательных чисел. В следующем упражнении вы познакомитесь со знаковыми интегральными типами в C#.

### Используйте свойства MinValue и MaxValue для каждого типа знаковых интегралов.
1. Убедитесь, что у вас открыт Visual Studio и на панели редактора отображается файл Program.cs. Program.cs должен быть пустым. Если это не так, выделите и удалите все строки кода. 
2. Чтобы увидеть диапазоны значений для различных типов данных, введите следующий код в редакторе кода Visual Studio.
```cs
Console.WriteLine("Signed integral types:");

Console.WriteLine($"sbyte  : {sbyte.MinValue} to {sbyte.MaxValue}");
Console.WriteLine($"short  : {short.MinValue} to {short.MaxValue}");
Console.WriteLine($"int    : {int.MinValue} to {int.MaxValue}");
Console.WriteLine($"long   : {long.MinValue} to {long.MaxValue}");
```
3. Запустите приложение. вы должны увидеть следующий результат
```
Signed integral types:
sbyte  : -128 to 127
short  : -32768 to 32767
int    : -2147483648 to 2147483647
long   : -9223372036854775808 to 9223372036854775807
```
Для большинства ненаучных приложений вам, скорее всего, понадобится работать только с int. В большинстве случаев вам не понадобится больше, чем от положительного до отрицательного значения 2,14 миллиарда целых чисел.

### Беззнаковые интегральные типы
Тип unsigned использует свои байты для представления только положительных чисел. В оставшейся части упражнения мы познакомимся с беззнаковыми интегральными типами в C#.

### Используйте свойства MinValue и MaxValue для каждого беззнакового интегрального типа

1. Ниже предыдущего фрагмента кода добавьте следующий код:
```cs
Console.WriteLine("");
Console.WriteLine("Unsigned integral types:");

Console.WriteLine($"byte   : {byte.MinValue} to {byte.MaxValue}");
Console.WriteLine($"ushort : {ushort.MinValue} to {ushort.MaxValue}");
Console.WriteLine($"uint   : {uint.MinValue} to {uint.MaxValue}");
Console.WriteLine($"ulong  : {ulong.MinValue} to {ulong.MaxValue}");
```
2. Сохраните и запустите код. вы должны увидеть
```Output
Signed integral types:
sbyte  : -128 to 127
short  : -32768 to 32767
int    : -2147483648 to 2147483647
long   : -9223372036854775808 to 9223372036854775807

Unsigned integral types:
byte   : 0 to 255
ushort : 0 to 65535
uint   : 0 to 4294967295
ulong  : 0 to 18446744073709551615
```
Хотя данный тип данных может использоваться во многих случаях, учитывая тот факт, что тип данных "байт" может представлять значение от 0 до 255, очевидно, что он предназначен для хранения значения, которое представляет собой байт данных. Данные, хранящиеся в файлах, или данные, передаваемые через Интернет, часто имеют двоичный формат. При работе с данными из таких внешних источников вам необходимо получать данные в виде массива байтов, а затем преобразовывать их в строки. Многие методы библиотеки классов .NET, связанные с кодированием и декодированием данных, требуют работы с массивами байтов.

### Выводы
- Интегральный тип - это простой тип данных, который может хранить целые числа. 
- Существуют знаковые и беззнаковые числовые типы данных. В знаковых интегральных типах используется 1 бит для хранения положительного или отрицательного значения. 
- Вы можете использовать свойства MaxValue и MinValue числовых типов данных, чтобы оценить, может ли число поместиться в заданный тип данных.

## Знакомство с типами с плавающей точкой

В этом упражнении вы работаете с типами данных с плавающей точкой, чтобы узнать о тонких различиях между каждым типом данных.

Плавающая точка - это простой тип данных, который представляет числа справа от десятичного знака. В отличие от целых чисел, существуют и другие соображения, помимо максимальных и минимальных значений, которые можно хранить в данном типе данных с плавающей точкой.

### Оценка типов с плавающей точкой
Во-первых, необходимо учитывать, какую точность допускает каждый тип. Точность - это количество разрядов, сохраняемых после десятичной точки.

Во-вторых, необходимо учитывать способ хранения значений и его влияние на точность. Например, значения `float` и `double` хранятся в двоичном формате (основание 2), а десятичные значения - в десятичном формате (основание 10). Почему это важно?

Выполнение математических операций с двоичными значениями с плавающей точкой может привести к результатам, которые могут вас удивить, если вы привыкли к десятичной математике (основание 10). Часто двоичная математика с плавающей точкой является приближением к реальному значению. Поэтому `float` и `double` полезны тем, что большие числа можно хранить в небольшом объеме памяти. Однако `float` и `double` следует использовать только в тех случаях, когда приближение полезно. Например, при расчете брызг от снежка в видеоигре достаточно приблизиться на несколько тысячных.

Если вам нужен более точный ответ, используйте `decimal`. Каждое значение типа `decimal` занимает относительно много памяти, однако при выполнении математических операций оно дает более точный результат. Поэтому при работе с финансовыми данными или в любом другом сценарии, где вам нужен точный результат вычислений, следует использовать десятичную систему счисления.

### Используйте свойства MinValue и MaxValue для каждого типа подписанных плавающих значений.



