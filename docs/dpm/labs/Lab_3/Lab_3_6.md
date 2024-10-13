# Добавляйте в код логические циклы с помощью операторов do-while и while в C#.

## Введение

Как мы уже неоднократно говорили в предыдущих модулях, посвященных итерации и операторам принятия решений, существует несколько техник, которые можно использовать для достижения подобных результатов. Как и в письменном и разговорном языках, в языках программирования вы можете выразить одну и ту же мысль разными способами. При этом каждое выражение может иметь свои нюансы.

Операторы do-while и while позволяют управлять потоком выполнения кода, перебирая блоки кода до тех пор, пока не будет выполнено условие. При работе с оператором foreach мы выполняем итерацию по одному разу для каждого элемента в последовательности, например, массива. Оператор for позволяет выполнять итерацию заранее определенное количество раз и контролировать процесс итерации. Операторы do-while и while позволяют нам выполнять итерацию в блоке кода с таким расчетом, чтобы логика внутри блока кода влияла на то, когда мы можем прекратить итерацию.

Предположим, вы хотите принимать и обрабатывать пользовательский ввод. Вы хотите продолжать принимать и обрабатывать вводимые данные до тех пор, пока пользователь не нажмет клавишу q, означающую «выход». Вы можете использовать операторы do-while и while, чтобы продолжать итерации по логике приема пользовательского ввода и его обработки до тех пор, пока пользователь не будет готов остановиться.

В этом модуле вы будете использовать оператор do-while и оператор while для итерации блока кода. Вы поймете, когда следует предпочесть одно другому. Вы будете использовать оператор continue, чтобы пропустить обработку оставшейся части кода в блоке кода и перейти непосредственно к булевой оценке оператора while.

К концу этого модуля вы сможете уверенно использовать операторы do-while и while для добавления логики цикла в ваше приложение.

## Цели обучения
В этом модуле вы научитесь:

- Писать код, использующий оператор do-while для итерации блока кода.
- Писать код, использующий оператор while для итерации блока кода.
- Использовать оператор continue для перехода непосредственно к булевой оценке.

## Упражнение - Создание итерационных циклов do и while
На первый взгляд, операторы do-while и while - это еще один оператор итерации, который позволяет вам выполнять итерации в блоке кода и тем самым менять ход его выполнения. Однако, изучив принцип работы каждого из них, мы сможем лучше определить нюансы каждого оператора итерации и то, когда их следует использовать.

### Что такое оператор do-while?
Оператор do-while выполняет оператор или блок операторов, пока заданное булево выражение оценивается как true. Поскольку это выражение оценивается после каждого выполнения цикла, цикл do-while выполняется один или несколько раз.
```cs
do
{
    // This code executes at least one time
} while (true);
```
Поток выполнения начинается внутри фигурной скобки. Код выполняется хотя бы один раз, затем оценивается булево выражение, стоящее рядом с ключевым словом while. Если булево выражение возвращает true, блок кода выполняется снова.

Жестко закодировав булево выражение в true, мы создали бесконечный цикл - цикл, который никогда не закончится, по крайней мере, в том виде, в котором он написан сейчас. Нам понадобится способ выйти из цикла внутри блока кода. Критерии выхода из цикла do-while мы обсудим чуть позже.

Итак, давайте подготовим среду кодирования и приступим к изучению примеров кода, реализующих оператор do-while.

### Напишите оператор do-while, который прерывается при генерации определенного случайного числа

Давайте напишем код, который будет постоянно генерировать случайные числа от 1 до 10, пока не получим число 7. Это может занять всего одну итерацию, чтобы получить 7, или десятки итераций.

1. Создайте новый проект
2. Введите следующий код в редактор кода Visual Studio.
```cs
Random random = new Random();
int current = 0;

do
{
    current = random.Next(1, 11);
    Console.WriteLine(current);
} while (current != 7);
```
3. Сохраните и запустите код
4. Просмотрите свои результаты. Поскольку генерируемые числа случайны, ваши результаты будут отличаться. Однако значение 7 будет последним выведенным числом, так как булево выражение оценится как false, когда будет сгенерировано 7, и поток выполнения выйдет из блока кода.
```
2
5
8
2
7
```
5. Уделите минуту просмотру своего кода.

Ключевой урок для этой первой задачи заключается в том, что блок кода цикла do-while будет выполняться по крайней мере один раз. Он может выполняться большое количество раз, и вряд ли мы заранее знаем, сколько будет итераций.

Также важно заметить, что код внутри блока кода влияет на то, продолжать ли итерацию в этом блоке кода или нет. Блок кода, влияющий на критерии выхода, - это основная причина выбрать операторы do-while или while, а не один из других итерационных операторов. И foreach, и for опираются на внешние по отношению к блоку кода факторы для определения количества итераций блока кода.

### Напишите оператор while, который выполняет итерацию только в том случае, если случайное число больше некоторого значения
Теперь давайте посмотрим на оператор while.

1. С помощью редактора кода Visual Studio обновите код следующим образом:
```cs
Random random = new Random();
int current = random.Next(1, 11);

/*
do
{
    current = random.Next(1, 11);
    Console.WriteLine(current);
} while (current != 7);
*/

while (current >= 3)
{
    Console.WriteLine(current);
    current = random.Next(1, 11);
}
Console.WriteLine($"Last number: {current}");
```
:::note
В этом случае мы помещаем ключевое слово while и булево выражение перед блоком кода. Это меняет смысл кода и действует как "ворота", позволяя потоку выполнения войти только в том случае, если булево выражение оценивается как true.
:::

2. Сохраните файл с кодом, а затем используйте Visual Studio для выполнения кода
3. Просмотрите приведенные выходные значения. Поскольку числа случайны, ваш код будет выдавать другую последовательность.
```
9
7
5
Last number: 1
```
4. Уделите минуту просмотру вашего кода.

В верхней части кода мы используем random для инициализации нашей переменной int с именем current. Следующая активная строка кода - оператор while.

Оператор while будет выполнять итерацию на основе булевского выражения (current >= 3). Мы не знаем, какое значение будет присвоено переменной current, но существуют возможности, которые влияют на наш цикл while:

- Если current инициализируется значением, большим или равным 3, то булево выражение вернет true, и поток выполнения попадет в блок кода. Внутри блока кода первое, что мы сделаем, это запишем значение current в консоль. Далее, все еще внутри блока кода, мы обновляем значение current новым случайным значением. В этот момент управление возвращается в верхнюю часть оператора while, где происходит оценка булева выражения. Этот процесс продолжается до тех пор, пока булево выражение не вернет false и поток выполнения не прервется из блока кода.

- Если current инициализирован (в верхней части нашего кода) значением меньше 3, то булево выражение вернет false, и блок кода никогда не выполнится.

Последняя строка кода записывает значение current в консоль. Этот код выполняется независимо от того, был ли выполнен блок кода итерации или нет, и это наш шанс записать окончательное значение current в консоль.

### Используйте оператор continue, чтобы перейти непосредственно к булевому выражению

В некоторых случаях мы хотим сократить оставшуюся часть кода в блоке кода и перейти к следующей итерации. Это можно сделать с помощью оператора continue.

1. С помощью редактора кода Visual Studio обновите код следующим образом:
```cs
Random random = new Random();
int current = random.Next(1, 11);

do
{
    current = random.Next(1, 11);

    if (current >= 8) continue;

    Console.WriteLine(current);
} while (current != 7);

/*
while (current >= 3)
{
    Console.WriteLine(current);
    current = random.Next(1, 11);
}
Console.WriteLine($"Last number: {current}");
*/
```
2. Уделите минуту просмотру своего кода.

Обратите внимание, что мы снова перешли на do-while. Do-while гарантирует, что цикл выполнится хотя бы один раз.

Первое, что мы делаем внутри блока кода, - присваиваем новое случайное значение current. Далее мы проверяем, больше или равно ли current 8. Если это выражение вернется в true, ключевое слово continue передаст управление в конец блока кода, а while выполнит оценку (current != 7). Таким образом, цикл будет продолжать итерацию до тех пор, пока значение current не станет равным 7.

Ключом к этому шагу упражнения является строка кода, содержащая ключевое слово continue:
```cs
if (current >= 8) continue;
```
Поскольку наш код, который записывает значение current в консоль, расположен после if (current >= 8) continue;, наш код гарантирует, что значение current, которое больше или равно 8, никогда не будет записано в окно вывода.

Давайте попробуем это сделать.

3. Сохраните файл с кодом, а затем используйте Visual Studio для запуска кода.
4. Просмотрите перечисленные выходные значения.
```
5
1
6
7
```
Скорее всего, вы увидите результаты, отличные от тех, что показаны. Однако вы не увидите в окне вывода значений 8 или больше до того, как выполнение кода завершится значением 7.

5. Рассмотрим разницу между операторами continue и break.

Как вы видели на последнем шаге, оператор continue переносит выполнение в конец текущей итерации. Это поведение отличается от поведения, которое мы видели в операторе break. Оператор break завершает итерацию (или переключатель) и передает управление оператору, который следует за завершенным оператором. Если после прерванного оператора нет оператора, то управление передается в конец файла или метода.

### Подведение итогов
Из этого раздела вы должны вынести несколько важных идей:

- Оператор do-while выполняет итерацию в блоке кода по крайней мере один раз и может продолжать итерацию на основе булева выражения. Оценка булева выражения обычно зависит от некоторого значения, сгенерированного или полученного внутри блока кода.
- Оператор while сначала оценивает булево выражение и продолжает итерацию по блоку кода до тех пор, пока булево выражение оценивается как true.
- Ключевое слово continue позволяет сразу перейти к булеву выражению.

## Общее задание. Использование итерационных операторов do и while.

### Ролевая игра "Сражение"
В некоторых ролевых играх персонаж игрока сражается с неигровыми персонажами, которые обычно являются монстрами или «плохими парнями». Иногда сражение состоит в том, что каждый персонаж получает случайное значение с помощью кубиков, и это значение вычитается из показателя здоровья противника. Как только здоровье любого из персонажей достигает нуля, они проигрывают игру.

В этой задаче мы сведем это взаимодействие к его сути. Герой и монстр начинают игру с одинаковым показателем здоровья. Во время хода героя он генерирует случайное значение, которое вычитается из здоровья монстра. Если здоровье монстра больше нуля, он делает свой ход и атакует героя. Пока и у героя, и у монстра здоровье больше нуля, битва возобновляется.

### Написать код для реализации правил игры
Вот правила игры-битвы, которые вы должны реализовать в своем проекте:

- В качестве внешнего цикла игры вы должны использовать либо оператор do-while, либо оператор while.
- Герой и монстр начинают с 10 очками здоровья.
- Все атаки имеют значение от 1 до 10.
- Герой атакует первым.
- Выведите количество здоровья, которое потерял монстр, и его оставшееся здоровье.
- Если здоровье монстра больше 0, он может атаковать героя.
- Выведите количество здоровья, которое потерял герой, и его оставшееся здоровье.
- Продолжайте эту последовательность атак, пока здоровье монстра или героя не станет равным нулю или меньше.
- Выведите победителя.

1. Создайте новый проект
2. Напишите код игры, реализующий каждое правило.
3. Запустите приложение и убедитесь, что результат соответствует требованиям.
```
Монстр был поврежден и потерял 1 здоровье, а теперь имеет 9 здоровья
Герой был поврежден и потерял 1 здоровье, а теперь имеет 9 здоровья
Монстр был поврежден и потерял 7 здоровья, а теперь имеет 2 здоровья
Герой был поврежден и потерял 6 здоровья, а теперь имеет 3 здоровья
Монстр был поврежден и потерял 9 здоровья, а теперь имеет -7 здоровья
Герой победил!
```
Поскольку в коде используются случайные числа и результат каждый раз разный, ваши результаты будут отличаться от показанных выше. Однако вы можете использовать его в качестве примера вывода, который должен генерировать ваш код.

## Общее задание "Различия между итерационными операторами do и while".
### Изучите разницу между итерациями операторов do и while.
Как вы уже видели, C# поддерживает четыре типа операторов итерации: for, foreach, do-while и while. В справочной документации по языку Microsoft эти операторы описываются следующим образом:

- Оператор for: выполняет свое тело, пока заданное булево выражение («условие») оценивается как истинное.
- Оператор foreach: перечисляет элементы коллекции и выполняет свое тело для каждого элемента коллекции.
- Оператор do-while: условно выполняет свое тело один или несколько раз.
- Оператор while: условно выполняет свое тело ноль или более раз.

Итерации for и foreach, похоже, четко отличаются друг от друга, а также от итераций do-while и while. Однако определения операторов do-while и while кажутся совершенно одинаковыми. Понимание того, когда нужно выбирать между do-while и while, кажется более произвольным и может даже немного запутать. Некоторые проблемные проекты могут помочь прояснить различия.

В этой задаче вам будут предложены условия для трех отдельных проектов. В каждом проекте вам нужно будет реализовать блок итерационного кода, используя либо оператор do-while, либо оператор while. Чтобы сделать выбор между операторами do-while и while, вам нужно будет оценить заданные условия. Вы можете поменять их после начала работы, если ваш первый выбор окажется не таким удачным, как вы рассчитывали.

:::note
Условия для вашего проекта можно использовать для выбора между операторами do-while и while. То, что вы знаете или не знаете о булевом выражении, которое будет оцениваться, иногда может помочь вам выбрать между операторами do-while и while. В этом задании условия проекта включают информацию, которая будет использоваться для построения булева выражения.
:::
### Управляйте вводом данных пользователем во время выполнения этой задачи
При использовании оператора Console.ReadLine() для получения пользовательского ввода принято использовать для входной переменной строку с нулевым типом (обозначенную как string?), а затем оценивать введенное пользователем значение. В следующем примере кода для получения пользовательского ввода используется строка с зануляемым типом. Итерация продолжается, пока введенное пользователем значение равно null:
```cs
string? readResult;
Console.WriteLine("Enter a string:");
do
{
    readResult = Console.ReadLine();
} while (readResult == null);
```
Булево выражение, оцениваемое оператором while, можно использовать для проверки соответствия вводимых пользователем данных определенным требованиям. Например, если подсказка просит пользователя ввести строку, содержащую не менее трех символов, можно использовать следующий код:
```cs
string? readResult;
bool validEntry = false;
Console.WriteLine("Enter a string containing at least three characters:");
do
{
    readResult = Console.ReadLine();
    if (readResult != null)
    {
        if (readResult.Length >= 3)
        {
            validEntry = true;
        }
        else
        {
            Console.WriteLine("Your input is invalid, please try again.");
        }
    }
} while (validEntry == false);
```
Если вы хотите использовать Console.ReadLine() для ввода числовых значений, вам необходимо преобразовать строковое значение к числовому типу.

Для преобразования строкового значения в целое можно использовать метод int.TryParse(). Метод использует два параметра: строку, которая будет оцениваться, и имя целочисленной переменной, которой будет присвоено значение. Метод возвращает булево значение. Следующий пример кода демонстрирует использование метода int.TryParse():
```cs
// capture user input in a string variable named readResult

int numericValue = 0;
bool validNumber = false;

validNumber = int.TryParse(readResult, out numericValue);
```
Если строковое значение, присвоенное readResult, представляет собой действительное целое число, оно будет присвоено целочисленной переменной с именем numericValue, а булевой переменной с именем validNumber будет присвоено значение true. Если значение, присвоенное readResult, не является действительным целым числом, то переменной validNumber будет присвоено значение false. Например, если readResult равен «7», числовой переменной numericValue будет присвоено значение 7.

#### Проект 1 - напишите код, который проверяет целочисленный ввод
Вот условия, которые должен выполнить ваш первый проект:

- Ваше решение должно включать итерацию do-while или while.

- Перед блоком итерации: ваше решение должно использовать оператор Console.WriteLine(), чтобы предложить пользователю ввести целое значение от 5 до 10.

- Внутри блока итерации:

    - Ваше решение должно использовать оператор Console.ReadLine() для получения ввода от пользователя.
    - Ваше решение должно убедиться, что вводимые данные являются правильным представлением целого числа.
    - Если целое значение не находится в диапазоне от 5 до 10, ваш код должен использовать оператор Console.WriteLine(), чтобы запросить у пользователя целое значение в диапазоне от 5 до 10.
    - Перед выходом из итерации ваше решение должно убедиться, что целое значение находится в диапазоне от 5 до 10.
- Ниже (после) блока кода итерации: ваше решение должно использовать оператор Console.WriteLine(), чтобы сообщить пользователю, что его входное значение было принято.

1. Создайте новый проект
2. Реализуйте код выполняющий выше описанные условия
3. Запустите приложение и убедитесь, что ваш код проверяет правильность ввода данных пользователем в соответствии с указанными требованиями. 

Например, при запуске приложения оно должно отклонить такие значения, как "два" и "2", но принять значение "7". 

В описанном выше примере вывод консоли должен выглядеть следующим образом:
```
Введите целое число от 5 до 10 
два 
Извините, вы ввели неверное число, попробуйте еще раз 
2 
Вы ввели 2. 
Пожалуйста, введите число от 5 до 10. 
7 
Ваше значение (7) было принято.
```

#### Проект 2 - напишите код, который проверяет правильность ввода строки
Вот условия, которые должен выполнить ваш второй проект:

- Ваше решение должно включать итерацию do-while или while.

- Перед блоком итерации: ваше решение должно использовать оператор Console.WriteLine(), чтобы предложить пользователю ввести одно из трех имен ролей: Администратор, Менеджер или Пользователь.

- Внутри блока итерации:

  - Ваше решение должно использовать оператор Console.ReadLine() для получения ввода от пользователя.
  - Ваше решение должно убедиться, что введенное значение соответствует одному из трех вариантов роли.
  - Ваше решение должно использовать метод Trim() для входного значения, чтобы игнорировать ведущие и завершающие символы пробела.
  - Ваше решение должно использовать метод ToLower() для входного значения, чтобы игнорировать регистр.
  - Если введенное значение не совпадает ни с одним из вариантов роли, ваш код должен использовать оператор Console.WriteLine(), чтобы предложить пользователю ввести правильное значение.
- Ниже (после) блока кода итерации: Ваше решение должно использовать оператор Console.WriteLine(), чтобы сообщить пользователю, что введенное им значение было принято.

1. Закомментируйте код проекта 1
2. Реализуйте код выполняющий выше описанные условия
3. Запустите приложение и убедитесь, что ваш код проверяет правильность ввода данных пользователем в соответствии с указанными требованиями. 
Например, при запуске приложения оно должно отклонить входное значение типа "Admin", но принять входное значение " administrator ". Вывод консоли для этого примера должен выглядеть следующим образом:
```
Enter your role name (Administrator, Manager, or User)
Admin
The role name that you entered, "Admin" is not valid. Enter your role name (Administrator, Manager, or User)
   Administrator
Your input value (Administrator) has been accepted.
```
#### Проект 3 - Напишите код, который обрабатывает содержимое массива строк
Вот условия, которые должен выполнить ваш третий проект кодирования: 
- ваше решение должно использовать следующий массив строк для представления входных данных для вашей логики кодирования:
```cs
string[] myStrings = new string[2] { "I like pizza. I like roast chicken. I like salad", "I like all three of the menu choices" };
```
- В вашем решении должна быть объявлена целочисленная переменная periodLocation, которая будет использоваться для хранения местоположения символа точки в строке.

- Ваше решение должно включать внешний цикл foreach или for, который будет использоваться для обработки каждого элемента строки в массиве. Строковая переменная, которую вы будете обрабатывать в цикле, должна иметь имя myString.

- Во внешнем цикле ваше решение должно использовать метод IndexOf() класса String для получения местоположения первого символа точки в переменной myString. Вызов метода должен выглядеть примерно так: myString.IndexOf(«.»). Если в строке нет символа точки, будет возвращено значение -1.

- Ваше решение должно включать внутренний цикл do-while или while, который может быть использован для обработки переменной myString.

- Во внутреннем цикле ваше решение должно извлекать и выводить на экран (записывать в консоль) каждое предложение, содержащееся в каждой из обрабатываемых строк.

- Во внутреннем цикле ваше решение не должно отображать символ точки.

- Для обработки строковой информации во внутреннем цикле используйте методы Remove(), Substring() и TrimStart().

1. Закомментируйте код проекта 2
2. Реализуйте код выполняющий выше описанные условия
3. Запустите приложение и убедитесь, что результат соответствует требованиям.
Если логика кода работает правильно, вывод должен выглядеть следующим образом:
```
I like pizza
I like roast chicken
I like salad
I like all three of the menu choices
```
## Заключение
Ваша цель заключалась в использовании операторов do-while и while для выполнения итераций. Операторы do-while и while уникальны тем, что тело блока кода определяет, должен ли поток выполнения продолжаться или останавливаться.

Используя оператор do-while, вы выполняете блок кода один раз, прежде чем оценить булево выражение и потенциально завершить итерацию. Используя оператор while, вы выполнили оценку булева выражения немедленно и продолжили ее, чтобы выйти из итерации. Вы использовали оператор continue в блоке кода, чтобы перейти непосредственно к булеву выражению.

Вы разработали практическое приложение, использующее операторы do-while и continue для моделирования сражения в ролевой игре. Реальные сценарии с использованием операторов do-while и while включают работу с потоками данных из файлов, из Интернета или любые другие сценарии, в которых вы будете продолжать выполнять итерацию до тех пор, пока не будет выполнено условие.

Без операторов do-while и while было бы сложно писать и поддерживать код итерации, который устанавливает условие выхода внутри блока кода итерации.

