# Храните и итерируйте последовательности данных с помощью массивов и оператора foreach в C#.
Массивы C# позволяют хранить последовательности значений в одной структуре данных. Другими словами, представьте себе одну переменную, в которой может храниться множество значений. Если у вас есть одна переменная, в которой хранятся все значения, вы можете сортировать их, изменять порядок следования, перебирать каждое значение по отдельности и так далее.

Предположим, вы работаете в отделе безопасности компании, которая занимается поиском продавцов в Интернете и рекламодателей на основе комиссионных. Вас попросили написать код на C#, который будет итеративно просматривать идентификаторы заказов, поступающих в компанию. Вам нужно проверить каждый идентификатор заказа, чтобы выявить заказы, которые могут быть мошенническими. Для решения этой задачи вам понадобится использовать массивы.

В этом модуле вы создадите и инициализируете массивы. Вы будете устанавливать и извлекать значения из элементов массива, обращаясь к каждому элементу по его индексу. Вы создадите циклическую логику, которая позволит вам работать с каждым элементом массива.

К концу этого модуля вы создадите свою первую структуру для хранения нескольких значений данных. Позже, в других модулях, вы узнаете, как сортировать, фильтровать, запрашивать, агрегировать и выполнять другие операции с данными.

## Цели обучения
В этом модуле вы научитесь:

- Создавать и инициализировать новый массив.
- Присваивать и извлекать значения элементов массива.
- Итерация каждого элемента массива с помощью оператора foreach.

## Упражнение. Начало работы и основные действия с массивами

Массивы можно использовать для хранения нескольких значений одного типа в одной переменной. Значения, хранящиеся в массиве, как правило, связаны между собой. Например, список имен студентов можно хранить в строковом массиве с именем students.

Ваша работа в отделе безопасности направлена на поиск шаблона для мошеннических заказов. Вы хотите, чтобы ваш код просматривал прошлые заказы клиентов и выявлял маркеры, связанные с мошенническими заказами. Ваша компания надеется, что эти маркеры можно будет использовать для выявления потенциальных мошеннических заказов в будущем, прежде чем они будут обработаны. Поскольку вы не всегда знаете заранее, сколько заказов вам нужно просмотреть, вы не можете создать отдельные переменные для хранения каждого идентификатора заказа. Как создать структуру данных для хранения нескольких связанных значений?

В этом упражнении вы используете массивы для хранения и анализа коллекции идентификаторов заказов.

### Что такое массив?
Массив - это набор отдельных элементов данных, доступных через одно имя переменной. Для доступа к каждому элементу массива используется числовой индекс, основанный на нуле. Массивы позволяют создать коллекцию значений данных, имеющих общую цель или характеристики, под одним именем переменной для упрощения обработки.

### Объявление массивов и доступ к элементам массива
Массив - это особый тип переменной, которая может хранить несколько значений одного типа данных. Синтаксис объявления для массива немного отличается, потому что вам нужно указать и тип данных, и размер массива.

### Подготовьте среду разработки

#### Объявить новый массив
1. Чтобы объявить новый массив строк, который может содержать три элемента, введите следующий код:
```cs
string[] fraudulentOrderIDs = new string[3];
```
2. Уделите минуту изучению своего кода.

Оператор new создает в памяти компьютера новый экземпляр массива, который может содержать три строковых значения. Дополнительные сведения о ключевом слове new см. в модуле «Вызов методов из библиотеки классов .NET с помощью C#».

Обратите внимание, что первый набор квадратных скобок [] просто сообщает компилятору, что переменная с именем fraudulentOrderIDs - это массив, а второй набор квадратных скобок [3] указывает на количество элементов, которые может содержать массив.

:::note
В этом примере показано, как объявить массив строк, однако вы можете создать массив любого типа данных, включая такие примитивы, как int и bool, а также более сложные типы данных, такие как классы. В этом примере используется простота строк, чтобы свести к минимуму количество новых идей, которые необходимо усвоить в процессе работы.
:::

### Присвоение значений элементам массива
На данный момент вы объявили массив строк, но каждый элемент массива пуст. Чтобы получить доступ к элементу массива, вы используете числовой индекс, основанный на нуле, внутри квадратных скобок. Вы можете присвоить значение элементу массива с помощью символа =, как если бы это была обычная переменная.

1. Чтобы присвоить значения идентификаторов заказов массиву fraudulentOrderIDs, обновите код следующим образом:
```cs
string[] fraudulentOrderIDs = new string[3];

fraudulentOrderIDs[0] = "A123";
fraudulentOrderIDs[1] = "B456";
fraudulentOrderIDs[2] = "C789";
```
2. Уделите минуту изучению вашего кода.

Обратите внимание, что вы используете имя массива для доступа к его элементам. Доступ к каждому элементу осуществляется по отдельности путем указания нулевого номера индекса внутри квадратных скобок.

Поскольку ваш массив объявлен как строка, значения, которые вы присваиваете, также должны быть строками. В данном сценарии вы присваиваете элементам массива идентификаторы заказов.

### Попытка использовать индекс, выходящий за пределы массива.
Поначалу это может показаться интуитивно понятным, но важно помнить, что вы объявляете количество элементов в массиве. Однако вы обращаетесь к каждому элементу массива, начиная с нуля. Так, чтобы получить доступ ко второму элементу массива, вы используете индекс 1.

Начинающие пользователи часто забывают, что массивы основаны на нулях, и пытаются получить доступ к несуществующему элементу массива. Если вы допустите такую ошибку, возникнет исключение, сообщающее, что вы попытались получить доступ к элементу, находящемуся за пределами массива.

Чтобы намеренно «сломать» ваше приложение, попытайтесь получить доступ к четвертому элементу массива, используя значение индекса 3.

1. В нижней части файла кода введите следующую строку кода:
```cs
fraudulentOrderIDs[3] = "D000";
```
2. Убедитесь, что ваш код соответствует этому примеру:
```cs
string[] fraudulentOrderIDs = new string[3];

fraudulentOrderIDs[0] = "A123";
fraudulentOrderIDs[1] = "B456";
fraudulentOrderIDs[2] = "C789";
fraudulentOrderIDs[3] = "D000";
```
3. Запустите код используя консоль разработчика (если не отображается включите через меню View) используя команду dotnet build
Вы должны увидеть следующее сообщение:
```
Build succeeded.        
    0 Warning(s)        
    0 Error(s)
```
4. В командной строке терминала, чтобы запустить код, введите dotnet run и нажмите Enter.
5. При запуске приложения вы получаете следующее сообщение об ошибке:
```
Unhandled exception. System.IndexOutOfRangeException: Index was outside the bounds of the array.     
   at Program.<Main>$(String[] args) in C:\Users\someuser\Desktop\CsharpProjects\TestProject\Program.cs:line 6
```
Обратите внимание на следующие части ошибки:

Сообщение об ошибке: System.IndexOutOfRangeException: Индекс вышел за границы массива.
Место ошибки: Program.cs:строка 6
6. Закомментируйте строку, в которой возникла ошибка времени выполнения.
```cs
// fraudulentOrderIDs[3] = "D000";
```
Вы видели, как присвоить значение элементу массива. Теперь посмотрим, как получить доступ к значению, хранящемуся в элементе массива.

### Получить значения из элементов массива
Доступ к значению элемента массива работает так же, как присвоение значения элементу массива. Вы просто указываете индекс элемента, значение которого хотите получить.

1. Чтобы записать значение каждого мошеннического идентификатора заказа, обновите свой код следующим образом:
```cs
string[] fraudulentOrderIDs = new string[3];

fraudulentOrderIDs[0] = "A123";
fraudulentOrderIDs[1] = "B456";
fraudulentOrderIDs[2] = "C789";
// fraudulentOrderIDs[3] = "D000";

Console.WriteLine($"First: {fraudulentOrderIDs[0]}");
Console.WriteLine($"Second: {fraudulentOrderIDs[1]}");
Console.WriteLine($"Third: {fraudulentOrderIDs[2]}");
```
2. В командной строке терминала введите dotnet run и нажмите Enter.
3. Вы должны увидеть следующее сообщение:
```
First: A123
Second: B456
Third: C789
```
### Переназначить значение массива
Элементы массива аналогичны любому другому значению переменной. Вы можете присваивать, извлекать и переназначать значение каждому элементу массива.

1. В конце файла кода, чтобы переназначить и затем распечатать значение первого элемента массива, введите следующий код:
```cs
fraudulentOrderIDs[0] = "F000";

Console.WriteLine($"Reassign First: {fraudulentOrderIDs[0]}");
```
2. Убедитесь, что ваш код соответствует следующему примеру:
```cs
string[] fraudulentOrderIDs = new string[3];

fraudulentOrderIDs[0] = "A123";
fraudulentOrderIDs[1] = "B456";
fraudulentOrderIDs[2] = "C789";
// fraudulentOrderIDs[3] = "D000";

Console.WriteLine($"First: {fraudulentOrderIDs[0]}");
Console.WriteLine($"Second: {fraudulentOrderIDs[1]}");
Console.WriteLine($"Third: {fraudulentOrderIDs[2]}");

fraudulentOrderIDs[0] = "F000";

Console.WriteLine($"Reassign First: {fraudulentOrderIDs[0]}");
```
3. Запустите приложение

    Вы должны увидеть следующее сообщение:
    ```
    First: A123
    Second: B456
    Third: C789
    Reassign First: F000
    ```

### Инициализировать массив
Вы можете инициализировать массив во время объявления так же, как и обычную переменную.

1. Закомментируйте строки, в которых вы объявляете переменную FraudulentOrderIDs. 

Вы можете использовать многострочный комментарий (/* ... */), чтобы закомментировать объявление FraudulentOrderID и строки, используемые для присвоения значений элементам массива.

2. Чтобы объявить массив и инициализировать значения в одном операторе, введите следующий код:
```cs
string[] fraudulentOrderIDs = [ "A123", "B456", "C789" ];
```
В этом примере используется синтаксис выражения Collection, который был представлен в C# 12. Вы также можете увидеть более старый синтаксис, используемый для инициализации массива.

```cs
string[] fraudulentOrderIDs = { "A123", "B456", "C789" };
```

Обратите внимание, что этот старый синтаксис использует фигурные скобки \{ \} для заключения значений массива. Оба синтаксиса допустимы.
:::note
Вы можете увидеть комбинацию старого синтаксиса и синтаксиса выражения коллекции, используемого в этом обучении.
:::
3. Убедитесь, что ваш код соответствует следующему примеру:
```cs
/*
string[] fraudulentOrderIDs = new string[3];

fraudulentOrderIDs[0] = "A123";
fraudulentOrderIDs[1] = "B456";
fraudulentOrderIDs[2] = "C789";
// fraudulentOrderIDs[3] = "D000";
*/

string[] fraudulentOrderIDs = [ "A123", "B456", "C789" ];

Console.WriteLine($"First: {fraudulentOrderIDs[0]}");
Console.WriteLine($"Second: {fraudulentOrderIDs[1]}");
Console.WriteLine($"Third: {fraudulentOrderIDs[2]}");

fraudulentOrderIDs[0] = "F000";

Console.WriteLine($"Reassign First: {fraudulentOrderIDs[0]}");
```
4. Уделите минуту изучению оператора объявления.

Обратите внимание, что этот синтаксис компактен и легко читается. Когда вы запустите приложение, в выводе не должно произойти никаких изменений.

5. Запустите код
Вы должны увидеть то же сообщение, что и раньше:
```
First: A123
Second: B456
Third: C789
Reassign First: F000
```

### Используйте свойство Length массива
В зависимости от способа создания массива вы можете заранее не знать, сколько элементов содержит массив. Чтобы определить размер массива, вы можете использовать свойство Length.

:::note
Свойство длина массива не отсчитывается от нуля.
:::
1. Чтобы сообщить о количестве мошеннических заказов, в конце файла кода введите следующий код:
```cs
Console.WriteLine($"There are {fraudulentOrderIDs.Length} fraudulent orders to process.");
```
Этот код использует свойство Length массива, целое число, чтобы вернуть количество элементов в массиве fraudulentOrderIDs.
2. Убедитесь, что ваш код соответствует этому примеру:
```cs
/*
string[] fraudulentOrderIDs = new string[3];

fraudulentOrderIDs[0] = "A123";
fraudulentOrderIDs[1] = "B456";
fraudulentOrderIDs[2] = "C789";
// fraudulentOrderIDs[3] = "D000";
*/

string[] fraudulentOrderIDs = [ "A123", "B456", "C789" ];

Console.WriteLine($"First: {fraudulentOrderIDs[0]}");
Console.WriteLine($"Second: {fraudulentOrderIDs[1]}");
Console.WriteLine($"Third: {fraudulentOrderIDs[2]}");

fraudulentOrderIDs[0] = "F000";

Console.WriteLine($"Reassign First: {fraudulentOrderIDs[0]}");

Console.WriteLine($"There are {fraudulentOrderIDs.Length} fraudulent orders to process.");
```
3. Сохраните изменения в файле Program.cs, а затем запустите приложение.

Вы должны увидеть следующий результат:
```
First: A123
Second: B456
Third: C789
Reassign First: F000
There are 3 fraudulent orders to process.
```

### Обзор
Вот самое важное, что нужно помнить при работе с массивами:

- Массив - это специальная переменная, которая содержит коллекцию связанных элементов данных.
- Вы должны запомнить основной формат объявления переменной массива.
- Для доступа к каждому элементу массива, чтобы задать или получить его значение, используйте индекс, основанный на нуле, внутри квадратных скобок.
- Если вы попытаетесь получить доступ к индексу вне границ массива, вы получите исключение во время выполнения.
- Свойство Length дает возможность программно определить количество элементов в массиве.

## Упражнение. Реализация оператора foreach
Предположим, вы работаете в производственной компании. Компании необходимо провести инвентаризацию склада, чтобы определить количество продукции, готовой к отправке. Помимо общего количества готовой продукции, вам необходимо указать количество готовой продукции, хранящейся в каждом отдельном контейнере на вашем складе, а также текущий итог. Этот промежуточный итог будет использоваться для создания контрольного журнала, чтобы вы могли перепроверить свою работу и выявить «усадку».

### Перебор массива с помощью foreach
Оператор foreach обеспечивает простой и чистый способ итерации по элементам массива. Оператор foreach обрабатывает элементы массива в порядке возрастания индекса, начиная с индекса 0 и заканчивая индексом Length - 1. Он использует временную переменную для хранения значения элемента массива, связанного с текущей итерацией. При каждой итерации выполняется блок кода, расположенный под объявлением foreach.

Вот простой пример:
```cs
string[] names = { "Rowena", "Robin", "Bao" };
foreach (string name in names)
{
    Console.WriteLine(name);
}
```
Под ключевым словом foreach блок кода, содержащий Console.WriteLine(name);, будет выполняться один раз для каждого элемента массива имен. По мере того как среда выполнения .NET перебирает каждый элемент массива, значение, хранящееся в текущем элементе массива имен, присваивается временной переменной name для удобства доступа к ней внутри блока кода.

Если бы вы выполнили этот код, то увидели бы следующий результат.
```
Rowena
Robin
Bao
```
## С помощью оператора foreach создайте сумму всех товаров, имеющихся в наличии в каждой корзине вашего склада.

### Создайте и инициализируйте массив int
1. Чтобы создать массив типа int, хранящий количество готовых изделий в каждой корзине, введите следующий код:
```cs
int[] inventory = { 200, 450, 700, 175, 250 };
```
### Добавьте оператор foreach для перебора массива.

Чтобы создать оператор foreach, который перебирает каждый элемент массива inventory, введите следующий код:
```cs
foreach (int items in inventory)
{

}
```
Обратите внимание, что оператор foreach временно присваивает значение текущего элемента массива переменной int с именем items.

2. Убедитесь, что ваш код соответствует следующему:
```cs
int[] inventory = { 200, 450, 700, 175, 250 };

foreach (int items in inventory)
{

}
```
### Добавьте переменную для суммирования значений каждого элемента массива.
1. Поместите курсор на пустую строку кода над оператором foreach.
2. Чтобы объявить новую переменную, которая представляет сумму всей готовой продукции на вашем складе, введите следующий код:
```cs
int sum = 0;
```
Убедитесь, что вы объявили переменную вне оператора foreach.

3. Поместите курсор внутри блока кода оператора foreach.
   
4. Чтобы добавить текущее значение, хранящееся в Items, к переменной sum, введите следующий код:
```cs
sum += items;
```
5. Убедитесь что ваш код соответствует следующему:
```cs
int[] inventory = { 200, 450, 700, 175, 250 };
int sum = 0;
foreach (int items in inventory)
{
    sum += items;
}
```
### Отобразить окончательное значение суммы
1. Создайте пустую строку кода под блоком кода оператора foreach.
2. Чтобы сообщить окончательную сумму предметов в вашем инвентаре, введите следующий код:
```cs
Console.WriteLine($"We have {sum} items in inventory.");
```
3. Убедитесь, что ваш код соответствует следующему:
```cs
int[] inventory = { 200, 450, 700, 175, 250 };
int sum = 0;
foreach (int items in inventory)
{
    sum += items;
}

Console.WriteLine($"We have {sum} items in inventory.");
```
4. Запустите приложение.
```
We have 1775 items in inventory.
```

### Создайте переменную для хранения текущего номера ячейки и отображения промежуточной суммы.

Чтобы выполнить последнее требование проекта по созданию отчетов об инвентаризации, вам нужно создать переменную, которая будет хранить текущую итерацию оператора foreach, чтобы вы могли отобразить корзину и количество готовых предметов в этой корзине, а также общий итог всех предметов в корзинах, учтенных на данный момент.

1. Создайте пустую строку кода над оператором foreach.
2. Чтобы объявить переменную int с именем bin, инициализированную значением 0, введите следующий код:
```cs
int bin = 0;
```
Вы будете использовать bin для хранения номера ячейки, запасы которой в данный момент обрабатываются.
3. Внутри блока кода foreach, чтобы увеличивать bin при каждом выполнении блока кода, введите следующий код:
```cs
bin++;
```
Обратите внимание, что вы используете оператор ++ для увеличения значения переменной на 1. Это сокращение для bin = bin + 1.

4. Чтобы сообщить номер ячейки, количество готовой продукции в ячейке и общее количество готовой продукции, введите следующий код внутри блока кода foreach после bin++;:
```cs
Console.WriteLine($"Bin {bin} = {items} items (Running total: {sum})");
```
Этот код будет использовать вашу переменную-счетчик bin, временную переменную foreach items и вашу переменную sum, чтобы сообщить о текущем состоянии вашего инвентаря в красиво отформатированном сообщении.

5. Убедитесь, что ваш код соответствует следующему:
```cs
int[] inventory = { 200, 450, 700, 175, 250 };
int sum = 0;
int bin = 0;
foreach (int items in inventory)
{
    sum += items;
    bin++;
    Console.WriteLine($"Bin {bin} = {items} items (Running total: {sum})");
}
Console.WriteLine($"We have {sum} items in inventory.");
```
6. Сохраните изменения в файле Program.cs, а затем запустите приложение.

Вы должны увидеть следующий вывод:
```
Bin 1 = 200 items (Running total: 200)
Bin 2 = 450 items (Running total: 650)
Bin 3 = 700 items (Running total: 1350)
Bin 4 = 175 items (Running total: 1525)
Bin 5 = 250 items (Running total: 1775)
We have 1775 items in inventory.
```
### Подведение итогов
Вот несколько моментов, которые следует запомнить о операторах foreach и инкрементировании значений, которые вы узнали в этом разделе:

- Используйте оператор foreach для перебора каждого элемента массива, выполняя соответствующий блок кода один раз для каждого элемента массива.
- Оператор foreach устанавливает значение текущего элемента массива во временную переменную, которую можно использовать в теле блока кода.
- Используйте оператор инкремента ++, чтобы добавить 1 к текущему значению переменной.

## Упражнение. Выполните задание для вложенных операторов итерации и выбора.

### Проблема мошеннических заказов
Ранее в этом модуле вы задались целью написать код, который будет хранить идентификаторы заказов, принадлежащих потенциально мошенническим заказам. Ваша цель - найти мошеннические заказы как можно раньше и отметить их для более глубокого анализа.

### Сообщите идентификаторы заказов, которые требуют дальнейшего расследования
Ваша команда обнаружила закономерность. Заказы, начинающиеся с буквы «B», подвергаются мошенничеству в 25 раз чаще, чем обычно. Вы пишете новый код, который выводит идентификатор заказа для новых заказов, где идентификатор заказа начинается с буквы «B». Это будет использоваться командой мошенников для дальнейшего расследования.

Для решения этой задачи выполните следующие шаги.

1. Объявите массив и инициализируйте его, чтобы он содержал следующие элементы:
```
B123
C234
A345
C15
B177
G3003
C235
B179
```
Эти значения представляют собой мошеннические данные идентификатора заказа, которые использует ваше приложение.

2. Создайте оператор foreach для перебора каждого элемента массива.

3. Сообщите идентификаторы заказов, начинающиеся с буквы «B».

Необходимо оценить каждый элемент массива. Выявите потенциально мошеннические идентификаторы ордеров, обнаружив ордера, начинающиеся с буквы «B». Чтобы определить, начинается ли элемент с буквы «B», используйте метод String.StartsWith(). Вот простой пример использования метода String.StartsWith(), который вы можете адаптировать для своего кода:
```cs
string name = "Bob";
if (name.StartsWith("B"))
{
    Console.WriteLine("The name starts with 'B'!");
}
```
Ваш вывод должен соответствовать следующему:
```
B123
B177
B179
```
:::tip
По мере того как вы будете перебирать каждый элемент массива, вам понадобится оператор if. Оператор if должен использовать метод класса string, чтобы определить, начинается ли строка с определенной буквы. Если вы не знаете, как использовать оператор if, обратитесь к модулю «Добавление логики принятия решений в ваш код с помощью оператора if-elseif-else в C#».
:::
 
## Заключение
Ваша цель в этом модуле - программно работать с последовательностью идентификаторов заказов для выявления потенциально мошеннических заказов. Вы создали массив идентификаторов заказов, а затем провели итерацию по каждому элементу последовательности в поисках общих признаков мошенничества.

Массивы позволяют хранить каждый идентификатор заказа как элемент одной переменной. Вы обращались к определенному элементу массива с помощью индекса - числового значения, основанного на нуле. Вы могли извлекать и устанавливать значение каждого элемента. Вы итерировались по элементам массива, чтобы проверить или вывести значение каждого элемента.

Представьте, как сложно было бы работать со связанными данными в вашем коде, если бы у вас не было такой структуры, как массив? Вам пришлось бы заранее знать, с каким количеством элементов данных придется работать, и определять отдельную переменную для каждого значения. Это создало бы хрупкое решение.

При создании массивов их размер можно изменять в зависимости от объема данных, с которыми вам нужно работать. По мере того как вы будете знакомиться с массивами (и подобными структурами данных), вы будете часто использовать их в своих приложениях для обработки и управления данными.