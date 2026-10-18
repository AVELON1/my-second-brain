
[recursivefactorial](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-04/recursivefactorial?event=1081)
Write a **recursive** function that returns the factorial of the `int` passed as parameter.
Errors (non possible values or overflows) will return `0`.
`for` is **forbidden** for this exercise.

```go
fucn RecursiveFactorial(nb int) int {
	if nb<0 {
		return 0
	}
	if nb == 0 {
		return 1
	}
	return nb * RecursiveFactorial(nb-1)
}

func main() {
arg := 4
fmt.Println(piscine.RecursiveFactorial(arg)) 
}

$ go run . 
24 
$
```
В рекурсивной функции нужны две вещи:

1. **Условие остановки** — самая маленькая задача, ответ на которую уже известен. Здесь: `0! = 1`.
2. **Рекурсивный шаг** — функция вызывает себя для числа поменьше.

как все было?
если nb=4
то 4RecursiveFactorial(4-1)
а теперь комп ищет значение
RecursiveFactorial(4-1)
а его значение это
3*RecursiveFactorial(3-1)
теперь нужно нацти значение
*RecursiveFactorial(3-1)
2*RecursiveFactorial(2-1)
и так до 
1*RecursiveFactorial(1-1)
а функция RecursiveFactorial(1-1) равен 1 поэтому мы и написали
if nb == 0 {
	return 1
}
и теперь все с этого 1 решает задачу всех функции и доходит до последнего
рекурсия это **Функция решает задачу, вызывая саму себя для чуть меньшей задачи.**

[iterativepower](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-04/iterativepower?event=1081)
Write an **iterative** function that returns the value of `nb` to the power of `power`.
Negative powers will return `0`. Overflows do **not** have to be dealt with.
```go
fucn IterativePower(nb int, power int)int{
	if power < 0 {
		return 0
	}
	if power == 0{
		return 1
	}
	res=1
	for i:=0; i < power; i++{
		res = res*nb
	}
	return res
}

func main() { 
	fmt.Println(piscine.IterativePower(4, 3)) 
}

$ go run . 
64 
$
```

[recursivepower](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-04/recursivepower?event=1081)
Write a **recursive** function that returns the value of `nb` to the power of `power`.
Negative powers will return `0`. Overflows do **not** have to be dealt with.
`for` is **forbidden** for this exercise.
```go
func RecursivePower(nb int, power int) int { 
	if power < 0 {
		return 0
	}
	if power == 0 {
		return 1
	}
	return nb*RecursivePower(nb, power-1)
}

func main() { 
	fmt.Println(piscine.RecursivePower(4, 3)) 
}

$ go run . 
64 
$


RecursivePower(4, 3)
= 4 × RecursivePower(4, 2)
= 4 × 4 × RecursivePower(4, 1)
= 4 × 4 × 4 × RecursivePower(4, 0)
= 4 × 4 × 4 × 1
= 64
```

[fibonacci](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-04/fibonacci?event=1081)
Write a **recursive** function that returns the value at the position `index` in the fibonacci sequence.
The first value is at index `0`.
The sequence starts this way: 0, 1, 1, 2, 3 etc...
A negative index will return `-1`.
`for` is **forbidden** for this exercise.

```go
func Fibonacci(index int) int { 
	if index < 0 {
		return -1
	}
	
	if index == 0 {
		return 0
	}
	if index == 1{
		return 1
	}
	
	return Fibonacci(index-1) + Fibonacci(index-2)
}

func main() { 
	arg1 := 4 
	fmt.Println(piscine.Fibonacci(arg1)) 
}

$ go run . 
3 
$

iteration:
when index = 4:
fibonacci(4-1)+fibonacci(4-2)=fibonacci(3)+fibonacci(2)
	1)fibonacci(3)
	fibonacci(2)+fibonacci(1)=fibonacci(2)+1
		fibonacci(2)
		fibonacci(1)+fibonacci(0)=1+0=1

	2)fibonacci(2)
	fibonacci(1)+fibonacci(0)=1+0
fibonacci(3)+fibonacci(2)=2+1=3
arg1:=4=index если что. мы просто индексы искали 

```


[sqrt](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-04/sqrt?event=1081)
Write a function that returns the square root of the `int` passed as parameter, if that square root is a whole number. Otherwise it returns `0`.

```go
func Sqrt(nb int) int { 
	if nb <= 0 {
		return 0
	}
	for i := 1; i*i <= nb; i++ {
		if i*i == nb {
			return i
		}
	}
	return 0
}

func main() { 
	fmt.Println(piscine.Sqrt(4)) 
	fmt.Println(piscine.Sqrt(3)) 
}

$ go run . 
2 
0 
$
```

последний `return 0` нужен, если цикл закончился, но точный целый корень не нашёлся. Например, для `nb == 10` проверятся `1`, `2` и `3`; ни одно из их квадратов не равно `10`, поэтому функция вернёт `0`. Здесь `0` означает «целого квадратного корня нет». Кроме того, в Go функция, которая возвращает `int`, должна вернуть значение на каждом пути выполнения — без этого код не скомпилируется.
почему когда мы находим правильный ответ то return 0 не срабатывает а вернет правильный ответ?
`return i` сразу завершает выполнение всей функции и возвращает найденное число. До последнего `return 0` выполнение уже не дойдёт.
Например, если `nb == 4`:
1. `i` становится `1`: `1*1 != 4`.
2. `i` становится `2`: `2*2 == 4`.
3. Выполняется `return i` — функция возвращает `2` и заканчивается.
Последний `return 0` сработает только если цикл закончился, а совпадение так и не нашлось. Например, при `nb == 5` функция вернёт `0`


[isprime](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-04/isprime?event=1081)
Write a function that returns `true` if the `int` passed as parameter is a prime number. Otherwise it returns `false`.
The function must be optimized in order to avoid time-outs with the tester.
(We consider that only positive numbers can be prime numbers)
(We also consider that 1 is **not** a prime number)

prime number is the number that can be divided only to 1 and to itself

```go
func IsPrime(nb int) bool {
	// We also consider that 1 is **not** a prime number по заданию так что исключаем все вещи которые не могут входить в прайм числа вклбчая 1 и минус числа
	if nb <= 1 {
		return false
	}
	// если число равен 2 то отправляем тру это нужно чтобы нам улучшить быстроту кода как на задании написано, и как она улушчается? мы знаем что большк 2 никакие нечетные числа не хводят в прайм так что мы выделяем именно 2 из них так как только это нечетное число входит в это
	if nb == 2 {
		return true
	}
	//если чтобы то не было если делаить на 2 бесконечно то калдык будет 0 то пишем фалс чтобы быстро исклбючить их
	if nb%2 == 0 {
		return false
	}
	//мы начинаем с 3(нечетное) а i += 2 означает что после 3 тот берет 5 и так далее тоесть все нечетные числа но если нечетное число делаится на интеджер с калдык 0 то пишем фалс(интеджер это не флоат так что может быть так что 9 мождет делиться на 3 и без калдык так что их тоже исключаем)
	for i := 3; i*i <= nb; i += 2 {
		if nb%i == 0 {
			return false
		}
	}
	return true
}

func main() { 
	fmt.Println(piscine.IsPrime(5)) 
	fmt.Println(piscine.IsPrime(4)) 
}

$ go run . 
true 
false 
$
```

[findnextprime](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-04/findnextprime?event=1081)
Write a function that returns the first prime number that is equal or superior to the `int` passed as parameter.
The function must be optimized in order to avoid time-outs with the tester.
(We consider that only positive numbers can be prime numbers)

```go
func IsPrimeCheck(nb int) bool {
	if nb <= 1 {
		return false
	}
	if nb == 2 {
		return true
	}
	if nb%2 == 0 {
		return false
	}
	for i := 3; i*i <= nb; i += 2 {
		if nb%i == 0 {
			return false
		}
	}
	return true
}
 
func FindNextPrime(nb int) int {
	if nb <= 2 { //самое минимальное superior prime number для nb <= 2 это 2
		return 2
	}
	for !IsPrimeCheck(nb) { //тоесть если мы берем 4 и тот false вышло из IsPrimeCheck(nb) и тот в=перевернет его на тру и только потом цикл заработает и даст 
		nb++
	}
	return nb
}


func main() { 
	fmt.Println(piscine.FindNextPrime(5)) 
	fmt.Println(piscine.FindNextPrime(4)) 
}

$ go run . 
5 
5 
$
```
как работает часть:	for !IsPrimeCheck(nb) { 
	nb++
}?
- **Запуск:** Мы вызываем функцию для `nb = 8`.
- **Проверка цикла:** Вычисляется условие `!IsPrimeCheck(8)`.
    - Функция `IsPrimeCheck(8)` проверяет число 8. Оно четное, делится на 2, поэтому она возвращает **`false`**.
    - Восклицательный знак перед функцией (`!`) инвертирует значение: `!false` превращается в **`true`**.
    - Условие цикла истинно (`true`), поэтому цикл **начинает работу**.
- **Первый шаг цикла (`nb++`):**
    - Переменная увеличивается на 1: теперь `nb = 9`.
- **Вторая итерация цикла:** Цикл снова проверяет условие: `!IsPrimeCheck(9)`.
    - Функция `IsPrimeCheck(9)` проверяет девятку. Она видит, что 9 делится на 3 ($9 \% 3 == 0$), поэтому `IsPrimeCheck(9)` возвращает **`false`**.
    - Восклицательный знак снова делает это значение **`true`** (`!false = true`). Условие снова истинно, цикл **продолжается**.
- **Второй шаг цикла (`nb++`):**
    - Переменная снова увеличивается на 1: теперь `nb = 10`.
- **Третья итерация цикла:** Проверяем `!IsPrimeCheck(10)`.
    - Число 10 четное, `IsPrimeCheck(10)` возвращает **`false`**, а `!` делает его **`true`**. Цикл снова идет дальше.
- **Третий шаг цикла (`nb++`):**
    - Переменная увеличивается: теперь `nb = 11`.
- **Четвертая итерация цикла:** Проверяем `!IsPrimeCheck(11)`.
    - Число 11 — **простое**! Функция `IsPrimeCheck(11)` возвращает **`true`**.
    - Но перед ней стоит восклицательный знак (`!`), который превращает `true` в **`false`**.
    - Условие цикла становится ложным (`false`), и **цикл мгновенно прекращает работу**!
- **Финал:** Функция возвращает текущее значение `nb`, которое равно **`11`**.

[eightqueens](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-04/eightqueens?event=1081)
Write a function that prints the solutions to the [eight queens puzzle](https://en.wikipedia.org/wiki/Eight_queens_puzzle).
Recursivity must be used to solve this problem.
It should print something like this :
$ go run .
15863724 
16837425 
17468253 
...

Each solution will be on a single line. The index of the placement of a queen starts at 1. It reads from left to right and each digit is the position for each column. The solutions will be printed in ascending order.

```go
func isSafe(board [8]int, col, row int) bool { //[8]int это массив из 8 чисел
	for c := 0; c < col; c++ {
		r := board[c]
		if r == row || r-c == row-col || r+c == row+col {
			return false
		}
	}
	return true
}

func solve(board [8]int, col int) {
	if col == 8 {
		for _, pos := range board {
			z01.PrintRune(rune(48 + pos))
		}
	z01.PrintRune(rune(10))
	return
	}

	for row := 1; row <= 8; row++ {
		if isSafe(board, col, row) {
			board[col] = row
			solve(board, col+1)
		}
	}
}

func EightQueens() {
	var board [8]int // создает пустой массив из восьми нулей (чистая доска, где еще нет ферзей)
	solve(board, 0) // Запускаем расстановку с нулевого столбца (col = 0)
}
```
`col` и `row` — координаты **нового** ферзя, которого мы хотим поставить.
`c` — переменная цикла, которая обозначает **столбцы слева** от нашего текущего (мы проверяем только те столбцы, где ферзи уже стоят, от `0` до `col - 1`).
`r` — строка, на которой стоит старый ферзь в проверочном столбце `c` (значение берется из `board[c]`).
`board` — текущее состояние доски с уже расставленными ферзями.
`col` — номер **текущего столбца**, в который мы прямо сейчас пытаемся поставить ферзя (идет от 0 до 7).
`row` — переменная в цикле, которая означает **номер строки** (от 1 до 8), куда мы пробуем поставить ферзя.
`pos` — временная переменная в цикле вывода, обозначающая позицию конкретного ферзя в массиве.
короче с этим разберемся потом

