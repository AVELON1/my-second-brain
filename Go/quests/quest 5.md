[firstrune](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-05/firstrune?event=1081)
Write a function that returns the first `rune` of a `string`.
```go
func FirstRune(s string) rune { 
	return []rune(s)[0]
}

func main() { 
	z01.PrintRune(piscine.FirstRune("Hello!")) 
	z01.PrintRune(piscine.FirstRune("Salut!")) 
	z01.PrintRune(piscine.FirstRune("Ola!")) 
	z01.PrintRune('\n') 
}

$ go run . 
HSO 
$
```

[lastrune](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-05/lastrune?event=1081)
Write a function that returns the last `rune` of a `string`.
```go
func FirstRune(s string) rune { 
	r = []rune(s)
	return r[len(r)-1]
}

func main() { 
	z01.PrintRune(piscine.FirstRune("Hello!")) 
	z01.PrintRune(piscine.FirstRune("Salut!")) 
	z01.PrintRune(piscine.FirstRune("Ola!")) 
	z01.PrintRune('\n') 
}

$ go run . 
!!! 
$
```
- `string` — строка;
- `rune` — один символ Unicode.
-
Запись `[]rune` — это **тип среза рун**. Срез — это коллекция элементов, похожая на массив, но с гибким размером.
``var letters []rune``
Здесь `letters` — переменная, которая может хранить несколько рун.
А вот так мы преобразуем строку в срез рун:
``letters := []rune("кот")
Можно мысленно читать так: «преобразовать строку `"кот"` в список рун».
После этого:
``letters[0] // 'к'
``letters[1] // 'о'
``letters[2] // 'т'
Индексы начинаются с нуля.
Важно: `[]rune` — это именно **срез**, а не массив. В обычном разговоре их легко спутать, но для этой задачи запомни: `[]rune(s)` превращает строку `s` в срез рун.

[nrune](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-05/nrune?event=1081)
Write a function that returns the nth `rune` of a `string`. If not possible, it returns `0`.
```go
func NRune(s string, n int) rune {
	runes := []rune(s)
	if n < 1 || n > len(runes) { //проверяет находится ли индекс в пределах длины среза
		return 0
	}
	return runes[n-1] // Возвращаем руну по индексу (n - 1), так как в Go индексация с 0)
}

func main() { 
	z01.PrintRune(piscine.NRune("Hello!", 3)) 
	z01.PrintRune(piscine.NRune("Salut!", 2)) 
	z01.PrintRune(piscine.NRune("Bye!", -1)) 
	z01.PrintRune(piscine.NRune("Bye!", 5)) 
	z01.PrintRune(piscine.NRune("Ola!", 4)) 
	z01.PrintRune('\n') }
}

$ go run . 
la! 
$
```

[compare](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-05/compare?event=1081)
Write a function that behaves like the `Compare` function.
```go
func Compare(a, b string) int {
	if a == b {
		return 0
	}
	if a < b {
		return -1
	}
	return 1
}

func main() { 
	fmt.Println(piscine.Compare("Hello!", "Hello!")) 
	fmt.Println(piscine.Compare("Salut!", "lut!")) 
	fmt.Println(piscine.Compare("Ola!", "Ol")) 
}

$ go run . 
0 
-1 
1 
$
```
Сравниваются **не только первые символы**, а символы по порядку — пока не найдётся первое различие.
Например:
"Salut!" и "lut!"
Сразу различаются первые символы: `'S'` и `'l'`. На этом сравнение заканчивается.
А вот:
"Ola!" и "Ol"
Сначала совпадают `'O'` и `'l'`. Потом строка `"Ol"` заканчивается, а в `"Ola!"` есть ещё символы. Поэтому `"Ol"` меньше `"Ola!"`.
Если бы строки начинались одинаково, например `"Hello"` и `"Help"`, сравнивали бы дальше: `H = H`, `e = e`, затем `l = l`, а после — `l < p`. Значит, `"Hello" < "Help"`.


[alphacount](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-05/alphacount?event=1081)
Write a function that counts the letters of a string and returns the count.
The letters are from the Latin alphabet list only, any other characters, symbols or empty spaces shall not be counted.

```go
func AlphaCount(s string) int { 
	count:=0
	for _, r := range s {
		if (r >= 'a' && r <= 'z') || (r >= 'A' && r <= 'Z') {
			count++
		)
	}
	return count
}

func main() { 
	s := "Hello 78 World! 4455 /" 
	nb := piscine.AlphaCount(s) 
	fmt.Println(nb) 
}

$ go run . 
10 
$
```


[index](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-05/index?event=1081)
Write a function that behaves like the `Index` function.
```go
func Index(s string, toFind string) int {
	lenS := len(s)
	lenF := len(toFind)
	
	if lenF == 0 {
		return 0
	}
	if lenF > lenS {
		return -1
	}
	
	for i := 0; i <= lenS-lenF; i++ {
		if s[i:i+lenF] == toFind { //Потому что lenF — это сколько символов мы хотим взять, а `i` — с какой позиции начать.
			return i
		}
	}
	return -1
}

func main() { 
	fmt.Println(piscine.Index("Hello!", "l")) 
	fmt.Println(piscine.Index("Salut!", "alu")) 
	fmt.Println(piscine.Index("Ola!", "hOl")) 
}

$ go run . 
2 
1 
-1 
$
```
- **Что искать?** Строку `toFind` внутри строки `s`.
- **Что вернуть, если нашли?** Позицию, с которой начинается совпадение.
- **Что вернуть, если не нашли?** `-1`, как в примере.

 Как проверять каждую позицию?
Например, в `"Salut!"` ищем `"alu"`. Длина `"alu"` — `3`.
Проверяем кусочки длиной 3:
позиция 0: "Sal" — не подходит 
позиция 1: "alu" — нашли! вернуть 1

[concat](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-05/concat?event=1081)
Write a function that returns the concatenation of two `string` passed in arguments.
```go
решение 1
func Concat(str1 string, str2 string) string { 
	return str1 + str2
}
решение 2
func Concat(str1 string, str2 string) string {
    result := append([]byte(str1), []byte(str2)...)
    return string(result)
} 
// можно использовать append, но для этой задачи это лишнее. append добавляет элементы в срез, а не прямо в строку 
// 1. `[]byte(str1)` превращает первую строку в срез байтов.
// 2. `[]byte(str2)` превращает вторую строку в срез байтов.
// 3. `...` передаёт байты второй строки в `append` по одному.


package main import ( "fmt" "piscine" ) func main() { 
	fmt.Println(piscine.Concat("Hello!", " How are you?")) 
}

$ go run . 
Hello! How are you? 
$
```


[isupper](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-05/isupper?event=1081)
Write a function that returns `true` if the `string` passed as parameter contains only uppercase characters, otherwise, returns `false`.
```go
func IsUpper(s string) bool {
	for _, r := range s {
		if r < 'A' || r > 'Z' {
			return false
		}
	}
	return true
}

альтернатива:
import "unicode"

func IsUpper(s string) bool {
	for _, r := range s {
		if !unicode.IsUpper(r) {
			return false
		}
	}
	return true
}


func main() { 
	fmt.Println(piscine.IsUpper("HELLO")) 
	fmt.Println(piscine.IsUpper("HELLO!")) 
}

$ go run . 
true 
false 
$
```


[islower](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-05/islower?event=1081)
Write a function that returns `true` if the `string` passed as parameter contains only lowercase characters, otherwise, returns `false`.
```go
func IsLower(s string) bool {
	for _, r := range s {
		if r < 'a' || r > 'a' {
			return false
		}
	}
	return true
}

func main() { 
	fmt.Println(piscine.IsUpper("hello")) 
	fmt.Println(piscine.IsUpper("hello!")) 
}

$ go run . 
true 
false 
$
```



[isalpha](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-05/isalpha?event=1081)
Write a function that returns `true` if the `string` passed as the parameter only contains alphanumerical characters or is empty, otherwise, and returns `false`.
```go
func IsAlpha(s string) bool {
	for _, r := range s {
		if !((r >= 'a' && r <= 'z') || (r >= 'A' && r <= 'Z') || (r >= '0' && r <= '9')) {
		return false
		}
	}
	return true
}


func main() { 
	fmt.Println(piscine.IsAlpha("Hello! How are you?"))
	 fmt.Println(piscine.IsAlpha("HelloHowareyou")) 
	 fmt.Println(piscine.IsAlpha("What's this 4?")) 
	 fmt.Println(piscine.IsAlpha("Whatsthis4")) 
}

$ go run . 
false 
true 
false 
true 
$
```


[isnumeric](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-05/isnumeric?event=1081)
Write a function that returns `true` if the `string` passed as a parameter contains only numerical characters, otherwise, returns `false`.
```go
func IsNumeric(s string) bool {
	for _, r := range s {
		if r < '0' || r > '9' {
			return false
		}
	}
	return true
}


func main() { 
	fmt.Println(piscine.IsNumeric("010203")) 
	fmt.Println(piscine.IsNumeric("01,02,03")) 
}

$ go run . 
true 
false 
$
```


[isprintable](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-05/isprintable?event=1081)
Write a function that returns `true` if the `string` passed as a parameter contains only printable characters, otherwise, returns `false`.

```go
func IsPrintable(s string) bool {
	for _, r := range s {
		if r < 32 || r > 126 {
			return false
		}
	}
	return true
}


func main() { 
	fmt.Println(piscine.IsPrintable("Hello"))
	fmt.Println(piscine.IsPrintable("Hello\n")) 
}

$ go run . 
true 
false 
$
```

[toupper](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-05/toupper?event=1081)
Write a function that capitalizes each letter in a `string`.
```go
func ToUpper(s string) string {
	runes := []rune(s)
	for i, r := range runes {
		if r >= 'a' && r <= 'z' {
			runes[i] = r - ('a' - 'A') //или r - 32
		}
	}
	return string(runes)
}

`func main() { 
	fmt.Println(piscine.ToUpper("Hello! How are you?")) 
}`

And its output :

`$ go run . 
HELLO! HOW ARE YOU? 
$`
```
Это выражение вычисляет **число**, на которое нужно «сдвинуть» строчную букву, чтобы получить заглавную:
r - ('a' - 'A')
Для английских букв разница между `'a'` и `'A'` равна `32`. Поэтому выражение по сути такое:
r - 32
Например, если `r` — это `'b'`:
'b' = 98
'a' = 97
'A' = 65
'b' - ('a' - 'A')
= 98 - (97 - 65)
= 98 - 32
= 66
= 'B'

[tolower](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-05/tolower?event=1081)
Write a function that lower cases for each letter in a `string`.
```go
func ToLower(s string) string {
	runes := []rune(s)
	for i, r := range runes {
		if r >= 'a' && r <= 'z' {
			runes[i] = r + ('a' - 'A') //или r + 32
		}
	}
	return string(runes)
}

`func main() { 
	fmt.Println(piscine.ToUpper("Hello! How are you?")) 
}`

And its output :

`$ go run . 
hello! how are you?
$`
```


[printnbrinorder](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-05/printnbrinorder?event=1081)
Write a function which prints the digits of an `int` passed in parameter in ascending order. All possible values of type `int` have to go through, excluding negative numbers. Conversion to `int64` is not allowed.
```go
import "github.com/01-edu/z01"
  

func PrintNbrInOrder(n int) {
	if n < 0 {
		return
	}
	if n == 0 { // Ноль — особый случай. Если применить к нему цикл ниже, цикл не запустится, и ничего не напечатается. Поэтому `0` выводим отдельно и сразу заканчиваем функцию.
		z01.PrintRune('0')
		return
	}
	
	var count [10]int /*Создаётся массив из 10 счётчиков — по одному для каждой цифры от `0` до `9`. Изначально все значения равны нулю: 
	индекс: 0 1 2 3 4 5 6 7 8 9 
	count:  0 0 0 0 0 0 0 0 0 0 
	Это значит: цифра `1` встретилась один раз, `2` — один раз, `3` — один раз.*/
	for n > 0 {
		count[n%10]++
		n /= 10
	}
	// Внешний цикл проверяет цифры по порядку: `0`, `1`, `2`, …, `9`. Внутренний цикл печатает каждую цифру столько раз, сколько она встретилась. Для `321` он сначала напечатает цифру `1`, потом `2`, потом `3`. Получится `123`.
	for digit := 0; digit < 10; digit++ {//печать по возрастанию(цель этой части)
		for i := 0; i < count[digit]; i++ {
			z01.PrintRune(rune('0' + digit))
		}
	}
}


`func main() { 
	piscine.PrintNbrInOrder(321) 
	piscine.PrintNbrInOrder(0) 
	piscine.PrintNbrInOrder(321) 
}`

And its output :

`$ go run . | cat -e 
1230123$ 
$`
```

Операция `% 10` получает последнюю цифру числа. Деление на `10` без остатка убирает последнюю цифру.
Для `321`:

|Шаг|`n % 10` — последняя цифра|Что считаем|`n /= 10` — что останется|
|--:|--:|---|--:|
|1|1|Увеличиваем счётчик цифры `1`|32|
|2|2|Увеличиваем счётчик цифры `2`|3|
|3|3|Увеличиваем счётчик цифры `3`|0|

Когда `n` становится `0`, цикл заканчивается. Все цифры исходного числа уже посчитаны.
почему мы ничего пишем после return?
потому что 
func PrintNbrInOrder(n int)
После `)` нет типа результата: функция ничего не возвращает, а только печатает. Поэтому ей нечего возвращать. В другой функции, например `Index`, в конце написано `int`, значит она должна вернуть число — поэтому там встречается `return 0` или `return -1`.

`count` — массив из десяти счётчиков: по одному для каждой цифры от `0` до `9`. Сначала все счётчики равны нулю.
Цикл достаёт цифры из числа справа налево:

- `n % 10` получает последнюю цифру;
- `count[n%10]++` увеличивает счётчик этой цифры;
- `n /= 10` убирает последнюю цифру.

Например, для `n = 321` цикл найдёт сначала `1`, затем `2`, потом `3`. В конце `count` запомнит, что цифры `1`, `2` и `3` встретились по одному разу.

**Этот цикл только считает цифры. По порядку он их не печатает.**

**Внутренний цикл** печатает каждую цифру столько раз, сколько она встретилась. Например, если цифра `2` встретилась три раза, `count[2]` равно `3`, и цифра `2` будет напечатана трижды.