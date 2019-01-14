Домашнее задание к занятию 4.2. Коллекции. Очередь.
==

## Задача 2. Польская запись.
### Описание

Задача написать программу перевода инфиксной записи (например 2 + 3) в постфиксную запись (2 3 +) что и будет являться так называемой
"Обратной польской записью". Обра́тная по́льская запись (англ. Reverse Polish notation, RPN) — форма записи математических и логических выражений,
в которой операнды расположены перед знаками операций (источник https://ru.wikipedia.org/wiki/%D0%9F%D0%BE%D0%BB%D1%8C%D1%81%D0%BA%D0%B0%D1%8F_%D0%BD%D0%BE%D1%82%D0%B0%D1%86%D0%B8%D1%8F).
Такая запись имеет ряд преимуществ перед инфиксной записью при выражении математических формул:
 1. Любая формула может быть выражена без скобок.
 2. Удобна для вычисления формул в stack машинах (например JVM).
 3. Нет нежелательных приоритетов операторов. 

Необходимо релизовать алгоритм на основе очереди который прочитает математичкую формулу найдет все числа и сложит их отдельно от знаков.  

### Процесс реализации
1. Создаим объект Scanner и запроси ввести формулу в формате: `2 + 3 * 4`.
```java
    Scanner scanner = new Scanner(System.in);
    System.out.println("Введите математическую формулу:");
    String input = scanner.nextLine();
```
2. Создадим две коллекции для хранения знаков и чисел, для хранения числе можно использовать Queue, а знаков Stack - так как нужно будет их доставать с конца.
```java
    Stack<String> sign = new Stack<>();
    Queue<Integer> numbers = new ArrayDeque<>();
```
3. Разберем формулу на по символам для этого используем метод класса `String split`.
```
    String[] arrayValues = input.split(" ");
```
4. Во время того как мы будем перебирать элементы, нужно уметь отличать числа от арифметических знаков, есть несколько способов. Вы можете воспользоваться своим, а я пердлагаю
создать отдельный метод для проверки было прочитано чило или знак.
```
   static boolean isNumber(String value) {
       try {
           Integer.parseInt(value);
           return true;
       } catch (Exception e) {
           return false;
       }
   }
```
5. Создадим цикл чтобы перебрать все элементы массива чисел и знаков, можно использовать `Stream API` или преобразовать в `List`, я же создам
цикл с индексом, и буду добавлять в очередь числа, а в stack все операции.
```
   for (int i = 0; i < arrayValues.length; i++) {
       String value = arrayValues[i];
       if (isNumber(value)) {
           numbers.add(Integer.parseInt(value));
       } else {
           sign.add(value);
       }
   }
```
6. Завершающим этапом можно создать два цикла, прочитать и вывести с начала все числа из очереди, а следом прочитать и вывести все из стэка знаков.
Пример:
```
   while (!numbers.isEmpty()) {
       System.out.print(numbers.poll() + " ");
   }
   
   while (!sign.isEmpty()) {
       System.out.print(sign.pop() + " ");
   }
```
7. Завершаем работу программы.
 
## Инструкция по выполнению домашнего задания

1. Зарегистрируйтесь на сайте [Repl.IT](http://repl.it/).
2. Перейдите в раздел **my repls**.
3. Нажмите кнопку **Start coding now!**, если приступаете впервые, или **New Repl**, если у вас уже есть работы.
4. В списке языков выберите `Java`.
5. Код пишите в левой части окна, вместо строки `System.out.println("Hello world!");`.
6. Опирайтесь на принятый [стиль оформления кода](https://github.com/netology-code/codestyle/blob/master/java/README.md).
7. Посмотреть результат выполнения файла можно, нажав на кнопку **Run**. Результат появится в правой части окна.
8. После окончания работы нажмите кнопку **Share** и скопируйте ссылку из поля Share link.
9. В личном кабинете на сайте [netology.ru](http://netology.ru/) в поле комментария к домашней работе вставьте скопированную ссылку и отправьте работу на проверку.

*Никаких файлов прикреплять не нужно.*

Все задачи обязательны к выполнению для получения зачета. Присылать на проверку можно каждую задачу по отдельности или все задачи вместе. Во время проверки по частям ваша домашняя работа будет со статусом "На доработке".

Любые вопросы по решению задач задавайте в группе на Facebook.