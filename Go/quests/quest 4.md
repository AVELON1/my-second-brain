[fibonacci](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-04/fibonacci?event=1081)
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


