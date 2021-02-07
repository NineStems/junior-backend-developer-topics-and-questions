# Список тем и вопросов для собеседования на web-backend developer
## Работа сети и архитектура сетевых приложений
### Чистая архитектура
Ссылка на дополнительные материалы - [тут](https://habr.com/ru/post/269589)
- Независимость от фреймворка – Архитектура не зависит от существования какой-либо библиотеки. Это позволяет использовать фреймворк в качестве инструмента, вместо того, чтобы втискивать свою систему в рамки его ограничений.
- Тестируемость – Бизнес-правила могут быть протестированы без пользовательского интерфейса, базы данных, веб-сервера или любого другого внешнего компонента.
- Независимоcть от UI – Пользовательский интерфейс можно легко изменить, не изменяя остальную систему. Например, веб-интерфейс может быть заменен на консольный, без изменения бизнес-правил.
- Независимоcть от базы данных – Вы можете поменять Oracle или SQL Server на MongoDB, BigTable, CouchDB или что-то еще. Ваши бизнес-правила не связаны с базой данных.
- Независимость от какого-либо внешнего сервиса – По факту ваши бизнес правила просто ничего не знают о внешнем мире.

### Верхнеуровневый процесс перехода по ссылке  
*Что происходит, когда вбиваешь в адресной строке **sitename.ru***  
Ссылка на дополнительные материалы - [тут](https://habr.com/ru/company/htmlacademy/blog/254825)
- Техническая подоплёка, в которой браузер разбирает, что ему передано – поисковый запрос или адрес
- Проверка, как обращаться к сайту (по какой версии протокола HTTP или HTTPS) 
- Получение по имени IP адреса (если он есть, если его нет – запрос к DNS серверу, где сервер обычно – DNS-сервер провайдера)
- Создание TCP соединения
- Передаются данные пока инициатор прекращения соединения не отправляет пакет FIN и ожидает получить его от второй стороны
- Проверка подписи сертификата 
- Обмен данными с помощью протокола HTTP
- Отдельные ресурсы по типу картинок могут запрашиваться клиентом(браузером) еще несколькими запросами
- Отображение результата пользователю

### Протоколы
**UDP**  
- Транспортный протокол, передающий сообщения-дата граммы без необходимости установки соединения в IP-сети
-	Не требует отклика от клиента и допускает потери пакетов при передаче данных  

**TCP**  
-	Транспортный протокол передачи данных в сетях TCP/IP, предварительно устанавливающий соединение с сетью
-	Требует заранее установленного соединения и позволяет контролировать процесс передачи данных  

**Отличия**  
-	TCP гарантирует доставку пакетов данных в неизменных виде, последовательности и без потерь, UDP ничего не гарантирует.
- TCP нумерует пакеты при передаче, а UDP нет
- TCP работает в дуплексном режиме, в одном пакете можно отправлять информацию и подтверждать получение предыдущего пакета.
-	TCP требует заранее установленного соединения, UDP соединения не требует, у него это просто поток данных.
-	UDP обеспечивает более высокую скорость передачи данных.
-	TCP надежнее и осуществляет контроль над процессом обмена данными.
-	UDP предпочтительнее для программ, воспроизводящих потоковое видео, виде/телефонии, сетевых игр.
-	UPD не содержит функций восстановления данных

### Основные типы HTTP запросов 
Коротко об HTTP - [тут](https://habr.com/ru/post/215117)  
Разница версий HTTP - [тут](https://hostiq.ua/wiki/http-https) 

Главное отличие HTTP (:80) от HTTPS (:443), что второй – надстройка над первым, которая использует защищенный протокол для передачи данных. Защита обеспечивается с помощью SSL сертификата  

- Какие типы бывают и для чего предназначены
  -	OPTIONS - Используется для определения возможностей веб-сервера или параметров соединения для конкретного ресурса
  -	GET - Используется для запроса содержимого указанного ресурса
  -	HEAD - Аналогичен методу GET, за исключением того, что в ответе сервера отсутствует тело, используется для извлечения метаданных
  -	POST - Применяется для передачи пользовательских данных заданному ресурсу
  -	PUT - Применяется для загрузки содержимого запроса на указанный в запросе URI
  -	PATCH - Аналогично PUT, но применяется только к фрагменту ресурса
  -	DELETE - Удаляет указанный ресурс
  -	TRACE - Возвращает полученный запрос так, что клиент может увидеть, какую информацию промежуточные серверы добавляют или изменяют в запросе
  -	CONNECT - Преобразует соединение запроса в прозрачный TCP/IP-туннель, обычно чтобы содействовать установлению защищённого SSL-соединения через нешифрованный прокси
- Коды запросов
  -	1хх – Информационный 
  -	2хх – Успешный 
  -	3хх – Перенаправление 
  -	4хх – Ошибка на стороне клиента
  -	5хх – Ошибка на стороне сервера  

### REST API
Архитектурный стиль взаимодействия компонентов распределённого приложения в сети  
Ссылка на дополнительные материалы - [тут](https://ru.wikipedia.org/wiki/REST)  

- Требования
  -	Модель клиент-сервер
  -	Отсутствие состояния – в отсутствие запросов никакая информация о клиенте на стороне сервера не храниться
  -	Кэширование – ответы должны иметь явный признак, нужно ли их кэшировать или нет
  -	Единообразие интерфейса
  -	Слои
  -	Код по требованию (необязательное ограничение)  


### SOAP  
Ссылка на дополнительные материалы - [тут](https://ru.wikipedia.org/wiki/SOAP)  

Протокол обмена структурированными сообщениями в распределённой вычислительной среде
- Первоначально SOAP предназначался в основном для реализации удалённого вызова процедур (RPC)
- Сейчас протокол используется для обмена произвольными сообщениями в формате XML
-	Использование SOAP для передачи сообщений увеличивает их объём и снижает скорость обработки. В системах, где скорость важна, чаще используется пересылка XML-документов через HTTP напрямую, где параметры запроса передаются как обычные HTTP-параметры.

### gPRC
TODO - Добавить раздел описание

## Микросервисная архитектура

### Возможные вопросы по микросервисам
Кратко по вопросам ниже - [тут](https://habr.com/ru/post/261689/)  

**Что, по-твоему, такое микросервисы?**  
-	[Побольше](https://habr.com/ru/post/249183/)
-	[Попроще](https://habr.com/ru/post/480914/)

**Какие преимущества ты видишь у микросервисной архитектуры по сравнению с монолитом? А какие недостатки?** 
-	Жесткие границы модулей (+) и Увеличение распределённости (-)
-	Независимый деплоймент (+) и Итоговая консистентность (Согласованность) (-)
-	Технологическое разнообразие (+) и Эксплуатационная сложность (-)

**С какими трудностями ты сталкивался в построении микросервисной архитектуры?**  
-	Нет ответа (сейчас)  

**Что ты использовал (или, о чем слышал) для трассировки сервисов? Для мониторинга? А для логирования?**  

- Трассировка/ Логгирование
  - Elasticsearch
  - Logstash
  - Kibana
  - Graylog
- Мониторинг
  - Как быть с консистентностью данных между несколькими микросервисами? -> Какое-то время хранить инфо о данных для восстановления/блокировки дублей, чтобы избежать потери данных и их задубливания  

## Базы данных
Немного о разнице SQL и NOSQL решений - [тут](https://tproger.ru/translations/sql-nosql-database-models/)  

**Основные примеры**  
- SQL
  - SQLite: очень мощная встраиваемая РСУБД
  - MySQL: самая популярная и часто используемая РСУБД
  - PostgreSQL: самая продвинутая и гибкая РСУБД
  - Oracle: мощная и гибкая СУБД, но с высокой стоимостью лицензии
- NOSQL
  - MongoDB – хранит данные в формате, похожем на JSON(Документ)
  - ClickHouse – напоминает классические реляционки, колоночная СУБД
  - Aerospike – хранит данные в формате «Ключ-значение»  
  
**Основные отличия**  
1. Структура и тип хранящихся данных – SQL/реляционные базы данных требуют наличия однозначно определённой структуры хранения данных, а NoSQL базы данных таких ограничений не ставят
2. Запросы – вне зависимости от лицензии, РСУБД реализуют SQL-стандарты, поэтому из них можно получать данные при помощи языка SQL. Каждая NoSQL база данных реализует свой способ работы с данными
3. Масштабируемость – оба решения легко растягиваются вертикально (например, путём увеличения системных ресурсов). Тем не менее, из-за своей современности, решения NoSQL обычно предоставляют более простые способы горизонтального масштабирования (например, создания кластера из нескольких машин)
4. Надёжность – когда речь заходит о надёжности, SQL базы данных однозначно впереди
5. Поддержка – РСУБД имеют очень долгую историю. Они очень популярны, и поэтому получить поддержку, платную или нет, очень легко. Поэтому, при необходимости, решить проблемы с ними гораздо проще, чем с NoSQL, особенно если проблема сложна по своей природе (например, при работе с MongoDB)
6. Хранение и доступ к сложным структурам данных – по своей природе реляционные базы данных предполагают работу с сложными ситуациями, поэтому и здесь они превосходят NoSQL-решения

**Индексы**  
Больше инфы - [тут](https://habr.com/ru/post/102785)  

- Сравнение основных типов
  - B – деревья
    - Хороши для данных с высокой кардинальностью
    - Хороши для баз данных [OLTP](https://ru.wikipedia.org/wiki/OLTP)
    - Занимают много места
    - Легко обновляются
  - Битовые индексы
    - Хороши для данных с низкой кардинальностью
    - Хороши для приложений хранилищ данных [OLAP](https://ru.wikipedia.org/wiki/OLAP)
    - Небольшие по размеру
    - Долгий процесс обновления
  - HASH индексы
    - Сравнивается не значение, а его хэш
    - Нельзя сортировать по значению, что приводит к невозможности использования в сравнениях больше/меньше и «is null»
    - Не уникален, для совпадающих хэшей применяются методы разрешения коллизий

**Термины** - TODO - Изменить название на более логичное  

- [Транзакция](https://ru.wikipedia.org/wiki/%D0%A2%D1%80%D0%B0%D0%BD%D0%B7%D0%B0%D0%BA%D1%86%D0%B8%D1%8F_(%D0%B8%D0%BD%D1%84%D0%BE%D1%80%D0%BC%D0%B0%D1%82%D0%B8%D0%BA%D0%B0)) - группа последовательных операций с базой данных, которая представляет собой логическую единицу работы с данными
- [Кардинальность](https://ru.m.wikipedia.org/wiki/%D0%9C%D0%BE%D1%89%D0%BD%D0%BE%D1%81%D1%82%D1%8C_%D0%BC%D0%BD%D0%BE%D0%B6%D0%B5%D1%81%D1%82%D0%B2%D0%B0) - уникальность данных. Высокая кардинальность - уникальные данные, низкая кардинальность - повторяющиеся данные
- [ACID](https://ru.wikipedia.org/wiki/ACID) - требования к информационной системе
  - [Atomicity](https://ru.wikipedia.org/wiki/%D0%90%D1%82%D0%BE%D0%BC%D0%B0%D1%80%D0%BD%D0%BE%D1%81%D1%82%D1%8C) — Атомарность, гарантирует, что никакая транзакция не будет зафиксирована в системе частично
  - [Consistency](https://ru.wikipedia.org/wiki/%D0%A1%D0%BE%D0%B3%D0%BB%D0%B0%D1%81%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D0%BE%D1%81%D1%82%D1%8C_%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D1%85) — Согласованность. Транзакция, достигающая своего нормального завершения (EOT — end of transaction, завершение транзакции) и, тем самым, фиксирующая свои результаты, сохраняет согласованность базы данных
  - Isolation — Изолированность. Во время выполнения транзакции параллельные транзакции не должны оказывать влияния на её результат
  - Durability — Стойкость. Независимо от проблем на нижних уровнях (к примеру, обесточивание системы или сбои в оборудовании) изменения, сделанные успешно завершённой транзакцией, должны остаться сохранёнными после возвращения системы в работу
- [CAP](https://ru.wikipedia.org/wiki/%D0%A2%D0%B5%D0%BE%D1%80%D0%B5%D0%BC%D0%B0_CAP) - утверждение о том, что в любой реализации распределённых вычислений возможно обеспечить не более двух из трёх следующих свойств

## Инфраструктура и деплой
### Общая информация
-	Что такое сине-зеленый деплой([blue-green deployment](https://habr.com/ru/post/309832/))?
-	Как происходило развертывание приложений на твоем текущем (или предыдущем) месте работы? Какие недостатки ты видишь в этом подходе?
-	Для чего нужны системы оркестрации контейнеров? 
-	Для управления сложными системами, каждый компонент которых это контейнер и выключение одного компонента не выключает всю систему, так же, как и его замена
-	Docker
-	Kubernetes
-	CI\CD
### Окружение
- UNIX
  - Общий опыт использования 
    - GREP – Поиск
    - TAIL – Логи
    - MC – Подобие интерфейса
    - GITK - Утилита для просмотра ветвления репозитория 

## GIT
TODO - Добавить описание основных команд

## Алгоритмы
**Виды**  
-	[Черно-красное дерево](https://habr.com/ru/post/330644)
-	[Бинарное дерево](https://habr.com/ru/post/267855)
-	[Сортировка](https://tproger.ru/translations/sorting-for-beginners)

# Вопросы по языку Golang
## Общая информация
Общая информация о хитростях и проблемах Golang - [тут](https://habr.com/ru/company/mailru/blog/314804/)  
Хорошая презентация с возможностью выполнять код онлайн  - [тут](https://talks.godoc.org/github.com/davecheney/presentations/gopher-puzzlers.slide#1)  
Немного информации про структурные типы данных в Golang   - [тут](http://golang-book.ru/chapter-06-arrays-slices-maps.html)  

Сборщик мусора 
- Вроде неплохой доклад (еще не проверял)  - [тут](https://www.youtube.com/watch?v=CX4GSErFenI)
- Очистка областей памяти, на которые ссылались переменные, что больше не используются  

Как устроены каналы “под капотом”? 
- Под капотом Golang — как работают каналы. Часть 1” - [тут](https://medium.com/%40victor_nerd/%D0%BF%D0%BE%D0%B4-%D0%BA%D0%B0%D0%BF%D0%BE%D1%82%D0%BE%D0%BC-golang-%D0%BA%D0%B0%D0%BA-%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0%D1%8E%D1%82-%D0%BA%D0%B0%D0%BD%D0%B0%D0%BB%D1%8B-%D1%87%D0%B0%D1%81%D1%82%D1%8C-1-e1da9e3e104d)
- Строение каналов в Golang. Часть 2. - [тут](https://medium.com/@victor_nerd/golang-channel-internal-part2-b4e37ad9a118)

## Вопросы
<details>
<summary> <b>Что из себя представляет тип данных string в языке Golang?</b> </summary>
Массив символов
</details> 

<details>
<summary> <b>Можно ли изменить определенный символ в строке?</b> </summary>
Нет, один символ изменить нельзя
</details>  

<details>
<summary> <b>Что происходит при склеивании строк?</b> </summary>
Создание новой строки  
</details>  

<details>
<summary> <b>Вытекающий вопрос — как эффективно склеивать множество строк?</b> </summary>
String.builder  
bytes.buffer + fmt.fprintf  
strconv.appendint  
</details>  

<details>
<summary> <b>Что будет происходить при конкурентной записи в map?</b> </summary>
Ситуация гонки/паника 
</details>  

<details>
<summary> <b>Как можно решить эту проблему?</b> </summary>
Конкурентность/параллелизм  
С помощью синхронизации доступа к объекту  
</details>  

<details>
<summary> <b>Нужно ли лочить структуру мьютексом, если идет конкурентная запись в разные поля структуры?</b> </summary>
Если есть гарантия, что в одно поле структуры одновременно записывает данные не более одного процесса  
</details>  


<details>
<summary> <b>Что выведет код?</b>  
  
 ```
func main() {
   runtime.GOMAXPROCS(1)  
   done := false  
   go func() {  
      done = true  
   }()  
   for !done {  
   }  
   fmt.Println("finished")  
}  
```
<b>Как можно изменить этот код, чтобы был вывод “finished”?</b>  
</summary>
На текущий момент и так выводит finished  
Чтобы увидеть, что он и так работает – нужно усыпить рутину на 2-3 секунды, перед сменой значения переменной done  
</details>  


<details>
<summary><b>Какая есть проблема в коде?   
Как её можно решить?</b>
  
```
var counter int
for i := 0; i < 1000; i++ {
   go func() {
      counter++
   }()
}
```  
  </summary>
С помощью пакета sync (mutex/waitgroup)
<details> <summary> А как её можно бы было решить, если бы в языке не было пакета sync? </summary> С помощью каналов или атомарного счётчика (который сейчас содержится в пакете sync) </details>   
</details>  

<details>
<summary><b>Можно ли реализовать sync.Mutex и sync.WaitGroup на каналах? Как?</b></summary>
Да, можно, с помощью пакета sync (mutex/waitgroup)  

```
package main
import (
	"fmt"
	"time"
)

func main() {
	c := make(chan bool)
	m := make(map[int]int)
	for i := 0; i < 10; i++ {
		go changeMap(c, i, m)
	}
	c <- true
	time.Sleep(2* time.Second)
	fmt.Println("map value", m)
}

func changeMap(n chan bool, i int, m map[int]int) {
	_ = <-n
	fmt.Printf("inside changeMap where i=%d \n", i)
	m[i] = i
	n <- true
}
```
</details>   

<details>
<summary><b>Что ты использовал из пакета sync(кроме Mutex и WaitGroup)?</b></summary>
Атомарный счётчик 
TODO - Добавить, что там еще есть
</details>  

<details>
<summary><b>Что выведет код?</b>

```
func main() {
v := 5
p := &v
println(*p)
changePointer(p)
println(*p)
}
func changePointer(p *int) {
v := 3
p = &v
}  
```  
  </summary>
  <details>
    <summary>Почему? Как нужно изменить функцию changePointer, чтобы вывело 5 и 3 (в оригинальной версии выводится 5 и 5)?
    </summary>
  Потому что мы в другой области видимости создаём переменную и подменяем не значение, а ссылку, что хранится в p, когда же функция отрабатывает в основной области видимости переменная хранит старую ссылку
  </details> 
</details>  

<details>
<summary><b>За сколько примерно выполнится приложение — за 3 секунды или за 6?</b>
  
```
func worker() chan int {
ch := make(chan int)
go func() {
time.Sleep(3 * time.Second)
ch <- 42
}()
return ch
}
func main() {
timeStart := time.Now()
_, _ = <-worker(), <-worker()
println(int(time.Since(timeStart).Seconds())) // что выведет - 3 или 6?
}
```  
  </summary>
<details> <summary> Что нужно изменить, чтобы код работал за 3 секунды? </summary> Добавить инициализацию воркеров, а потом ждать ответов из них </details>   
</details>  


# Задачи для разминки 

## Задачки на БД
**№1**  
Составить структуру таблиц и связей (спроектировать бд библиотеки, автор, книга, пользователь. Много авторов, книга на руках у одного пользователя)

**№2**  
Несколько выборок с группировками по этой созданной БД
-	Найдите книги (в т.ч названия), которые на руках у пользователя и написанные более чем 2 авторами
-	Топ 3 популярных авторов  

**№3**  
Пояснить какой индекс будет создан и почему именно такой при использовании конкретного запроса  
Построить оптимальный индекс для `SELECT * FROM employee WHERE sex = 'm' AND salary > 300000 AND age = 20 ORDER BY created_at`  

## Задачи на алгоритмы  
Доп задачки для переноса - [тут](https://habr.com/ru/company/rebrainme/blog/540354/)
Еще задачки - [тут](https://tproger.ru/problems/sobesedovanie-na-poziciju-middle-javascript-razrabotchika-primery-zadach-i-neobhodimye-znanija/)
**№1**  
Написать функцию, которая возвращает массив заданной длины, с уникальными числами  

**№2**  
Написать функцию, которая будет валидировать строку со скобочками (задачка на скобочки. Нужно определить валидно ли расставлены скобочки {}{[]}() – true , {)(} – false, (([(]))) – false)  

**№3**  
Написать функцию, которая принимает число n и возвращает матрицу nxn, где заполняет её значениями спирально (справа налево, к центру)  

**№4**  
Есть структура геолокаций Страна-Регион-Город. На вход подаётся два массива, которые могут содержать произвольное количество элементов(но не более 3х) или быть пустыми.  
Первый элемент, это то, что должно быть в итоге показано, а второй - то, что должно быть исключено из показа.
Нужно определить пересекаются ли элементы и вернуть те, что пересекаются, например:  
- Россия-Краснодарский край-Краснодар и Россия-Краснодарский край = Пересекаются и нужно исключить весь Краснодарский край
- Россия-Краснодарский край и Россия-Краснодарский край-Краснодар = Пересекаются и нужно исключить только Краснодар
- Россия-Ростовская область и Россия-Краснодарский край-Краснодар = Не пересекаются и исключать ничего не нужно

## Задачи на понимание архитектуры
**№1**  
Есть два сервиса, сервис один сохраняет данные и отправляет их в медленный сервис два - как бы вы организовали работу двух этих сервисов с учётом того, что сервис два медленный и только получает данные  

# Дополнительная информация
## Полезные ссылки
-	[Спецификация по языку](https://golang.org/ref/spec) 
- 	[Модель памяти го. на начальном этапе не надо, но знать полезно](https://golang.org/ref/mem)
- 	[Про организацию кода. GOPATH и пакеты](https://golang.org/doc/code.html)
-	[https://golang.org/cmd/go/](https://golang.org/cmd/go/)	
-	[https://blog.golang.org/strings](https://blog.golang.org/strings)
-	[https://blog.golang.org/slices](https://blog.golang.org/slices)
-	[https://blog.golang.org/go-slices-usage-and-internals](https://blog.golang.org/go-slices-usage-and-internals)
-	[Вики го на гитхабе. очень много полезной информации](https://github.com/golang/go/wiki)
-	[https://blog.golang.org/go-maps-in-action](https://blog.golang.org/go-maps-in-action)
-	[https://blog.golang.org/organizing-go-code](https://blog.golang.org/organizing-go-code)
-	[Основной сборник тайного знания, сюда вы будуте обращатсья в первое время часто](https://golang.org/doc/effective_go.html)
-	[Как ревьювить (и писать код). обязательно к прочтению](https://github.com/golang/go/wiki/CodeReviewComments)
-	[Материал аналогичный 50 оттенков го](https://divan.github.io/posts/avoid_gotchas/)
-	[https://research.swtch.com/interfaces](https://research.swtch.com/interfaces)
-	[https://research.swtch.com/godata](https://research.swtch.com/godata)
-	[http://jordanorelli.com/post/42369331748/function-types-in-go-golang](http://jordanorelli.com/post/42369331748/function-types-in-go-golang)
-	[Работа с файлами](https://www.devdungeon.com/content/working-files-go)
-	[Много how-to касательно базовых вещей в go](http://www.golangprograms.com)
-	[Набор how-to где можно получить углублённую информацию по всем базовым вещам. очень полезн](http://yourbasic.org/golang/)
-	[http://yourbasic.org/golang/blueprint/](http://yourbasic.org/golang/blueprint/)
-	[https://github.com/Workiva/go-datastructures](https://github.com/Workiva/go-datastructures)
-	[Большая подборка статей по многим темам (не только данной лекции)](https://github.com/enocom/gopher-reading-list)
-	[Как организовать код](https://www.youtube.com/watch?v=MzTcsI6tn-0)
-	[Статья на предыдущую тему](https://medium.com/@benbjohnson/standard-package-layout-7cdbc8391fc1)
-	[50 оттенков го](https://habrahabr.ru/company/mailru/blog/314804/)
-	[Разбираемся в Go: пакет io](https://habrahabr.ru/post/306914/)
-	[Постулаты go. Маленькая статья об основными принципах языка](https://habrahabr.ru/post/272383/)
-	[Лучшие практики go](https://habrahabr.ru/company/mailru/blog/301036/)
-	[Организация кода в go](https://habrahabr.ru/post/308198/)
-	[Зачем в Go амперсанд и звёздочка (& и *)](https://habrahabr.ru/post/339192/)
-	[Как не наступать на грабли в Go](https://habrahabr.ru/post/325468/)
-	[Краш-курс по интерфейсам в Go](https://habrahabr.ru/post/276981/)
-	[http://golang-book.ru](http://golang-book.ru)
## Литература по го на русском языке:  
-	Язык программирования Go, Алан А. А. Донован, Брайан У. Керниган
-	Go на практике, Matt Butcher, Мэтт Фарина Мэтт
-	Программирование на Go. Разработка приложений XXI века, Марк Саммерфильд
