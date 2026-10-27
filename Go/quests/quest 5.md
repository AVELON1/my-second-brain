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
J
[nrune](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-05/nrune?event=1081)
Write a function that returns the nth `rune` of a `string`. If not possible, it returns `0`.
```go
func NRune(s string, n int) rune {
	runes := []rune(s)
	if n < 1 || n > len(runesu) { //проверяет находится ли индекс в пределах длины среза
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


[trimatoi](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-05/trimatoi?event=1081)
- Write a function that transforms numbers within a `string`, into an `int`.
- If the `-` sign is encountered before any number it should determine the sign of the returned `int`.
    
- This function should **only** return an `int`. In the case of an invalid input, the function should return `0`.
    
- **Note**: There will never be more than one sign in a `string` in the tests.

```go
func TrimAtoi(s string) int {
	res := 0
	sign := 1
	hasDigit := false
	
	for _, r := range s {
		if r >= '0' && r <= '9' {
			hasDigit = true
			res = res*10 + int(r-'0') //разряд + r-48
		} else if r == '-' && !hasDigit {{ /* Allow negative sign only if no digits have been encountered yet*/
			sign = -1
		}
	}
	
	return res * sign
}


func main() { 
	fmt.Println(piscine.TrimAtoi("12345")) 
	fmt.Println(piscine.TrimAtoi("str123ing45")) 
	fmt.Println(piscine.TrimAtoi("012 345")) 
	fmt.Println(piscine.TrimAtoi("Hello World!")) 
	fmt.Println(piscine.TrimAtoi("sd+x1fa2W3s4")) 
	fmt.Println(piscine.TrimAtoi("sd-x1fa2W3s4")) 
	fmt.Println(piscine.TrimAtoi("sdx1-fa2W3s4")) 
	fmt.Println(piscine.TrimAtoi("sdx1+fa2W3s4")) 
}


$ go run . 12345 
12345 
12345 
0 
1234 
-1234 
1234 
1234 
$
```

### Разбор логики и флага `hasDigit`
Главное отличие от обычного `Atoi`: любые посторонние символы (буквы, пробелы, плюс) не сбрасывают функцию в `0`, а просто пропускаются.
Но знак минус `'-'` имеет строгое правило: он учитывается **только если встретился ДО первой цифры**.

Для этого введён флаг-замок `hasDigit := false`:
1. Пока цифр не было, `hasDigit` равен `false`. Если встретился `'-'`, ветка `else if r == '-' && !hasDigit` делает `sign = -1`.
2. Как только встретилась первая цифра, мы ставим `hasDigit = true`.
3. Если после этого в строке встретится ещё один минус (как в `"sdx1-fa2"`), условие `!hasDigit` будет ложным, и этот минус просто проигнорируется!

### Итерации на граничных случаях:

1. **Строка `"sd-x1fa2"` (минус ДО цифр):**
   - Символы `'s'`, `'d'`: не цифры, не минус $\rightarrow$ пропуск. `hasDigit` всё ещё `false`.
   - Символ `'-'`: `hasDigit` равен `false` $\rightarrow$ `sign = -1`.
   - Символ `'1'`: цифра $\rightarrow$ `hasDigit = true`, `res = 0*10 + 1 = 1`.
   - Символы `'f'`, `'a'`: пропуск.
   - Символ `'2'`: цифра $\rightarrow$ `res = 1*10 + 2 = 12`.
   - Итог: `res * sign = 12 * -1 = -12`.

2. **Строка `"sdx1-fa2"` (минус ПОСЛЕ цифр):**
   - Символы `'s'`, `'d'`: пропуск.
   - Символ `'1'`: первая цифра $\rightarrow$ `hasDigit = true`, `res = 1`.
   - Символ `'-'`: проверяем `!hasDigit`. Но `hasDigit` уже `true`! Значит, условие ложно, минус игнорируется!
   - Символ `'2'`: цифра $\rightarrow$ `res = 1*10 + 2 = 12`.
   - Итог: `res * sign = 12 * 1 = 12`.




[capitalize](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-05/capitalize?event=1081)
Write a function that capitalizes the first letter of each word **and** lowercases the rest.
A word is a sequence of **alphanumeric** characters.
```go
func isAlphaNum(r rune) bool {
	return (r >= 'a' && r <= 'z') || (r >= 'A' && r <= 'Z') || (r >= '0' && r <= '9') //alphanumerical condition
}

func Capitalize(s string) string {
	runes := []rune(s)
	newWord := true
	
	for i, r := range runes {
		if isAlphaNum(r) {
			if newWord /* Это первый символ слова*/{
				if r >= 'a' && r <= 'z' {
					runes[i] = r - ('a' - 'A') //r-32
				}
				newWord = false
			} else /* Это не первый символ слова*/{
				if r >= 'A' && r <= 'Z' {
					runes[i] = r + ('a' - 'A') //r+32=
				}
			}
		} else {
			newWord = true
		}
	}
	
	return string(runes)
}


`func main() { 
	fmt.Println(piscine.Capitalize("Hello! How are you? How+are+things+4you?")) 
}`

And its output :

`$ go run . 
Hello! How Are You? How+Are+Things+4you? 
$`
```
`newWord` сначала равен `true`:
newWord := true
Это значит: «Мы пока не встретили символ текущего слова». Поэтому первый буквенно-цифровой символ строки считается началом слова.
Если символ — буква или цифра, функция смотрит на `newWord`:
- `true` — это первый символ слова;
- `false` — мы уже внутри слова.
Если символ **не** буква и **не** цифра — например, пробел, `!`, `?` или `+` — слово закончилось. Функция снова ставит `newWord = true`. Следующий буквенно-цифровой символ станет началом нового слова.
1. В начале `newWord == true`. Первый символ — `H`, это буква. Значит, это начало слова. `H` уже заглавная, менять её не нужно. Затем `newWord` становится `false`.
2. Символы `e`, `l`, `l`, `o` — всё ещё часть того же слова. Они не первые.
3. Символ `!` — не буква и не цифра. Слово закончилось, поэтому `newWord` снова становится `true`.
4. После пробела начинается `How`. Буква `H` — первый символ слова, а значит, она заглавная. Остальные буквы слова становятся строчными.
5. Пробел снова устанавливает `newWord = true`. Поэтому `a` в слове `are` будет заглавной: получится `Are`.

Так происходит для всей строки. Символ `+`, как и пробел, разделяет слова, поэтому после него следующая буква тоже считается первой:
How+are+things
превращается в:
How+Are+Things
|№|Символ|`newWord` до|Что делает программа|`newWord` после|
|0|пробел|`true`|Это не буква и не цифра. Слово ещё не началось.|`true`|
|1|`H`|`true`|Это первая буква слова. Она уже заглавная, поэтому остаётся `H`.|`false`|
|2|`o`|`false`|Не первая буква слова. Она уже строчная, остаётся `o`.|`false`|
|3|`w`|`false`|Не первая буква слова. Остаётся `w`.|`false`|
|4|пробел|`false`|Это разделитель, значит, следом может начаться новое слово.|`true`|
|5|`a`|`true`|Первая буква слова. Она строчная, превращается в `A`.|`false`|
|6|`r`|`false`|Не первая буква. Остаётся `r`.|`false`|
|7|`e`|`false`|Не первая буква. Остаётся `e`.|`false`|
|8|пробел|`false`|Разделитель — следующее слово начнётся заново.|`true`|
|9|`y`|`true`|Первая буква слова. Строчная `y` превращается в `Y`.|`false`|
|10|`o`|`false`|Не первая буква. Остаётся `o`.|`false`|
|11|`u`|`false`|Не первая буква. Остаётся `u`.|`false`|
|12|`?`|`false`|Это не буква и не цифра, поэтому отмечаем начало нового слова.|`true`|
|13|пробел|`true`|Это тоже разделитель. `newWord` остаётся `true`.|`true`|

Изменились только `a` → `A` и `y` → `Y`:
" How Are You? "


[basicjoin](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-05/basicjoin?event=1081)
Write a function that returns a concatenated `string` from the 'strings' passed as arguments.
Функция получает несколько строк и должна соединить их в одну длинную строку.
```go
func BasicJoin(elems []string) string {
	res := ""
	for _, s := range elems {
		res += s
	}
	return res
}


`func main() { 
	elems := []string{"Hello!", " How", " are", " you?"} 
	fmt.Println(piscine.BasicJoin(elems)) 
}`

And its output :

`$ go run . 
Hello! How are you? 
$`
```
Начинаем с пустой строки: res := ""
Go понимает, что `res` — строка, потому что ей присвоено значение `""`.
Например, передаваемый срез:
[]string{"Hello!", " How", " are", " you?"}
содержит четыре строки.
`range elems` проходит по элементам среза один за другим.



11111111  1 11111111111111111111
[join](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-05/join?event=1081)
Write a function that returns the concatenation of all the `string`s of a slice of `string`s **separated** by the separator passed as the argument `sep`.
```go
func Join(strs []string, sep string) string {
	if len(strs) == 0 {
		return ""
	}
	
	res := strs[0]
	for i := 1; i < len(strs); i++ {
		res += sep + strs[i]
	}
	return res
}



`func main() { 
	toConcat := []string{"Hello!", " How", " are", " you?"} 
	fmt.Println(piscine.Join(toConcat, ":")) 
}`

And its output :

`$ go run . 
Hello!: How: are: you? 
$`
```

### Разбор логики разделителя без лишних условий
Как склеить список строк с разделителем `sep` так, чтобы он не появился перед первым словом и после последнего?
Простой приём:
1. Заранее забираем самое первое слово: `res := strs[0]`.
2. Цикл запускаем со **второго** элемента: `for i := 1; i < len(strs); i++`.
3. Внутри цикла сначала приклеиваем разделитель, а затем следующее слово: `res += sep + strs[i]`.
4. Если передан пустой срез `len(strs) == 0`, сразу возвращаем `""`.

### Итерации:
Вызов `Join([]string{"Hello!", "How", "are"}, ":")`:
- До цикла: `res = "Hello!"`
- `i = 1`: `strs[1] = "How"` $\rightarrow$ `res = "Hello!" + ":" + "How"` = `"Hello!:How"`
- `i = 2`: `strs[2] = "are"` $\rightarrow$ `res = "Hello!:How" + ":" + "are"` = `"Hello!:How:are"`
- Конец цикла. Итог: `"Hello!:How:are"`. Ни в начале, ни в конце лишнего `:` нет.


[printnbrbase](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-05/printnbrbase?event=1081)
Write a function that prints an `int` in a `string` base passed as parameters.
If the base is not valid, the function prints `NV` (Not Valid):
Validity rules for a base :
- A base must contain at least 2 characters.
    
- Each character of a base must be unique.
    
- A base should not contain `+` or `-` characters.
    
The function has to manage negative numbers. (as shown in the example)
```go
func isValidBase(b []rune) bool {
	if len(b) < 2 {
		return false
	}
	for i := 0; i < len(b); i++ {
		if b[i] == '+' || b[i] == '-' {
			return false
		}
		for j := i + 1; j < len(b); j++ {
			if b[i] == b[j] {
				return false
			}
		}
	}
	return true
}

func PrintNbrBase(nbr int, base string) {
	b := []rune(base)
	if !isValidBase(b) {
		z01.PrintRune('N')
		z01.PrintRune('V')
		return
	}
	
	baseLen := len(b)
	
	if nbr < 0 {
		z01.PrintRune('-')
		if nbr <= -baseLen {
			PrintNbrBasePos(-(nbr / baseLen), b, baseLen)
		}
		z01.PrintRune(b[-(nbr % baseLen)])
		return
	}
	
	PrintNbrBasePos(nbr, b, baseLen)
}

func PrintNbrBasePos(n int, b []rune, baseLen int) {
	if n >= baseLen {
		PrintNbrBasePos(n/baseLen, b, baseLen)
	}
	z01.PrintRune(b[n%baseLen])
}


`func main() { 
	piscine.PrintNbrBase(125, "0123456789") 
	z01.PrintRune('\n') 
	piscine.PrintNbrBase(-125, "01") 
	z01.PrintRune('\n') 
	piscine.PrintNbrBase(125, "0123456789ABCDEF") 
	z01.PrintRune('\n') 
	piscine.PrintNbrBase(-125, "choumi") 
	z01.PrintRune('\n') 
	piscine.PrintNbrBase(125, "aa") 
	z01.PrintRune('\n') 
}`

And its output :

`$ go run . 
125 
-1111101 
7D 
-uoi 
NV 
$`
```

### 1. Как работает произвольная система счисления?
Основание системы счисления — это просто длина алфавита `base` (`baseLen := len(b)`).
- В десятичной системе 10 цифр (`0..9`), поэтому делили на `10` и брали остаток `% 10`.
- В шестнадцатеричной (`"0123456789ABCDEF"`) длина равна `16`, поэтому делим на `16` и остаток `% 16` указывает на букву из строки базы.
- В выдуманной базе `"choumi"` длина `6`, символы: `c=0, h=1, o=2, u=3, m=4, i=5`. Делим на `6`, остаток берем как индекс `b[n % baseLen]`.

### 2. Валидация базы (`isValidBase`)
- `len(b) < 2`: в системе должно быть минимум 2 знака (как 0 и 1 в двоичной).
- `b[i] == '+' || b[i] == '-'`: знаки плюс и минус запрещены, иначе будет путаница со знаком числа.
- Проверка на дубликаты: вложенный цикл `for j := i + 1; j < len(b); j++` сравнивает каждый символ со всеми правее него. Если нашлись одинаковые знаки (как в `"aa"`), возвращает `false`, а функция печатает `NV`.

### 3. Обработка отрицательных чисел
Печатаем `'-'`, а остаток и деление берем с минусом `-(nbr % baseLen)`, что защищает от переполнения при минимальном числе `MinInt`.

### Итерации:
1. Вызов `PrintNbrBase(125, "0123456789ABCDEF")` (`baseLen = 16`):
   - Первый вызов: `125 >= 16` $\rightarrow$ рекурсивно вызываем `PrintNbrBasePos(125 / 16, b, 16)` с числом `7`.
   - Второй вызов для `7`: `7 >= 16` ложно $\rightarrow$ печатаем `b[7 % 16] = b[7] = '7'`. Завершение.
   - Возврат в первый вызов: печатаем младший остаток `b[125 % 16] = b[13] = 'D'`.
   - Итог: `7D`.

2. Вызов `PrintNbrBase(-125, "choumi")` (`baseLen = 6`):
   - Число отрицательное $\rightarrow$ печатает `'-'`.
   - `nbr <= -6` (-125 <= -6 истинно) $\rightarrow$ рекурсия для `-( -125 / 6 ) = 20`.
   - Внутри рекурсии для `20`: `20 >= 6` $\rightarrow$ рекурсия для `20 / 6 = 3`: печатает `b[3] = 'u'`.
   - Возврат: печатает `b[20 % 6 = 2] = 'o'`.
   - Возврат на самый верх: печатает остаток `b[ -( -125 % 6 ) = 5 ] = 'i'`.
   - Итог: `-uoi`.


[atoibase](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-05/atoibase?event=1081)
Write a function that takes two arguments:
- `s`: a numeric `string` in a given [base](https://simple.wikipedia.org/wiki/Base_\(mathematics\)).
    
- `base`: a `string` representing all the different digits that can represent a numeric value.
And return the integer value of `s` in the given `base`.
If the base is not valid it returns `0`.
Validity rules for a base :
- A base must contain at least 2 characters.
    
- Each character of a base must be unique.
    
- A base should not contain `+` or `-` characters.
String number must contain only elements that are in base.
Only valid `string` numbers will be tested.
The function **does not have** to manage negative numbers.
```go
func checkBase(b []rune) bool {
	if len(b) < 2 {
		return false
	}
	for i := 0; i < len(b); i++ {
		if b[i] == '+' || b[i] == '-' {
			return false
		}
		for j := i + 1; j < len(b); j++ {
			if b[i] == b[j] {
				return false
			}
		}
	}
	return true
}

func getIndex(r rune, b []rune) int {
	for i, char := range b {
		if char == r {
			return i
		}
	}
	return -1
}

func AtoiBase(s string, base string) int {
	baseRunes := []rune(base)
	if !checkBase(baseRunes) {
		return 0
	}
	
	baseLen := len(baseRunes)
	res := 0
	
	for _, r := range s {
		val := getIndex(r, baseRunes)
		if val == -1 {
			return 0
		}
		res = res*baseLen + val
	}
	return res
}


`func main() { 
	fmt.Println(piscine.AtoiBase("125", "0123456789")) 
	fmt.Println(piscine.AtoiBase("1111101", "01")) 
	fmt.Println(piscine.AtoiBase("7D", "0123456789ABCDEF")) 
	fmt.Println(piscine.AtoiBase("uoi", "choumi")) 
	fmt.Println(piscine.AtoiBase("bbbbbab", "-ab")) 
}`

And its output :

`$ go run . 
125 
125 
125 
125 
0 
$`
```

### Разбор логики AtoiBase
Это операция, строго обратная `PrintNbrBase`: мы принимаем строку цифр `s` в системе `base` и переводим её в десятичное число `int`.

1. **Функция `getIndex(r, b)`**:  
   Ищет символ `r` в алфавите `b`. Индекс найденного символа и есть его вес!  
   Например, в `"choumi"` символ `'c'` имеет вес `0`, а символ `'u'` имеет вес `3`. Если символа в базе нет — возвращает `-1`.
2. **Формула накопления разрядов**:  
   В обычном `Atoi` для десятичной системы мы делали `res = res*10 + val`.  
   Здесь вместо `10` мы умножаем на размер базы:  
   `res = res * baseLen + val`.

### Итерации:
Вызов `AtoiBase("uoi", "choumi")` (`baseLen = 6`):
Алфавит: `c=0, h=1, o=2, u=3, m=4, i=5`.
- До цикла: `res = 0`.
- Символ `'u'`: `getIndex('u') = 3` $\rightarrow$ `res = 0 * 6 + 3 = 3`.
- Символ `'o'`: `getIndex('o') = 2` $\rightarrow$ `res = 3 * 6 + 2 = 18 + 2 = 20`.
- Символ `'i'`: `getIndex('i') = 5` $\rightarrow$ `res = 20 * 6 + 5 = 120 + 5 = 125`.
- Конец строки. Функция возвращает `125`!


