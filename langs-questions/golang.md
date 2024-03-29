## Вопросы по языку Golang

[Больше вопросов](https://github.com/goavengers/go-interview)

<details>
<summary> <b>Что из себя представляет тип данных string в языке Golang?</b> </summary>
последовательность(массив байт) из одного или нескольких символов (буквы, числа, символы), которая может представлять собой константу или переменную. В зависимости от кодировки символ может занимать один или более байт.
</details> 

<details>
<summary> <b>Можно ли изменить определенный символ в строке?</b> </summary>
Строки составляются из символов Unicode и являются неизменяемыми последовательностями, т. е. порядок этой последовательности нельзя изменить. В зависимости от кодировки.
</details>  

<details>
<summary> <b>Что происходит при склеивании строк?</b> </summary>
Выделение памяти на новую переменную, т.е. создание новой строки.
</details>  

<details>
<summary> <b>Вытекающий вопрос — как эффективно склеивать множество строк?</b> </summary>
С помощью нескольких вариантов strings.builder / bytes.buffer / fmt.fprintf / strconv.appendint  
</details>  

<details>
<summary><b>Как хранятся переменные в Golang?</b></summary>
Переменная представляет именованный участок в памяти, который может хранить некоторое значение
</details>  

<details>
<summary><b>Как устроен пустой интерфейс?</b></summary>
Пустой интерфейс может содержать значения любого типа. (Каждый тип реализует как минимум нулевые методы.)
Пустые интерфейсы используются кодом, обрабатывающим значения неизвестного типа. Например, fmt.Print принимает любое количество аргументов типа interface{}.  
Есть как плюсы, так и минусы использования.
</details>  

<details>
<summary>todo <b>Как устроен слайс и чем он отличается от массива?</b></summary>
Слайс - гибкое отображение элементов массива с возможностью динамического изменения размера.
Слайс в отличии от массима - динамическая структура.
</details>  

<details>
<summary><b>Нужно ли передавать slice по ссылке в фукнцию?</b></summary>
Слайс - ссылочная структура, если не изменяется cap слайса, то любые изменения будут отражены вне области изменения, иначе новые добавленные элементы, свыше изначального cap не будут видны вне области их добавления. Это происходит потому что при расширении cap меняется ссылка на область памяти, куда смотрит слайс.
</details> 

<details>
<summary>todo <b>Расскажите про планировщик golang</b></summary>
Планировщик эффективно использует потоки системы. На каждый поток есть N горутин, активация которых происходит из пула очередей. Контекст, связанный с потоком выбирает горутину, которую сделать активной. В случае если в пуле нет горутин, выполняется механизм "кражи", который забирает горутину у соседнего потока или из "неотсортированного" пула, куда попали горутины, что ранее вышли из зоны ответственности гошного планировщика, но позже вернулись обратно.
</details> 

<details>
<summary><b>В чем различия goroutine от потока системы?</b></summary>
это легкий поток, управляемый средой выполнения Go. В каждом потоке системы может быть N горутин. Изначально стек горутина занимает 2kb и может как увеличиваться, так и уменьшаться.
</details> 

<details>
<summary><b>Как огранить число потоков на системы при запуске Golang программы и возможно ли огранить их до 1 потока?</b></summary>
С помощью установки значения переменной gomaxproc
</details> 

<details>
<summary>todo <b>Что такое каналы и каких видов они бывают?</b></summary>
Это типизированные области памяти, по которым вы можете посылать и получать значения. Они бывают двух видов - буферизованные(блокировка не происходит пока не забьётся буфер) и небуферизованные(отправление и получение блокируются до тех пор, пока другая сторона не готова).
</details> 

<details>
<summary>todo <b>Что будет если писать в закрытый канал?</b></summary>
Программа пробросит панику
</details> 

<details>
<summary>todo <b>Что будет если писать в неинициализированный канал?</b></summary>
Произойдёт взаимная блокировка (deadlock)
</details> 

<details>
<summary><b>Как в golang освобождается память и можно ли отключить это поведение и зачем это делать?</b></summary>
Есть GC, автоматическую очистку можно отключить и вызывать очистку вручную. Для более точного управления ресурсами приложения.
</details> 

<details>
<summary><b>Что будет происходить при конкурентной записи в map?</b> </summary>
Ситуация гонки/паника 
</details>  

<details>
<summary><b>Как можно решить эту проблему?</b> </summary>
Конкурентность/параллелизм  
С помощью синхронизации доступа к объекту  
</details>  

<details>
<summary><b>Нужно ли блокировать структуру мьютексом, если идет конкурентная запись в разные поля структуры?</b> </summary>
Если есть гарантия, что в одно поле структуры одновременно записывает данные не более одного процесса  
</details>  

<details>
<summary><b>Что такое lock-free структуры</b> </summary>
Если есть гарантия, что в одно поле структуры одновременно записывает данные не более одного процесса  
</details> 


<details>
<summary><b>Что выведет код?</b>  
  
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
</summary>
<details>
<summary><b>Как можно изменить этот код, чтобы был вывод “finished”?</b>  </summary>
Можно, например, усыпить главную рутину, чтобы активировалась та, что должна была сменить значение параметра done и тем самым отобразит в консоли finished
</details>  
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
<summary>todo <b>Что ты использовал из пакета sync(кроме Mutex и WaitGroup)?</b></summary>
Атомарный счётчик 
todo - Добавить, что там еще есть
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
    <summary><b>Почему? Как нужно изменить функцию changePointer, чтобы вывело 5 и 3 (в оригинальной версии выводится 5 и 5)?</b>
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

<details>
<summary><b>Расскажите о ООП в Golang</b></summary>
todo
</details> 

<details>
<summary><b>Как работает сборщик мусора в Golang?</b></summary>
Очистка областей памяти, на которые ссылались переменные, что больше не используются
</details> 

<details>
<summary><b>Что произойдёт при выполнении данного кода?</b>
  
```
package main

import (
	"fmt"
)

type Test struct {
	Name string
}

func main() { 
	mapCampaigns := make(map[string]*Test)
	name := mapCampaigns[""].Name
	fmt.Println(name)
}
```  
</summary>
<details> <summary><b>Что нужно сделать, чтобы избежать паники?</b></summary> Получать два параметра при получении значении из мапы и явно обрабатывать ключ существования элемента </details>   
</details>  

<details>
<summary>todo <b>У вас есть метод square объявленный у структуры по указателю, он берет поле структуры i и возвращает его квадрат.  
Имеет ли смысл объявить этот метод от значения?  
В каких случаях у нас будет работать только один метод?</b></summary>
todo 
</details>  

<details>
<summary><b>Какая из записей будет требовать дополнительных действий по инициализации и почему</b>  

```
var a []int64  
var b map[int64]string  
c := []int64{}  
d := make(map[int64]string)
```  

</summary>
Для переменной b необходимо провести инициализацию, потому что значением не инициализированной карты - nil, но в отличии от функции append для слайса, в которой под капотом происходит инициализация, для мапы такого механизма нет 
</details>  

<details>
<summary><b>Что вы можете сказать о данном коде? Что произойдет при вызове данных методов? Поясните свою точку зрения</b>  

```
package a
func A1() int {return b.B() + 3}  
func A2() int {return 2}  

package b
func B() int {return a.A2() * 2}  
```  

</summary>
Код не будет скомпилирован, так как тут есть цикличная зависимость
</details>  
