# Создание методов C#, возвращающих значения

## Введение
Методы могут предоставлять возвращаемые значения после выполнения своих задач. Совместное использование параметров и возвращаемых типов позволяет создавать оптимизированные методы, которые получают входные данные, выполняют задачу и предоставляют выходные данные. Такой формат позволяет эффективно встраивать функциональность в программы, сохраняя чистый и читабельный код.  

Предположим, вам нужно создать приложение, которое использует множество методов для выполнения вычислений над входными значениями. Вам нужен способ получить результаты вычислений и использовать их во всей программе. Это можно сделать, создав методы с возвращаемыми значениями.  

Рассмотрим игру, в которой игрок должен сражаться с врагами. Игра содержит некоторый код, который определяет, был ли персонаж поражен при каждом вызове метода `Update()`. Код может содержать следующие методы:
```cs
void Update();

int[] GetEnemyCoordinates(string enemyId);
int[] GetDistanceFromHero(string enemyId);
int[] GetHeroCoordinates();

bool EnemyCanHitHero(string enemyId);
int GetEnemyDamageOutput(string enemyId);
void UpdateHeroHP(int damage);
```
Глядя на сигнатуры методов, вы можете представить, как входные и выходные данные каждого метода могут быть использованы в программе. Методы также делают код игры более надежным, поскольку каждый из них имеет возвращаемые значения, которые могут быть использованы в различных сценариях.  

Захват возвращаемых значений из методов невероятно полезен для самых разных приложений. В этом модуле вы узнаете больше о выполнении методов и работе с возвращаемыми типами методов.  

## Цели обучения 

В этом модуле вы узнаете:  

- Поймете, что такое типы возврата
- Узнаете больше о ключевом слове `return`
- Узнаете больше о захвате возвращаемых значений методов

## Понимание синтаксиса типов возврата

Методы могут не только выполнять операции, но и возвращать значение. Методы могут возвращать значение, включив тип возврата в сигнатуру метода. Методы могут возвращать любой тип данных или вообще ничего не возвращать. Тип возврата всегда должен быть указан перед именем метода.  

Использование `void` в качестве возвращаемого типа означает, что метод только выполняет операции и не возвращает значение. Например:

```cs
void PrintMessage(string message)
```
Когда используется тип данных (например, `int`, `string`, `bool` и т. д.), метод выполняет операции и по завершении возвращает указанный тип. Внутри метода для возврата результата используется ключевое слово `return`. В методах `void` вы также можете использовать ключевое слово `return` для завершения метода.  

В этом упражнении вы узнаете больше об использовании ключевого слова `return`.

### Используйте методы расчета общей стоимости покупки
В торговом центре Contoso проходит суперраспродажа! На многие товары действуют скидки. Вам дается список цен на товары и список соответствующих скидок. Скидки представлены в процентах, например 50% = 0,5. Если покупатель тратит больше 30,00, он получает 5,00 от общей суммы покупки. В этом задании вы напишете код для вычисления общей суммы покупки покупателя. Давайте начнем!

1. Введите следующий код в редактор кода Visual Studio:
```cs
double total = 0;
double minimumSpend = 30.00;

double[] items = {15.97, 3.50, 12.25, 22.99, 10.98};
double[] discounts = {0.30, 0.00, 0.10, 0.20, 0.50};

Console.WriteLine($"Total: ${total}");

void GetDiscountedPrice(int itemIndex)
{
    // Calculate the discounted price of the item
}

void TotalMeetsMinimum()
{
    // Check if the total meets the minimum
}

void FormatDecimal(double input)
{
    // Format the double so only 2 decimal places are displayed
}
```
На этом шаге вы задаете переменные, которые понадобятся вашей программе, и создаете методы-заместители, которые будут использоваться для выполнения задач, чтобы получить общую стоимость покупки.
2. Измените метод `GetDiscountedPrice` так, чтобы он возвращал `double` значение, изменив код на следующий:
```cs
double GetDiscountedPrice(int itemIndex)
{
    // Calculate the discounted price of the item
}
```
Обратите внимание, что этот метод выдает ошибку компиляции: не все пути кода возвращают значение. Метод с возвращаемым типом должен всегда возвращать значение этого типа. Давайте исправим эту ошибку.
3. Обновите метод `GetDiscountedPrice`, добавив следующий код:
```cs
double GetDiscountedPrice(int itemIndex)
{
    double result = items[itemIndex] * (1 - discounts[itemIndex]);
    return result;
}
```
Чтобы вернуть значение из метода, добавьте значение или выражение после ключевого слова `return`. Возвращаемое значение должно соответствовать типу данных, указанному в сигнатуре метода.  

В этом коде вы вычисляете цену товара со скидкой по адресу `itemIndex`, а затем возвращаете результат. Однако ключевое слово `return` не ограничивается возвратом переменных или литеральных значений. Давайте пропустим переменную и вернем выражение.

4. Обновите метод `GetDiscountedPrice`, добавив следующий код:
```cs
double GetDiscountedPrice(int itemIndex)
{
    return items[itemIndex] * (1 - discounts[itemIndex]);
}
```
Поскольку код `items[itemIndex] * (1 - discounts[itemIndex])` оценивается в `double` значение, этот оператор `return` корректен.

5. Измените метод `TotalMeetsMinimum` так, чтобы он возвращал значение `bool`, изменив свой код следующим образом:
```cs
bool TotalMeetsMinimum()
{
    return total >= minimumSpend;
}
```
В этом коде вы возвращаете результат сравнения, который оценивается как `bool`. Возврат выражений из методов - отличный способ сделать ваш код более упорядоченным и улучшить читаемость.

Измените метод `FormatDecimal` так, чтобы он возвращал `string`, изменив свой код следующим образом:

```cs
string FormatDecimal(double input)
{
    return input.ToString().Substring(0, 5);
}
```
Обратите внимание, что в выражении оператора `return` можно вызывать другие методы. При вызове этого метода управление выполнением сначала оценивает `input.ToString`, затем оценивает и возвращает значение подстроки. Гибкость ключевого слова `return` позволяет создавать короткие строки кода, наполненные функциональностью.

### Захват возвращаемых значений

Теперь, когда ваши методы возвращают значения, вы можете перехватить их и использовать в остальном коде. Использование результатов, возвращаемых методами, - отличный способ сохранить код структурированным и легко читаемым. Давайте потренируемся!

1. Найдите следующую строку кода в вашей программе:`Console.WriteLine($«Total: ${total}»);`
2. Обновите код до следующего вида:
```cs
for (int i = 0; i < items.Length; i++)
{
    total += GetDiscountedPrice(i);
}

Console.WriteLine($"Total: ${total}");
```
В этом коде вы используете цикл `for` для получения суммы всех цен на товары со скидкой. Поскольку `GetDiscountedPrice` возвращает `double` значение, вы можете использовать этот метод для инициализации или работы с любыми другими `double` переменными. В данном случае вы используете результат `GetDiscountedPrice` для увеличения `total`.

3. Введите новую пустую строку кода перед `Console.WriteLine`, а затем добавьте следующий код:
```cs
if (TotalMeetsMinimum())
{
    total -= 5.00;
}
```
Поскольку `TotalMeetsMinimum` возвращает значение `bool`, вы можете вызвать метод внутри условия `if`. Вы также можете использовать этот метод в троичном выражении следующим образом:  

`total -= TotalMeetsMinimum() ?` `5.00 : 0.00;`

4. Используйте `FormatDecimal` для форматирования отображаемой цены покупки, изменив код следующим образом:
```cs
Console.WriteLine($"Total: ${FormatDecimal(total)}");
```
Как и в предыдущем коде, `FormatDecimal` возвращает `строковое` значение. Поэтому вы можете вызвать метод вместо использования строковой переменной или литерала. В этом коде управление выполнением передается `FormatDecimal` для оценки результата перед вычислением `Console.WriteLine`.

### Проверьте свою работу 

1. Сравните свой код с приведенным ниже, чтобы убедиться в его правильности:
```cs
double total = 0;
double minimumSpend = 30.00;

double[] items = {15.97, 3.50, 12.25, 22.99, 10.98};
double[] discounts = {0.30, 0.00, 0.10, 0.20, 0.50};

for (int i = 0; i < items.Length; i++)
{
    total += GetDiscountedPrice(i);
}

total -= TotalMeetsMinimum() ? 5.00 : 0.00;

Console.WriteLine($"Total: ${FormatDecimal(total)}");

double GetDiscountedPrice(int itemIndex)
{
    return items[itemIndex] * (1 - discounts[itemIndex]);
}

bool TotalMeetsMinimum()
{
    return total >= minimumSpend;
}

string FormatDecimal(double input)
{
    return input.ToString().Substring(0, 5);
}
```
2. Убедитесь, что ваш код выдает следующий результат:
```
Total: $44.58
```
Если ваш код показывает другие результаты, вам нужно пересмотреть код, чтобы найти ошибку и внести обновления. Запустите код снова, чтобы проверить, устранили ли вы проблему. Продолжайте обновлять и запускать код до тех пор, пока он не даст ожидаемые результаты.

### Резюме
- Методы могут возвращать значение, указывая тип данных return, или `void`, если значение не возвращается.
- Ключевое слово `return` может использоваться с переменными, литералами и выражениями.
- Значение, возвращаемое методом, должно соответствовать указанному типу возвращаемых данных
- Данные, возвращаемые из методов, могут быть перехвачены и использованы вызывающей стороной метода

## Возвращайте числа из методов

Вам часто может понадобиться возвращать числа из методов и использовать результаты для решения других задач. В этом коротком упражнении вы потренируетесь возвращать данные типов `int` и `double` и перехватывать возвращаемые значения.

### Создайте метод, возвращающий целое число 

Предположим, вы посещаете Вьетнам и хотите создать короткую программу, которая конвертирует валюту. Вы можете предположить, что текущий обменный курс составляет `1 USD = 23500 VND`. В этом задании вы напишете метод, который конвертирует USD в VND.  

1. В редакторе кода Visual Studio удалите весь существующий код из предыдущих заданий.
2. Введите следующий код в редактор кода Visual Studio:
```cs
double usd = 23.73;
int vnd = UsdToVnd(usd);

Console.WriteLine($"${usd} USD = ${vnd} VND");

int UsdToVnd(double usd) 
{

}
```
В этом шаге вы инициализируете две переменные для хранения значений USD и VND. Обратите внимание, что `vnd` инициализируется результатом метода `UsdToVnd`. Метод возвращает целое значение, так как VND обычно представляется в виде целых чисел. Для отображения результатов конвертации валют используется `Console.WriteLine`.

3. Далее вы добавите код для выполнения преобразования. Обновите метод `UsdToVnd`, добавив следующий код:
```cs
int UsdToVnd(double usd) 
{
    int rate = 23500;
    return (int) (rate * usd);
}
```
Если опустить приведение из возвращаемого результата, вы увидите следующую ошибку:
```
Cannot implicitly convert type 'double' to 'int'.
```
Это происходит потому, что компилятор пытается привести возвращаемое значение к типу данных, указанному в сигнатуре метода. Однако неявное приведение доступно только тогда, когда в результате преобразования не происходит потери данных. Возвращаемое значение всегда должно соответствовать типу данных, указанному в сигнатуре метода, поэтому в этом случае необходимо привести результат.

4. Сравните результат
```
$23.73 USD = $557655 VND
```
Если ваш код выдает неожиданные результаты, вам нужно пересмотреть код, чтобы найти ошибку и внести изменения. Запустите код снова, чтобы проверить, устранили ли вы проблему. Продолжайте обновлять и запускать код до тех пор, пока он не даст ожидаемые результаты.

### Создайте метод, возвращающий `double` значение

Далее вы создадите метод для конвертации VND обратно в USD. 
1. Создайте новую пустую строку кода в конце метода `UsdToVnd`. 
2. Введите следующий код:
```cs
double VndToUsd(int vnd) 
{

}
```
3. Обновите метод `VndToUsd`, добавив следующий код:
```cs
double VndToUsd(int vnd) 
{
    double rate = 23500;
    return vnd / rate;
}
```
В этом случае необходимо, чтобы `rate` был `double`, иначе компилятор использует целочисленное деление и вернет усеченное значение `int`. USD должен быть представлен десятичным числом.  

Если вы зададите для `rate` значение `int`, а не `double`, то заметите, что компилятор не выдает никаких ошибок. Это происходит потому, что значение `vnd / rate` неявно приводится к типу данных `double`, указанному в сигнатуре метода. При создании методов, возвращающих числовые значения, важно учитывать типы данных в операциях, которые выполняет ваш метод.

4. Найдите вызов `Console.WriteLine` и добавьте новую пустую строку кода. Затем введите следующий код, чтобы вызвать наш новый метод и вывести результат:
```cs
Console.WriteLine($"${vnd} VND = ${VndToUsd(vnd)} USD");
```
### Проверьте свою работу 

1. Сравните свой код с приведенным ниже, чтобы убедиться в его правильности:
```cs
double usd = 23.73;
int vnd = UsdToVnd(usd);

Console.WriteLine($"${usd} USD = ${vnd} VND");
Console.WriteLine($"${vnd} VND = ${VndToUsd(vnd)} USD");

int UsdToVnd(double usd) 
{
    int rate = 23500;
    return (int) (rate * usd);
}

double VndToUsd(int vnd) 
{
    double rate = 23500;
    return vnd / rate;
}
```
2. Убедитесь, что ваш код выдает следующий результат:
```
$23.73 USD = $557655 VND
$557655 VND = $23.73 USD
```
## Возвращайте строки из методов

Вы часто сталкиваетесь с необходимостью написать метод, возвращающий строку. Например, вы можете захотеть получить строку из набора данных или каким-то образом изменить строку. В этом упражнении вы получите некоторый опыт работы со строками в методах, одновременно отрабатывая распространенный вопрос на собеседовании.

### Создайте метод, возвращающий строку

Предположим, вы кандидат на собеседование по кодированию. Интервьюер просит вас написать метод, возвращающий строку без использования `string.Reverse`. Подумайте немного о том, как вы можете решить эту задачу.  

Возможно, вы решили, что можно развернуть строку, начиная итерацию с конца строки. Вы можете использовать временную строку для хранения каждой буквы от конца к началу. Давайте начнем!  

1. В редакторе кода Visual Studio удалите весь существующий код из предыдущих упражнений.
2. Введите в редактор следующий код:
```cs
string ReverseWord(string word) 
{
    string result = "";

    return result;
}
```
3. Метод должен выполнять итерации по заданному слову и обновлять результат. Для этого обновите метод `ReverseWord` следующим кодом:
```cs
string ReverseWord(string word) 
{
    string result = "";
    for (int i = word.Length - 1; i >= 0; i--) 
    {
        result += word[i];
    }
    return result;
}
```
В этом блоке кода вы начинаете с конца слова, используя `word.Length - 1`. Из длины вычитается единица, поскольку индексы массива начинаются с нуля, и вы хотите избежать обращения к элементу, выходящему за границы. Затем вы добавляете букву с текущим индексом в строку `результата` и перемещаете индекс назад. Вы используете `i >= 0`, поскольку `i` обновляется после выполнения кода в цикле, и вы хотите быть уверены, что включаете нулевой индекс.

### Протестируйте свой код

При кодировании важно часто проверять свою работу. Нахождение и исправление ошибок на ранних этапах процесса кодирования позволит вам потратить больше времени на создание правильного кода, а не на отладку одной большой программы. Частая проверка своей работы - это навык, который также высоко ценится интервьюерами, проводящими собеседования по кодингу.

1. Введите новую пустую строку кода. Затем создайте текст для ввода и вызовите свой метод, введя следующий код над методом `ReverseWord`:
```cs
string input = "snake";

Console.WriteLine(input);
Console.WriteLine(ReverseWord(input));
```
2. Сравните полученный результат со следующим:
```
snake
ekans
```
Если ваш код выдает неожиданные результаты, вам нужно пересмотреть код, чтобы найти ошибку и внести изменения. Запустите код снова, чтобы проверить, устранили ли вы проблему. Продолжайте обновлять и запускать код до тех пор, пока он не даст ожидаемые результаты.

### Создайте метод обратного преобразования слов в предложении

Предположим, что интервьюер задает вам дополнительный вопрос. Вам нужно перевернуть каждое слово в заданном предложении, сохранив исходное положение каждого слова. Можно предположить, что каждое слово отделено пробелом. Например, «string return type» превратится в «gnirts nruter epyt». Подумайте, как вы можете выполнить это задание.

Если вы воспользуетесь методом, который вы написали в предыдущем задании, то поймете, что с его помощью можно изменить каждое слово в строке по отдельности. Вы можете создать новое предложение и добавлять каждое слово по мере его реверсирования. Давайте начнем!

1. Создайте новую пустую строку кода в конце текущей программы. Затем введите следующий код, чтобы создать новый метод:
```cs
string ReverseSentence(string input) 
{
    string result = "";

    return result;
}
```
2. Далее вы можете извлечь отдельные слова из строки с помощью `string.Split`. Обновите метод `ReverseSentence` до следующего вида:
```cs
string ReverseSentence(string input) 
{
    string result = "";
    string[] words = input.Split(" ");

    return result;
}
```
Теперь, когда у вас есть доступ к каждому отдельному слову в предложении, вы можете использовать метод `ReverseWord` для каждого слова и сохранить их в `result`.

3. Обновите метод `ReverseSentence` до следующего вида:
```cs
string ReverseSentence(string input) 
{
    string result = "";
    string[] words = input.Split(" ");

    foreach(string word in words) 
    {
        result += ReverseWord(word) + " ";
    }

    return result;
}
```
Обратите внимание, как можно вызвать метод `ReverseWord` внутри составного оператора присваивания. В этом коде возвращаемое значение перехватывается из `ReverseWord` и добавляется в `result`. Методы с возвращаемыми значениями можно использовать везде, где они нужны, если только тип данных соответствует требованиям.  

В этом коде каждое перевернутое слово добавляется к результату с добавлением пробела. Однако это оставляет лишний пробел в конце перевернутого предложения.

4. Удалить лишний пробел в конце можно с помощью метода `string.Trim`. Обновите метод до следующего кода:
```cs
string ReverseSentence(string input) 
{
    string result = "";
    string[] words = input.Split(" ");

    foreach(string word in words) 
    {
        result += ReverseWord(word) + " ";
    }

    return result.Trim();
}
```
Подумайте о возвращаемом результате этого метода. Метод может использовать другие методы во время выполнения и даже в операторе возврата, если типы данных совпадают.Теперь вы готовы вызвать свой метод!

5. Обновите текст `input` и оператор `Console.WriteLine` до следующих значений:
```cs
string input = "there are snakes at the zoo";

Console.WriteLine(input);
Console.WriteLine(ReverseSentence(input));
```
### Проверьте свою работу

1. Сравните свой код с приведенным ниже, чтобы убедиться в его правильности:
```cs
string input = "there are snakes at the zoo";

Console.WriteLine(input);
Console.WriteLine(ReverseSentence(input));

string ReverseSentence(string input) 
{
    string result = "";
    string[] words = input.Split(" ");
    foreach(string word in words) 
    {
        result += ReverseWord(word) + " ";
    }
    return result.Trim();
}

string ReverseWord(string word) 
{
    string result = "";
    for (int i = word.Length - 1; i >= 0; i--) 
    {
        result += word[i];
    }
    return result;
}
```
2. Убедитесь, что ваш код выдает следующий результат:
```
there are snakes at the zoo
ereht era sekans ta eht ooz
```

## Возвращение булевых значений из методов

Методы с булевым типом возврата могут быть простыми, но полезными для консолидации кода. Методы, возвращающие значения типа bool, можно вызывать для оценки вводимых данных в любом месте, в операторах if, при объявлении переменных и т. д. В этом упражнении вы получите некоторый опыт создания и использования методов с булевым типом возврата.

### Создайте метод, возвращающий булево значение

Предположим, вы - кандидат на собеседование по кодированию. Интервьюер просит вас проверить, являются ли несколько слов палиндромом. Слово является палиндромом, если оно читается одинаково наперед, так и задом наперед. Например, слово racecar - это палиндром. Давайте начнем!

1. В редакторе кода Visual Studio удалите весь существующий код из предыдущих упражнений. 
2. Введите в редактор следующий код:
```cs
string[] words = {"racecar" ,"talented", "deified", "tent", "tenet"};

Console.WriteLine("Is it a palindrome?");
foreach (string word in words) 
{
    Console.WriteLine($"{word}: {IsPalindrome(word)}");
}
```
Этот код создает несколько тестовых примеров и ссылается на метод `IsPalindrome`. Слова и вывод метода `IsPalindrome` печатаются в операторах `Console.WriteLine`.

3. Введите новую пустую строку кода и создайте метод bool, введя следующий код:
```cs
bool IsPalindrome(string word) 
{
    return true;
}
```
4. Подумайте, как проверить, является ли слово палиндромом.

Один из способов проверки - сравнить первую и последнюю буквы слова. Если они совпадают, то сравните вторую и предпоследнюю буквы слова. Если вы дошли до середины слова, значит, все буквы были сравнены и совпали. Если буквы не совпадают, значит, слово не является палиндромом.

5. Обновите метод `IsPalindrome`, добавив следующий код:
```cs
bool IsPalindrome(string word) 
{
    int start = 0;
    int end = word.Length - 1;

    while (start < end) 
    {
        if (word[start] != word[end]) 
        {
            return false;
        }
        start++;
        end--;
    }

    return true;
}
```
Обратите внимание на переменные `start` и `end`, указывающие на первый и последний символы в строке. Цикл прерывается, когда встречается середина слова; когда `start` и `end` указывают на один и тот же символ или пересекаются друг с другом. Указатели перемещаются внутрь при каждом совпадении. Если они не совпадают, метод завершается и возвращает `false`.  

Теперь ваш метод успешно проверяет, является ли слово палиндромом, и возвращает `true` или `false` соответственно.

### Проверьте свою работу

Убедитесь, что ваш код выдает следующий результат:

```
Is it a palindrome?
racecar: True
talented: False
deified: True
tent: False
tenet: True
```

## Возвращайте массивы из методов

При разработке приложений вам часто придется создавать и изменять наборы данных. Методы полезны для выполнения операций над данными, и они являются особенно мощными инструментами для создания самих наборов данных. Разработка методов для создания массивов, представляющих набор данных, помогает сохранить код многократно используемым, организованным и упрощенным. В этом упражнении вы попрактикуетесь в возврате массивов из методов.

### Найдите монеты, чтобы получить сдачу

Предположим, у вас есть несколько монет разного достоинства. Перед вами стоит задача найти две монеты, сумма которых равна заданному значению. В этом упражнении имеющиеся монеты представлены в целочисленном массиве. Вам нужно вернуть индексы двух монет в новый массив. Давайте начнем!

1. В редакторе кода Visual Studio удалите весь существующий код из предыдущих упражнений. 
2. Введите следующий код в редактор кода Visual Studio:
```cs
int[] TwoCoins(int[] coins, int target) 
{
    return  new int[0];
}
```
В случае, когда двух монет не найдено, ваш метод возвращает пустой массив. Обратите внимание на синтаксис возвращаемого результата. Хотя вы можете создать переменную для хранения нового массива `int[]` и вернуть переменную, оператор `return` позволяет одновременно создавать и возвращать значения.

3. Существует множество подходов к решению этой задачи. Подумайте, как можно найти в массиве два числа, сумма которых равна заданному значению. В этом упражнении будет использован следующий подход:
    1. Выберите одно число из массива.
    2. Проверьте другие числа по одному, чтобы узнать, не совпадают ли они с заданным значением.
    3. Верните результат, как только будет найдено совпадение.
4. Чтобы проверить каждое число в массиве, обновите метод `TwoCoins` с помощью следующего кода:
```cs
int[] TwoCoins(int[] coins, int target) 
{
    for (int curr = 0; curr < coins.Length; curr++) 
    {
        for (int next = curr + 1; next < coins.Length; next++) 
        {

        }
    }

    return  new int[0];
}
```
Здесь `curr` представляет собой один фиксированный индекс монеты, а `next` - последующие индексы монет. Вы попробуете сложить каждую `следующую` монету с фиксированной монетой `curr` и посмотреть, равны ли они целевому значению.

5. Далее добавьте логику для проверки суммы двух монет на соответствие целевому значению. Для этого обновите предыдущие циклы `for` следующим кодом:
```cs
for (int curr = 0; curr < coins.Length; curr++) 
{
    for (int next = curr + 1; next < coins.Length; next++) 
    {
        if (coins[curr] + coins[next] == target) 
        {
            return new int[]{curr, next};
        }

    }
}
```
В этом коде вы проверяете, равна ли сумма значений по адресам `curr` и `next` в массиве целевому значению. Если сумма равна, вы создаете массив для хранения этих индексов и возвращаете его. Если они не равны, вы можете проигнорировать их и продолжить проверку.

### Проверьте свое решение

1. Создайте новую пустую строку кода над подписью метода `TwoCoins`. Затем введите следующий код:
```cs
int target = 60;
int[] coins = new int[] {5, 5, 50, 25, 25, 10, 5};
int[] result = TwoCoins(coins, target);
```
Напомним, что метод `TwoCoins` возвращает пустой массив, если изменений не обнаружено. Вам нужно будет проверить размер массива, прежде чем пытаться вывести массив результатов.

2. Введите новую пустую строку кода. Затем введите следующий код:
```cs
if (result.Length == 0) 
{
    Console.WriteLine("No two coins make change");
} 
else 
{
    Console.WriteLine($"Change found at positions {result[0]} and {result[1]}");
}
```
4. Убедитесь что вывод соответствует:
```
Change found at positions 2 and 5
```
### Найдите несколько пар монет, которые дают сдачу

В этом шаге вы расширите метод `TwoCoins`, чтобы найти больше пар монет, сумма которых равна заданному значению. В этом упражнении вы найдете максимум пять пар. Это означает, что возвращаемый тип будет 2D-массив, а не 1D-массив, и вам нужно будет изменить способ, которым ваш код возвращает результаты. Давайте приступим!

1. Измените возвращаемый тип в сигнатуре метода с int[] на int[,], изменив свой код следующим образом:
```cs
int[,] TwoCoins(int[] coins, int target)
```
Далее вы создадите массив int[,] для хранения и возврата результатов, а также переменную counter для отслеживания количества пар, добавленных в массив.
2. Обновите метод `TwoCoins`, добавив следующий код:
```cs
int[,] TwoCoins(int[] coins, int target) 
{
    int[,] result = {{-1,-1},{-1,-1},{-1,-1},{-1,-1},{-1,-1}};
    int count = 0;
```
Обратите внимание, что вы инициализировали элементы массива result значением `-1`. Это поможет вам позже, когда вы захотите вывести найденные пары.  

Далее вы будете использовать массив `result` для хранения каждой найденной пары вместо того, чтобы возвращать первое совпадение.

3. Обновите метод `TwoCoins`, добавив следующий код:
```cs
int[,] TwoCoins(int[] coins, int target) 
{
    int[,] result = {{-1,-1},{-1,-1},{-1,-1},{-1,-1},{-1,-1}};
    int count = 0;

    for (int curr = 0; curr < coins.Length; curr++) 
    {
        for (int next = curr + 1; next < coins.Length; next++) 
        {
            if (coins[curr] + coins[next] == target) 
            {
                result[count, 0] = curr;
                result[count, 1] = next;
                count++;
            }

        }
    }
```
Обратите внимание, что `count` увеличивается каждый раз, когда в массив добавляется пара. Это может привести к ошибке index out of bounds, если найдено более пяти пар. Чтобы предотвратить эту ошибку, можно добавить код для проверки значения `count` и вернуть результат, когда массив `result` заполнен.

4. Обновите логику в методе `TwoCoins` с помощью следующего кода:
```cs
for (int next = curr + 1; next < coins.Length; next++) 
{
    if (coins[curr] + coins[next] == target) 
    {
        result[count, 0] = curr;
        result[count, 1] = next;
        count++;
    }
    if (count == result.GetLength(0)) 
    {
        return result;
    }
}
```
Наконец, вам нужно обновить финальный оператор `return`, чтобы он возвращал правильный результат, если не найдено ни одного совпадения, или если найдено менее пяти совпадений.
5. Перейдите к оператору `return `в методе `TwoCoins`. Измените оператор возврата так, чтобы он соответствовал следующему коду:
```cs
if (count == 0) 
{
    return new int[0,0];
}
return result;
```
Вы также можете сократить этот код возврата с помощью тернарного оператора, как показано ниже:
```cs
return (count == 0) ? new int[0,0] : result;
```
6. На этом этапе метод `TwoCoins` должен соответствовать следующему коду:
```cs
int[,] TwoCoins(int[] coins, int target) 
{
    int[,] result = {{-1,-1},{-1,-1},{-1,-1},{-1,-1},{-1,-1}};
    int count = 0;

    for (int curr = 0; curr < coins.Length; curr++) 
    {
        for (int next = curr + 1; next < coins.Length; next++) 
        {
            if (coins[curr] + coins[next] == target) 
            {
                result[count, 0] = curr;
                result[count, 1] = next;
                count++;
            }
            if (count == result.GetLength(0)) 
            {
                return result;
            }
        }
    }
    return (count == 0) ? new int[0,0] : result;
}
```

### Захватите новый возвращаемый массив

Теперь, когда ваш метод возвращает двумерный массив, вы можете обновить свой код для получения и печати результатов. Поскольку элементы массива результатов были инициализированы значением -1, можно добавить проверку, которая будет печатать все пары до тех пор, пока не будет найдено значение -1.

1. Перейдите в начало программы, где определена `target` переменная. Измените свой код следующим образом:
```cs
int target = 30;
int[] coins = new int[] {5, 5, 50, 25, 25, 10, 5};
int[,] result = TwoCoins(coins, target);
```
Далее вы обновите вызов Console.WriteLine, чтобы корректно выводить значения результатов.

2. Перейдите к вызову Console.WriteLine. Обновите свой код, чтобы он соответствовал следующему:
```cs
if (result.Length == 0) 
{
    Console.WriteLine("No two coins make change");
} 
else 
{
    Console.WriteLine("Change found at positions:");
    for (int i = 0; i < result.GetLength(0); i++) 
    {
        if (result[i,0] == -1) 
        {
            break;
        }
        Console.WriteLine($"{result[i,0]},{result[i,1]}");
    }
}
```
Здесь вы сохраняете проверку на пустой массив как есть и выводите значения двумерного массива в цикле for-loop. Когда найдено значение -1, вы выходите из цикла, поскольку следующих пар нет.

### Проверьте свою работу

1. Сравните свой код с приведенным ниже, чтобы убедиться в его правильности:
```cs
int target = 30;
int[] coins = new int[] {5, 5, 50, 25, 25, 10, 5};
int[,] result = TwoCoins(coins, target);

if (result.Length == 0) 
{
    Console.WriteLine("No two coins make change");
} 
else 
{
    Console.WriteLine("Change found at positions:");
    for (int i = 0; i < result.GetLength(0); i++) 
    {
        if (result[i,0] == -1) 
        {
            break;
        }
        Console.WriteLine($"{result[i,0]},{result[i,1]}");
    }
}

int[,] TwoCoins(int[] coins, int target) 
{
    int[,] result = {{-1,-1},{-1,-1},{-1,-1},{-1,-1},{-1,-1}};
    int count = 0;

    for (int curr = 0; curr < coins.Length; curr++) 
    {
        for (int next = curr + 1; next < coins.Length; next++) 
        {    
            if (coins[curr] + coins[next] == target) 
            {
                result[count, 0] = curr;
                result[count, 1] = next;
                count++;
            }
            if (count == result.GetLength(0)) 
            {
                return result;
            }
        }
    }
    return (count == 0) ? new int[0,0] : result;
}
```
2. Убедитесь, что ваш код выдает следующий результат
```
Change found at positions:
0,3
0,4
1,3
1,4
3,6
```
3. Затем обновите значение параметра target до значения 80
4. Чтобы убедиться, что ваш код работает так, как ожидалось, сравните результат работы вашего приложения со следующим результатом:
```
No two coins make change
```

## Общее задание. Добавить методы, позволяющие сделать игру играбельной

### Задача мини-игры с кубиками 

Ваша задача - разработать мини-игру. В игре должно быть выбрано целевое число, которое является случайным числом от одного до пяти (включительно). Игрок должен бросить шестигранную игральную кость. Чтобы выиграть, игрок должен выбросить число, превышающее целевое. В конце каждого раунда игрока нужно спросить, хочет ли он сыграть еще раз, и продолжить или завершить игру.  

В этой задаче вам дается стартовый код. Вы должны определить, какие методы нужно создать, их параметры и типы возврата.  

### Задача кода: добавьте методы, чтобы сделать игру играбельной

В коде, с которого вы начинаете, есть два недоступных метода:  

`ShouldPlay`: этот метод должен получать данные от пользователя и определять, хочет ли он играть снова `WinOrLose`: этот метод должен определять, выиграл игрок или проиграл.  

Также есть две неинициализированные переменные:  

`target`: Случайное целевое число от 1 до 5 `roll`: Результат случайного броска шестистороннего кубика.  

Ваша задача - создать методы `ShouldPlay` и `WinOrLose`, а также методы, которые устанавливают `target` и `roll` в случайные значения в нужном диапазоне. Когда все методы будут завершены, игра должна успешно запуститься.

1. Скопируйте и вставьте следующий код в панель редактора
```cs
Random random = new Random();

Console.WriteLine("Would you like to play? (Y/N)");
if (ShouldPlay()) 
{
    PlayGame();
}

void PlayGame() 
{
    var play = true;

    while (play) 
    {
        var target;
        var roll;

        Console.WriteLine($"Roll a number greater than {target} to win!");
        Console.WriteLine($"You rolled a {roll}");
        Console.WriteLine(WinOrLose());
        Console.WriteLine("\nPlay again? (Y/N)");

        play = ShouldPlay();
    }
}
```
2. Обновите код, чтобы использовать методы для запуска игры в соответствии со спецификациями задачи. Используйте то, что вы узнали о возвращаемых значениях и параметрах, чтобы завершить обновление.
3. Проверьте, что игра работает

Ваш код должен выдавать результаты, похожие на следующие:
```
Would you like to play? (Y/N)
Y
Roll a number greater than 1 to win!
You rolled a 2
You win!

Play again? (Y/N)
Y
Roll a number greater than 4 to win!
You rolled a 6
You win!

Play again? (Y/N)
Y
Roll a number greater than 1 to win!
You rolled a 1
You lose!

Play again? (Y/N)
N
```
## Заключение 
В этом модуле вы должны были понять, как ключевое слово return влияет на выполнение метода, и попрактиковаться в использовании различных выражений в операторах return. Вы также узнали, как перехватывать и использовать значения, возвращаемые методами. Вы даже получили опыт использования возвращаемых типов, отрабатывая некоторые распространенные вопросы на собеседовании по кодированию.