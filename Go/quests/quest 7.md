Write a function that takes an `int` min and an `int` max as parameters. The function should return a slice of `int`s with all the values between the min and max.
Min is included, and max is excluded.
If min is greater than or equal to max, a `nil` slice is returned.
`make` is not allowed for this exercise.
```go
func AppendRange(min, max int) []int {
	if min >= max {
		return nil
	}
	
	var result []int
	for i := min; i < max; i++ {
		result = append(result, i)
	}
	
	return result
}

`func main() { 
	fmt.Println(piscine.AppendRange(5, 10)) 
	fmt.Println(piscine.AppendRange(10, 5)) 
}`

And its output :

`$ go run . 
[5 6 7 8 9] 
[] 
$`
```

### 1. Что такое `nil` срез и динамическое добавление через `append`?
- Переменная `var result []int` создаёт срез без выделения фиксированного размера в памяти. До добавления первого элемента такой срез равен `nil` (пустота).
- Если условие `min >= max` истинно (например, `min = 10, max = 5`), функция сразу возвращает `nil`. При печати через `fmt.Println` такой срез отображается как пустые скобки `[]`.
- Функция `append(result, i)` автоматически расширяет срез в оперативной памяти и дописывает число `i` в самый конец.

### 2. Границы диапазона: включительно и исключительно
- `min` входит в диапазон, поэтому цикл стартует строго с `i := min`.
- `max` не входит, поэтому условие строгое: `i < max` (на числе `max` цикл останавливается).

### Итерации:
Вызов `AppendRange(5, 10)`:
`min = 5`, `max = 10`. Проверка `5 >= 10` ложна $\rightarrow$ идём в цикл.
- `i = 5`: `result = append([], 5)` $\rightarrow$ `[5]`
- `i = 6`: `result = append([5], 6)` $\rightarrow$ `[5, 6]`
- `i = 7`: `result = append([5, 6], 7)` $\rightarrow$ `[5, 6, 7]`
- `i = 8`: `result = append([5, 6, 7], 8)` $\rightarrow$ `[5, 6, 7, 8]`
- `i = 9`: `result = append([5, 6, 7, 8], 9)` $\rightarrow$ `[5, 6, 7, 8, 9]`
- `i = 10`: условие `10 < 10` ложно $\rightarrow$ выход из цикла.
Функция возвращает срез `[5, 6, 7, 8, 9]`.


[makerange](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-07/makerange?event=1081)
Write a function that takes an `int` min and an `int` max as parameters. The function must return a slice of `int`s with all the values between min and max.
Min is included, and max is excluded.
If min is greater than or equal to max, a `nil` slice is returned.
`append` is not allowed for this exercise
```go
func MakeRange(min, max int) []int {
	if min >= max {
		return nil
	}
	
	size := max - min
	result := make([]int, size)
	
	for i := 0; i < size; i++ {
		result[i] = min + i
	}
	
	return result
}

`func main() { 
	fmt.Println(piscine.MakeRange(5, 10)) 
	fmt.Println(piscine.MakeRange(10, 5)) 
}`

And its output :

`$ go run . 
[5 6 7 8 9] 
[] 
$`
```

### 1. Чем `make` отличается от `append` «под капотом»?
В предыдущей задаче мы использовали `append`, который не знает финального размера среза и при нехватке памяти вынужден заново выделять кусок побольше и перекопировать элементы.
В задаче `MakeRange` функция `append` **запрещена**.
Мы используем встроенную функцию `make`:
1. Вычисляем точное количество будущих чисел: `size := max - min` (для 5 и 10 это $10 - 5 = 5$ ячеек).
2. Вызываем `make([]int, size)`: Go сразу одним запросом резервирует непрерывный массив ровно на 5 ячеек, заполненный нулями `[0, 0, 0, 0, 0]`.
3. Поскольку все ячейки уже созданы, мы не дописываем в конец, а напрямую записываем значения по индексу: `result[i] = min + i`.

### Итерации:
Вызов `MakeRange(5, 10)`:
`size = 10 - 5 = 5`.
`result` создан через `make`: `[0, 0, 0, 0, 0]`.

| Шаг цикла `i` | Формула `min + i` | В какую ячейку пишем | Состояние среза `result` |
| :---: | :---: | :---: | :--- |
| `0` | $5 + 0 = 5$ | `result[0] = 5` | `[5, 0, 0, 0, 0]` |
| `1` | $5 + 1 = 6$ | `result[1] = 6` | `[5, 6, 0, 0, 0]` |
| `2` | $5 + 2 = 7$ | `result[2] = 7` | `[5, 6, 7, 0, 0]` |
| `3` | $5 + 3 = 8$ | `result[3] = 8` | `[5, 6, 7, 8, 0]` |
| `4` | $5 + 4 = 9$ | `result[4] = 9` | `[5, 6, 7, 8, 9]` |

Конец цикла (`i = 5 < 5` ложно). Функция возвращает `[5, 6, 7, 8, 9]`.


[concatparams](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-07/concatparams?event=1081)
Write a function that takes the arguments received in parameters and returns them as a `string`. The `string` is the result of all the arguments concatenated with a newline (`\n`) between.
```go
func ConcatParams(args []string) string {
	if len(args) == 0 {
		return ""
	}
	
	result := ""
	for i, s := range args {
		if i > 0 {
			result += "\n"
		}
		result += s
	}
	
	return result
}

`func main() { 
	test := []string{"Hello", "how", "are", "you?"}
	 fmt.Println(piscine.ConcatParams(test)) 
}`

And its output :

`$ go run . 
Hello 
how 
are 
you? 
$`
```

### Разбор логики разделителя переноса строки `\n`
Задача требует соединить все слова из среза `args` через перенос строки `"\n"`, но так, чтобы в самом конце лишнего переноса строки не было.
- Проверка `if len(args) == 0` защищает от пустого входного среза.
- Условие `if i > 0`: для самого первого слова с индексом `i = 0` перенос строки не добавляется.
- Для каждого следующего слова (`i = 1, 2, ...`) мы сначала приклеиваем `"\n"`, а затем само слово `s`. В итоге `"\n"` всегда оказывается строго **между** словами.

### Итерации:
Вызов `ConcatParams([]string{"Hello", "how", "are"})`:
- До цикла: `result = ""`
- `i = 0`, `s = "Hello"`: `i > 0` ложно $\rightarrow$ `result = "" + "Hello"` = `"Hello"`
- `i = 1`, `s = "how"`: `i > 0` истинно $\rightarrow$ `result = "Hello" + "\n" + "how"` = `"Hello\nhow"`
- `i = 2`, `s = "are"`: `i > 0` истинно $\rightarrow$ `result = "Hello\nhow" + "\n" + "are"` = `"Hello\nhow\nare"`
- Конец цикла. Возвращает строку `"Hello\nhow\nare"`.


[splitwhitespaces](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-07/splitwhitespaces?event=1081)
Write a function that separates the words of a `string` and puts them in a `string slice`.
The separators are spaces, tabs and newlines.
```go
func isWhiteSpace(r rune) bool {
	return r == ' ' || r == '\t' || r == '\n'
}

func SplitWhiteSpaces(s string) []string {
	var result []string
	word := ""
	
	for _, r := range s {
		if isWhiteSpace(r) {
			if len(word) > 0 {
				result = append(result, word)
				word = ""
			}
		} else {
			word += string(r)
		}
	}
	
	if len(word) > 0 {
		result = append(result, word)
	}
	
	return result
}

`func main() { 
	fmt.Printf("%#v\n", piscine.SplitWhiteSpaces("Hello how are you?")) 
}`

And its output :

`$ go run . 
[]string{"Hello", "how", "are", "you?"} 
$`
```

### 1. Как работает буфер слова (`word`) при разборе строки?
Переменная `word := ""` работает как временный контейнер:
- Пока идут обычные буквы, мы складываем их в буфер: `word += string(r)`.
- Как только натыкаемся на разделитель (пробел, табуляция `\t` или перенос строки `\n`), слово закончилось. Мы сбрасываем накопленное слово в срез: `result = append(result, word)` и очищаем буфер `word = ""`.

### 2. Зачем две проверки `if len(word) > 0`?
1. **Внутри цикла при встрече разделителя:**  
   Если в тексте идут несколько пробелов подряд (например, `"Hello    World"`), при встрече второго и третьего пробелов буфер `word` пустой (`len == 0`). Проверка `len(word) > 0` защищает срез от попадания пустых слов `""`.
2. **После завершения цикла:**  
   Самое последнее слово в строке обычно не заканчивается пробелом (например, слово `"you?"` в `"Hello how are you?"`). Когда цикл доходит до конца строки, последнее слово всё ещё лежит в буфере `word`. Финальный `if len(word) > 0` забирает этот остаток и добавляет в результат.

### Итерации:
Строка `s = "Hi Go"`:

| Символ `r` | `isWhiteSpace` | Буфер `word` до шага | Действие | Буфер `word` после | Содержимое `result` |
| :---: | :---: | :---: | :--- | :---: | :--- |
| `'H'` | `false` | `""` | Добавляем букву | `"H"` | `[]` |
| `'i'` | `false` | `"H"` | Добавляем букву | `"Hi"` | `[]` |
| `' '` | `true` | `"Hi"` | `len > 0` истинно $\rightarrow$ сброс в срез | `""` | `["Hi"]` |
| `'G'` | `false` | `""` | Добавляем букву | `"G"` | `["Hi"]` |
| `'o'` | `false` | `"G"` | Добавляем букву | `"Go"` | `["Hi"]` |

Цикл завершён. В буфере `word` осталось `"Go"`.
Финальный блок: `len("Go") > 0` $\rightarrow$ `result = append(["Hi"], "Go")` $\rightarrow$ `["Hi", "Go"]`.


[printwordstables](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-07/printwordstables?event=1081)
Write a function that receives a `string slice` and prints each element of the slice in a seperate line.
```go
func PrintWordsTables(a []string) {
	for _, word := range a {
		for _, r := range word {
			z01.PrintRune(r)
		}
		z01.PrintRune('\n')
	}
}

`func main() { 
	a := piscine.SplitWhiteSpaces("Hello how are you?") 
	piscine.PrintWordsTables(a) 
}`

And its output :

`$ go run . 
Hello 
how 
are 
you? 
$`
```

### Разбор связи со `SplitWhiteSpaces`
Эта задача — логическое продолжение предыдущей. `SplitWhiteSpaces` нарезает строку на срез слов `[]string`, а `PrintWordsTables` принимает этот срез и выводит слова на экран по правилам бассейна (посимвольно через `z01.PrintRune`).
- Внешний цикл `for _, word := range a` берёт каждое слово по очереди.
- Внутренний цикл `for _, r := range word` печатает буквы этого слова.
- После каждого слова печатается `z01.PrintRune('\n')`.

### Итерации:
Входной срез `a = []string{"Hello", "how"}`:
- **Круг 1:** `word = "Hello"`. Внутренний цикл печатает `'H'`, `'e'`, `'l'`, `'l'`, `'o'`. Затем `'\n'`.
- **Круг 2:** `word = "how"`. Внутренний цикл печатает `'h'`, `'o'`, `'w'`. Затем `'\n'`.
- Конец выполнения.


[split](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-07/split?event=1081)
Write a function that receives a string and a separator and returns a `slice of strings` that results of splitting the string `s` by the separator `sep`.
```go
func Split(s, sep string) []string {
	var result []string
	n := len(sep)
	
	if n == 0 {
		for _, r := range s {
			result = append(result, string(r))
		}
		return result
	}
	
	start := 0
	for i := 0; i <= len(s)-n; {
		if s[i:i+n] == sep {
		result = append(result, s[start:i])
		i += n
		start = i
		} else {
			i++
		}
	}
	
	result = append(result, s[start:])
	return result
}


`func main() { 
	s := "HelloHAhowHAareHAyou?" 
	fmt.Printf("%#v\n", piscine.Split(s, "HA")) 
}`

And its output :

`$ go run . 
[]string{"Hello", "how", "are", "you?"} 
$`
```

### 1. Как разрезать строку по многосимвольному разделителю?
В отличие от простых пробелов, разделитель `sep` может состоять из нескольких букв (например, `"HA"`, длина `n = 2`).
Поэтому мы управляем шагом цикла вручную:
```go
for i := 0; i <= len(s)-n; {
```
Заметь: в заголовке цикла **нет `i++`**! Шаг зависит от того, что мы нашли:
- Мы смотрим на срез длины разделителя: `s[i : i+n]`.
- **Если совпало с `sep`:** мы нашли границу слова! Берём кусок от предыдущей метки `start` до текущего индекса `i`: `s[start:i]`, добавляем в `result`.  
  Затем перепрыгиваем через весь разделитель: `i += n` и сдвигаем метку начала следующего слова: `start = i`.
- **Если не совпало:** сдвигаемся всего на один символ вперёд: `i++`.

### 2. Захват финального остатка
После выхода из цикла в строке остаётся последнее слово (начиная с метки `start` до конца строки `len(s)`). Строка `result = append(result, s[start:])` забирает этот хвост.

### Итерации:
Строка `s = "HiHAhow"`, разделитель `sep = "HA"` (`n = 2`). Длина `s = 7`.
Граница цикла: `i <= 7 - 2 = 5`.
`start = 0`.

- `i = 0`: `s[0:2] = "Hi" != "HA"` $\rightarrow$ `i++` (стал `1`).
- `i = 1`: `s[1:3] = "iH" != "HA"` $\rightarrow$ `i++` (стал `2`).
- `i = 2`: `s[2:4] = "HA" == "HA"` $\rightarrow$ совпало!
  - Добавляем кусок `s[start:i] = s[0:2] = "Hi"` в `result` $\rightarrow$ `["Hi"]`.
  - Прыжок через разделитель: `i += 2` (стал `4`).
  - Новая метка: `start = 4`.
- `i = 4`: `s[4:6] = "ho" != "HA"` $\rightarrow$ `i++` (стал `5`).
- `i = 5`: `s[5:7] = "ow" != "HA"` $\rightarrow$ `i++` (стал `6`).
- `i = 6`: условие `6 <= 5` ложно $\rightarrow$ выход из цикла.
- **Хвост:** `s[start:] = s[4:] = "how"`.
  - `result = append(["Hi"], "how")` $\rightarrow$ `["Hi", "how"]`.


[convertbase](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-07/convertbase?event=1081)
Write a function that receives three arguments:
- `nbr`: A string representing a numberic value in a [base](https://simple.wikipedia.org/wiki/Base_\(mathematics\)).
    
- `baseFrom`: A string representing the base `nbr` it's using.
    
- `baseTo`: A string representing the base `nbr` should be represented in the returned value.
Only valid bases will be tested.
Negative numbers will not be tested.
```go
func ConvertBase(nbr, baseFrom, baseTo string) string {
	baseFromLen := len(baseFrom)
	baseToLen := len(baseTo)
	
	val := 0
	for _, r := range nbr {
		digit := -1
		for i, b := range baseFrom {
			if r == b {
				digit = i
				break
			}
		}
		val = val*baseFromLen + digit
	}
	
	if val == 0 {
		return string(baseTo[0])
	}
	
	result := ""
	for val > 0 {
		rem := val % baseToLen
		result = string(baseTo[rem]) + result
		val /= baseToLen
	}
	
	return result
}


`func main() { 
	result := piscine.ConvertBase("101011", "01", "0123456789") 
	fmt.Println(result) 
}`

And its output :

`$ go run . 
43 
$`
```

### 1. Архитектура решения: Мост через десятичное число (`val`)
Перевести число напрямую из одной произвольной базы в другую математически сложно.
Поэтому алгоритм разбивается на **два понятных этапа**:
1. **Этап 1 (`baseFrom` $\rightarrow$ `int`):** Считываем строку `nbr` и превращаем её в обычное целое число `val` (как в `AtoiBase`).
   - Ищем символ `r` в алфавите `baseFrom`. Его позиция `i` — это значение разряда `digit`.
   - Накапливаем: `val = val * baseFromLen + digit`.
2. **Этап 2 (`int` $\rightarrow$ `baseTo`):** Переводим полученное число `val` в новую систему `baseTo`.

### 2. Как развернуть цифры без рекурсии: Склейка слева
Когда мы делим число на основание новой базы `rem := val % baseToLen`, мы получаем цифры **с конца (младшие разряды)**.
Вместо вызова рекурсии используется простая конкатенация строк:
```go
result = string(baseTo[rem]) + result
```
Новый символ `string(baseTo[rem])` приклеивается **СЛЕВА** от уже накопленной строки `result`.
В результате старшие разряды автоматически оказываются впереди, и строка получается в правильном порядке без разворота!

### Итерации:
Вызов `ConvertBase("101", "01", "0123456789")`:
`baseFrom = "01"` (`длина 2`), `baseTo = "0123456789"` (`длина 10`).

- **Этап 1: перевод `"101"` в десятичное число `val`:**
  - Символ `'1'`: индекс в `"01"` равен `1` $\rightarrow$ `val = 0 * 2 + 1 = 1`.
  - Символ `'0'`: индекс в `"01"` равен `0` $\rightarrow$ `val = 1 * 2 + 0 = 2`.
  - Символ `'1'`: индекс в `"01"` равен `1` $\rightarrow$ `val = 2 * 2 + 1 = 5`.
  - Итог этапа 1: `val = 5`.

- **Этап 2: перевод `val = 5` в `baseTo`:**
  - `val = 5 > 0`:
    - `rem = 5 % 10 = 5`.
    - Символ `baseTo[5] = '5'`.
    - `result = "5" + "" = "5"`.
    - `val = 5 / 10 = 0`.
  - Цикл завершён.

Функция возвращает строку `"5"`. Для примера из условия `"101011"` в двоичной системе результат равен `"43"`.
