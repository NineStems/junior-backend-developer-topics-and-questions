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
