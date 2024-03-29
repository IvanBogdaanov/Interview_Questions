# Вопросы и ответы (Swift)

  Эта страница содержит в себе основные вопросы для собеседования junior iOS разработчика по языку **Swift**

**1. Различие между структурой и класом?**
   - Струкутра не поддерживает наследование.
   - Следовательно структура не может использовать приведение типов.
   - Структуры не могут использовать деинициализаторы.
   - Система подсчета ссылок (ARC) не работает со структурами.
   - Струкутра это тип значения (value type), а класс - ссылочный тип (reference type).
   
**2. В чем отличие типа значения от ссылочного типа?**
   - Когда указан value type, то значение копируется, а когда reference type, то значение передается по ссылке.
 ```Swift
    
    // Value type
    struct Player {
      
      var name = "Vanya"
      var age = 22
      
    }
    var firstPlayer = Player() // name = "Vanya", age = 22
    var secondPlayer = firstPlayer // создаем второго игрока с таким же именем и возрастом
    firstPlayer.age = 21
    print(firstPlayer) // name = "Vanya", age = 21
    print(secondPlayer) // name = "Vanya", age = 22, то есть по сути это второй объект
    
    // Reference type
    class Player {
    
      var name = "Vanya"
      var age = 22
      
    }
    let firstPlayer = Player() // name = "Vanya", age = 22
    let secondPlayer = firstPlayer // создаем игрока с такими же данными, но теперь мы следим за игроком и если
                                   // у него значение поменяется то соответственно и у нас значение изменится,
                                   // по сути создается ссылка
    firstPlayer.age = 21
    print(firstPlayer) // name = "Vanya", age = 21
    print(secondPlayer) // name = "Vanya", age = 21
    
 ```
 **3. Что такое ООП?**
  - ООП (Объектно-ориентированное программирование) - это способ программирования который основан на объектах, где
   объект является экземпляром класса, а класс является информационной сущностью в которой хранятся наши данные (свойства, методы и т.д).
   Главной целью ООП является структурирование информации для наилучшего управления ею.
   
 **4. Основные принципы ООП.**
   - **Наследование** - перенятие (копирование) свойств и методов у другого класса. Класс у которого переняли свойства и методы называется
   родительским классом, тот кто перенял будет называться дочерним классом.
   - **Инкапсуляция** - сокрытие реализаций своего кода там где нужно. К примеру нужно решить уравнение и у нас есть некоторая функция,
   мы в ее параметры подставляем свои аргументы и она "под капотом" производит вычисления.
   - **Полиморфизм** - Это выделение общих интерфейсов (функций) для абстрактных классов. К примеру Абстрактный класс Phone должен уметь звонить,
   так вот функция call() и будет называться полиморфной функцией.
   
   *P.S. В языке Swift не существует такого понятия как "абстрактный класс", у нас он заменяется путем расширения нашего класса протоколом.*
   
 **5. Что такое UIViewController?**
  - UIViewController - это класс, который имеет свой жизненный цикл, где жизненный цикл представляет собой определённые события.
  
 **6. Рассказать про жизненный цикл UIViewController.**
  - Жизненный цикл UIViewController - это набор событий (функций) которые выполняются в определённом порядке в классе UIViewController.
  Жизненный цикл состоит из (по порядку):
  1) **Init()** - инициализация. Инициализация - создание и назначение определенных параметров.
  2) **LoadView()** - инициализавция UIView.
  3) **ViewDidLoad()** - Наша UIView загрузилась, но у нее нет внутрених границ (bounds).
  4) **ViewWillAppear()** - Готов к появлению, но еще не установлена ориентацию экрана.
  5) **ViewWillLayoutSubviews()** - Вызывается перед поворотом экрана.
  6) **ViewDidLayoutSubviews()** - Вызывается после поворота экрана.
  7) **ViewDidAppear()** - Вызывает после появления на экране.
  8) **ViewWillDisappear()** - Вызывается перед тем как исчезнуть с экрана.
  9) **ViewDidDisappear()** - Вызывается после исчезновение с экрана.
  
  **7. Что такое замыкание?**
   - Замыкание - это функция, содержащая в себе ссылки на переменные из внешней области видимости.
   
  **8. Какой тип имеют замыкания?**
   - Замыкания являются ссылочным типом.
   
  **9. Что такое лист захвата (capture list)?**
   - Это массив из значений на которые мы ссылаемся.Его основная цель состоит в том чтобы избавить нас от утечки памяти. В коде этот массив выглядит так:
   ```Swift
   { [weak self] in
   
   }
   ```
   
   **10. В чем отличие escaping замыкания от обычного?**
    - Тем что сбегающее замыкание можем передать во внешнюю область кода или использовать в асинхронных потоках
    
   ```Swift
    var arrayClousers = [() -> ()]()
    // Для того чтобы была возможность использовать так как ниже - нужно добавить перед типом @escaping
    func myFunc1(clouser: () -> ()) {
    
      arrayClousers.append(clouser) // Выдаст ошибку
      
      DispatchQueue.main.async {
        clouser() // Так же не рекомендуется выполнять
      }
      
    }
   ```
   **11. Рассказать про принципы SOLID**
   - **S** *(The Single Responsibility Principle)* - Принцип гласит о том что класс должен иметь одну ответственность.Все 
     его поведения должны быть направлены исключительно на обеспечение этой ответственности.
   - **O** *(The Open Closed Principle)* - Объекты должны быть открыты для расширения, но закрыты для модификаци.
   - **L** *(The Liskov Substitution Principle)* - Наследующий класс должен дополнять, а не изменять базовый.
   - **I** *(The Interface Segregation Principle)* - Много интерфейсов (функций) лучше чем однин общий.
   - **D** *(The Dependency Inversion Principle)*  - Лучше зависить от чего то общего, чем от чего то конкретного.
  
  **12. Что такое GCD, поток? Рассказать про них, назвать основные проблемы многопоточности и как они решаются.**
    *GCD* - это фреймворк служащий для управления потоками.
    
 Поток это по сути последовательное выполнение каких - либо задач. Количество потоков зависит напрямую от количества ядер процессора.
   Сами потоки можно разделить на два типа - **main** и **global**. Гланый поток - это поток в котором выполняются все действия связанные с ui - интерфейсом и он создается всегда.
   
   По способу выполнения задач потоки деляется на последовательные и параллельные. Последовательное выполнение - это когда следущая задача не может начаться пока не кончится предыдущая, а параллельное выполнение - это когда задачи могут начинать свое выполнение не дожидаясь пока кончится предыдущая.

 Так же потоки разделяются на **синхронные** и **асинхронные**. Тут тоже все достаточно просто, синхронные потоки это те потоки которые блокируют текущую очередь и передают выполнение задачи на другую, и пока она не выполнится очередь будет заблокированна. Асинхронная очередь - это тоже самое но очередь не блокируется, а продолжает свое выполнение.

 Проблемы многопоточности:

 Можно выделить три основные проблемы многопоточности. 

 - *Состояние гонки(race condition)* - возникает тогда, когда несколько потоков многопоточного приложения пытаются одновременно получить доступ к данным, причем хотя бы один поток выполняет запись, последствия могут быть не предсказуемыми.

 Решение: использовать семафоры или группы отправки.

 - *Инверсия приоритетов* - по сути это то когда высокоприоритетный процесс ждет сигнала от низкоприоритетного процесса о том что он выполнил задачу.

Решение: принудительное повышение приоритетов

 - *Взаимная блокировка* - это когда несколько потоков находятся в ожидании доступа к ресурсам и не один из них не может начать выполнение пока не освободится доступ к ресурсу.

 Решение: не использовать такие вложенности или же использовать повышение приоритетов.

**13.Что такое ARC? Как работает?**

 *ARC* - это автоматическая система подсчета ссылок, нужна для управления памятью. Эта система применима только к ссылочным типам.

 Когда мы создаем экземпляр класса, в оперативной памяти выделяется место для ее хранения, у этого места есть адрес и этот адрес будет являться ссылкой на объект в памяти. ARC ведет за вас подсчет количество ссылок на этот экземпляр и в случае когда счетчик будет равен нулю ARC освободит из памяти данный объект.

**14. Что такое strong, weak and unowned ссылки?**

 - *Strong* ссылка - это та ссылка которая учитывается ARC в счётчике ссылок.

 - *Weak* ссылка - это та ссылка которая не учитывается ARC в счётчике ссылок. То есть по сути она может быть равна nil.

 - *Unowned* ссылка - это та ссылка которая не учитывается ARC в счётчике ссылок. Но всегда будет иметь значение.

**15.Что такое цикл сильный ссылок?**

 Это когда одна сильная ссылка ссылается на другую, а та в свою очередь ссылается на ту которая ссылается на нее.

 Решается путем объявления одной из ссылок weak или unowned.

**16. Что такое перечесления? К какому типу они относятся?**

 - *Перечисления* - это набор ассоциативных значений у которых может быть свое значение.

 Перечесления относятся к типу значений.

**17. Рассказать о коллекциях в Swift(структуры данных)**

 В Swift можно выделить 3 типа коллекций.

 - *Массивы* - это структура данных в которой значения упорядочненны в определенном порядке(по индексам).

 - *Множества* - это неупорядочненная структура данных в которой хранятся уникальные значения (подписана под протокл хэширования).

 - *Словари* - это неупорядочненная структура данных в которой значения хранятся в виде ключ-значение (подписана под протокл хэширования).

**18. Что такое опциональное тип?**

 Опциональное тип говорит о том что объект может не содержать ничего, быть равным nil(нулю).

**19. Как безопасно извлечь опциональное значение?**

 Есть несколько способов:

 - Использовать конструкцию guard let, if let.

 - Использовать опциональную цепочку.

 - Проверить через if(object != nil)

- Nil-Coalescing 

**20. Чем frame отличается от bounds?**

 *Frame* - это внешние границы, а *bounds* это внтурние границы.

**21. Что такое HTTP и чем отличается от HTTPS?**

 - *HTTP* - это протокол для передачи данных в интернете, а HTTPS это тот же протокол, но с шифрованием данных.

**22. Что такое REST API?**

 - *REST API* - это архитектура API которая описывает общение с сервером.

**23. Какие HTTP методы вы знаете?**

 **GET**
 - Метод GET запрашивает данные ресурса.


 **HEAD**
 - Делает тоже самое что и GET, но без тела ответа.


 **POST**
 - Отправляет данные на сервер и в отличии от GET метода имеет тело запроса.


 **DELETE**
 - Удаляет указанный ресурс.


 **PUT**
 - Служит для изменения текущих записей на сервере.

**24. Что такое дженерики?**

 Это шаблон при котором можно писать универсальные функции.
