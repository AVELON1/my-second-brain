
[printprogramname](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-06/printprogramname?event=1081)
Write a **program** that prints the name of the program.
```go
import (
	"os"
	
	"github.com/01-edu/z01"
)
  
func main() {
	arg := os.Args[0]
	start := 0
	for i, r := range arg {
		if r == '/' {
			start = i + 1
		}
	}
	name := arg[start:]
	for _, r := range name {
		z01.PrintRune(r)
	}
	z01.PrintRune('\n')
}

Example of output :

student/piscine/printprogramname$ go build main.go 
student/piscine/printprogramnane$ ./main 
main 
student/piscine/printprogramname$ go build 
student/piscine/printprogramname$ ./printprogramname | cat -e 
printprogramname$ 
student/piscine/printprogramname$ go build -o Nessy 
student/piscine/printprogramname$ ./Nessy 
Nessy 
student/piscine/printprogramname$
```

### 1. Что принципиально нового в Квесте 6?
До этого момента мы писали отдельные функции в пакете `piscine` (`package piscine`).
Начиная с Квеста 6, мы пишем **полноценные консольные программы** (`package main` с точкой входа `func main()`), которые запускаются из терминала и принимают параметры.

### 2. Как программа видит консоль? Пакет `os` и срез `os.Args`
Пакет `"os"` (Operating System) даёт доступ к функциям операционной системы.
Переменная `os.Args` — это срез строк (`[]string`), куда терминал автоматически складывает всё, что пользователь ввёл при запуске:
- В ячейке `os.Args[0]` **всегда** лежит путь к самой запущенной программе (например, `./main` или `/tmp/go-build123/b001/exe/Nessy`).
- В ячейках с `os.Args[1]` и дальше лежат аргументы, переданные пользователем.

### 3. Зачем цикл и поиск слэша `'/'`?
Терминал передаёт в `os.Args[0]` имя файла вместе с путём к папке: например, `./Nessy` или `/Users/student/piscine/Nessy`.
Нам нужно напечатать **только само имя файла** без пути папок:
1. Мы заводим индекс `start := 0`.
2. Цикл `for i, r := range arg` идёт по строке пути.
3. Каждый раз, когда встречается символ слэша `r == '/'`, мы запоминаем позицию следующего за ним символа: `start = i + 1`.
4. В итоге в `start` остаётся индекс первой буквы **после самого последнего слэша**.
5. Срез `name := arg[start:]` отрезает весь путь слева и оставляет только чистое имя.

### Итерации:
Запуск: `./Nessy`
Строка `arg = "./Nessy"` (длина 7):

| Индекс `i` | Символ `r` | Условие `r == '/'` | Переменная `start` | Что происходит |
| :---: | :---: | :---: | :---: | :--- |
| 0 | `.` | `false` | `0` | Пропуск |
| 1 | `/` | `true` | `1 + 1 = 2` | Нашли слэш! Имя начнётся с индекса 2 |
| 2 | `N` | `false` | `2` | Пропуск |
| 3 | `e` | `false` | `2` | Пропуск |
| 4 | `s` | `false` | `2` | Пропуск |
| 5 | `s` | `false` | `2` | Пропуск |
| 6 | `y` | `false` | `2` | Пропуск |

Конец цикла. Срез `arg[2:]` берёт символы с индекса 2 до конца $\rightarrow$ `"Nessy"`.
Цикл посимвольно печатает `'N'`, `'e'`, `'s'`, `'s'`, `'y'` и в конце `'\n'`.


[printparams](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-06/printparams?event=1081)
Write a **program** that prints the arguments received in the command line.

```go
import (
"os"

"github.com/01-edu/z01"
)

func main() {
	for _, arg := range os.Args[1:] {
		for _, r := range arg {
			z01.PrintRune(r)
		}
		z01.PrintRune('\n')
	}
}

Example of output :
`$ go run . choumi is the best cat 
choumi 
is 
the 
best 
cat 
$
```

### Разбор логики среза аргументов
В этой задаче нужно напечатать только введённые пользователем слова, каждое с новой строки.
1. `os.Args[1:]` — отрезает нулевой элемент (имя программы) и берёт все аргументы, начиная с первого до самого последнего. Если аргументов не ввели вовсе, срез пустой, и цикл просто ни разу не выполнится.
2. Внешний цикл `for _, arg := range os.Args[1:]` перебирает аргументы-слова по очереди.
3. Внутренний цикл `for _, r := range arg` печатает буквы текущего слова по одной руне.
4. После окончания внутреннего цикла (когда слово напечатано) выполняется `z01.PrintRune('\n')`, переводя курсор на новую строку для следующего слова.

### Итерации:
Запуск: `go run . choumi is`
Срез `os.Args[1:]` содержит 2 строки: `["choumi", "is"]`.

- **Круг 1 внешнего цикла:** `arg = "choumi"`
  - Внутренний цикл печатает руны: `'c'`, `'h'`, `'o'`, `'u'`, `'m'`, `'i'`.
  - Печатает `'\n'`. Слово `"choumi"` завершено на своей строке.
- **Круг 2 внешнего цикла:** `arg = "is"`
  - Внутренний цикл печатает руны: `'i'`, `'s'`.
  - Печатает `'\n'`. Слово `"is"` завершено на своей строке.
- Конец работы.


[revparams](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-06/revparams?event=1081)
Write a **program** that prints the arguments received in the command line in reverse order.
Example of output :
Write a **program** that prints the arguments received in the command line.
```go
import (
"os"

"github.com/01-edu/z01"
)

func main() {
	args := os.Args[1:]
	for i := len(args) - 1; i >= 0; i-- {
		for _, r := range args[i] {
			z01.PrintRune(r)
		}
		z01.PrintRune('\n')
	}
}

Example of output :
`$ go run . choumi is the best cat 
cat
best
the
is
choumi
$

```

### Разбор обратного прохода по срезу строк
Задача требует вывести слова в обратном порядке, но **сами буквы внутри слов переворачивать не нужно** (слово `"cat"` остаётся `"cat"`, а не `"tac"`).
1. `args := os.Args[1:]` сохраняет срез аргументов.
2. Обратный цикл `for i := len(args) - 1; i >= 0; i--`:
   - Начинает с самого правого элемента: индекс `len(args) - 1`.
   - Идёт до нулевого элемента включительно: условие `i >= 0`.
   - На каждом шаге уменьшает индекс: `i--`.
3. Внутри мы берём слово `args[i]` и выводим его буквы слева направо, после чего ставим `'\n'`.

### Итерации:
Запуск: `go run . choumi is cat`
`args = ["choumi", "is", "cat"]`. Длина `len(args) = 3`.
Индексы: `0: "choumi"`, `1: "is"`, `2: "cat"`.

- **Шаг 1:** `i = 3 - 1 = 2`. `args[2] = "cat"`.
  - Печатает руны `'c'`, `'a'`, `'t'`, затем `'\n'`.
- **Шаг 2:** `i--` делает `i = 1`. `args[1] = "is"`.
  - Печатает руны `'i'`, `'s'`, затем `'\n'`.
- **Шаг 3:** `i--` делает `i = 0`. `args[0] = "choumi"`.
  - Печатает руны `'c'`, `'h'`, `'o'`, `'u'`, `'m'`, `'i'`, затем `'\n'`.
- **Шаг 4:** `i--` делает `i = -1`. Условие `-1 >= 0` ложно $\rightarrow$ цикл остановлен.


[sortparams](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-06/sortparams?event=1081)
Write a **program** that prints the arguments received in the command line in ASCII order.


```go
import (
"os"

"github.com/01-edu/z01"
)

func main() {
	args := os.Args[1:]
	for i := 0; i < len(args)-1; i++ {
		for j := 0; j < len(args)-i-1; j++ {
			if args[j] > args[j+1] {
				args[j], args[j+1] = args[j+1], args[j]
			}
		}
	}
	
	for _, arg := range args {
		for _, r := range arg {
			z01.PrintRune(r)
		}
		z01.PrintRune('\n')
	}
}

Example of output :
`$ go run . 1 a 2 A 3 b 4 C 
1
2 
3 
4 
A 
C 
a 
b 
$
```

### 1. Как Go сравнивает строки через знак `>`?
Операторы `>` и `<` в Go умеют сравнивать целые строки.
Сравнение идёт побайтово/посимвольно по кодам ASCII:
- Цифры `'0'..'9'` (коды `48..57`) меньше любых букв.
- Заглавные буквы `'A'..'Z'` (коды `65..90`) меньше строчных `'a'..'z'` (коды `97..122`).
Поэтому порядок получается таким: цифры $\rightarrow$ заглавные $\rightarrow$ строчные.

### 2. Сортировка пузырьком (Bubble Sort) для среза строк
- Внешний цикл `for i := 0; i < len(args)-1; i++` отвечает за количество полных проходов.
- Внутренний цикл `for j := 0; j < len(args)-i-1; j++` сравнивает два соседних слова: `args[j]` и `args[j+1]`.
- Если левое слово больше правого (`args[j] > args[j+1]`), они меняются местами: `args[j], args[j+1] = args[j+1], args[j]`.
- Самый «тяжёлый» элемент за каждый проход всплывает в самый конец, поэтому граница внутреннего цикла уменьшается на `i`.

### Итерации:
Запуск: `go run . b 1 A`
`args = ["b", "1", "A"]`. Длина `3`.
Коды первого символа: `'b'=98`, `'1'=49`, `'A'=65`.

- **Проход `i = 0` (граница `j < 3 - 0 - 1 = 2`):**
  - `j = 0`: сравниваем `"b"` и `"1"`. $98 > 49$ истинно $\rightarrow$ обмен: `["1", "b", "A"]`.
  - `j = 1`: сравниваем `"b"` и `"A"`. $98 > 65$ истинно $\rightarrow$ обмен: `["1", "A", "b"]`.
  - Слово `"b"` встало на своё финальное место в конце.
- **Проход `i = 1` (граница `j < 3 - 1 - 1 = 1`):**
  - `j = 0`: сравниваем `"1"` и `"A"`. $49 > 65$ ложно $\rightarrow$ обмен не нужен.
- Итог сортировки: `["1", "A", "b"]`.
- Финальный цикл печатает каждое слово с новой строки:
  `1`
  `A`
  `b`


[nbrconvertalpha](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-06/nbrconvertalpha?event=1081)
Write a **program** that prints the corresponding letter in the `n` position of the latin alphabet, where `n` is each argument received.
For example `1` matches `a`, `2` matches `b`, etc. If `n` does not match a valid position of the alphabet or if the argument is not an integer, the **program** should print a space (" ").
A flag `--upper` should be implemented. When used, the program prints the result in upper case. The flag will always be the first argument.
```go
import (
"os"

"github.com/01-edu/z01"
)

func main() {
	args := os.Args[1:]
	if len(args) == 0 {
		return
	}
	
	upper := false
	if args[0] == "--upper" {
		upper = true
		args = args[1:]
	}
	
	for _, arg := range args {
		n := 0
		valid := true
		for _, r := range arg {
			if r < '0' || r > '9' {
				valid = false
				break
			}
			n = n*10 + int(r-'0')
		}
		
		if !valid || n < 1 || n > 26 {
			z01.PrintRune(' ')
		} else {
			if upper {
				z01.PrintRune(rune('A' + n - 1))
			} else {
				z01.PrintRune(rune('a' + n - 1))
			}
		}
	}
	z01.PrintRune('\n')
}


$ go run . 
$ go run . 8 5 12 12 15 | cat -e 
hello$ 
$ go run . 12 5 7 5 14 56 4 1 18 25 | cat -e 
legen dary$ 
$ go run . 32 86 h | cat -e 
   $ 
$ go run . --upper 8 5 25 
HEY$ 
$
```

### 1. Как разобрать и «съесть» флаг командной строки?
По условию флаг `--upper` может быть **только самым первым аргументом**:
```go
if args[0] == "--upper" {
    upper = true
    args = args[1:]
}
```
Если первое слово равно `"--upper"`, мы:
1. Запоминаем булев переключатель `upper = true`.
2. Сдвигаем срез: `args = args[1:]` (первый элемент удаляется из списка аргументов). Теперь в `args` остаются только сами числа, и циклу не нужно думать о флаге!

### 2. Валидация числа и досрочный выход `break`
В цикле по символам аргумента мы проверяем каждую руну `r < '0' || r > '9'`.
Если встретилась не-цифра (например, буква `"h"` в `"32 86 h"`):
- Ставим флаг `valid = false`.
- Вызываем команду `break` — она немедленно прерывает внутренний цикл, чтобы не тратить время на парсинг невалидного числа.

### 3. Математика позиции в алфавите (`n - 1`)
В латинском алфавите 26 букв. Нумерация в задаче начинается с `1`: `1 -> 'a'`, `2 -> 'b'`.
- Буква `'a'` имеет код `97`.
- Если нам дали `n = 1`, то `'a' + 1 - 1 = 'a'` (код `97`).
- Если нам дали `n = 2`, то `'a' + 2 - 1 = 'a' + 1 = 'b'` (код `98`).
Если число выходит за границы (`n < 1 || n > 26`) или аргумент не является числом (`!valid`), печатается пробел `' '`.

### Итерации:
Запуск: `go run . --upper 8 56 25`
1. `args = ["--upper", "8", "56", "25"]`.
2. `args[0] == "--upper"` истинно $\rightarrow$ `upper = true`, срез сдвигается: `args = ["8", "56", "25"]`.
3. **Аргумент `"8"`:**
   - Превращается в число `n = 8`. `valid = true`.
   - Проверка границ: `8` лежит между 1 и 26.
   - `upper == true` $\rightarrow$ печатает `'A' + 8 - 1 = 'A' + 7 = 'H'`.
4. **Аргумент `"56"`:**
   - Превращается в число `n = 56`.
   - Проверка: `56 > 26` $\rightarrow$ не входит в алфавит! Печатает пробел `' '`.
5. **Аргумент `"25"`:**
   - Число `n = 25`. Входит в алфавит.
   - Печатает `'A' + 25 - 1 = 'A' + 24 = 'Y'`.
6. В конце печатает `'\n'`. Итог на экране: `H Y`.


Write a program that can take --insert (or -i), --order (or -o) and a string as arguments.
This program should :
- Insert the string given to the --insert (or -i), into the argument string, if given.

- If the flag --order (or -o) is given, order the string argument (in ASCII order).

- If there are no arguments or if the flag --help (or -h) is given, the options should be printed as in the example.

- The short flag will have two spaces before the (-).

- The explanation of the flag will have a tab followed by a space before the beginning of the sentence (This flag...).
Don't mind the extra spaces or tabs on the following example as they were placed there to provide a better understanding and visualization of the output in the terminal. Follow the rules above for the spacing.


```go
package main

import (
	"os"

	"github.com/01-edu/z01"
)

func printHelp() {
	helpText := "--insert\n  -i\n\t This flag inserts the string into the string passed as argument.\n--order\n  -o\n\t This flag will behave like a boolean, if it is called it will order the argument.\n"
	for _, r := range helpText {
		z01.PrintRune(r)
	}
}

func main() {
	args := os.Args[1:]

	if len(args) == 0 {
		printHelp()
		return
	}

	insertStr := ""
	orderFlag := false
	baseStr := ""

	for _, arg := range args {
		if arg == "-h" || arg == "--help" {
			printHelp()
			return
		} else if len(arg) >= 9 && arg[:9] == "--insert=" {
			insertStr = arg[9:]
		} else if len(arg) >= 3 && arg[:3] == "-i=" {
			insertStr = arg[3:]
		} else if arg == "--order" || arg == "-o" {
			orderFlag = true
		} else {
			baseStr = arg
		}
	}

	resultRunes := []rune(baseStr + insertStr)

	if orderFlag {
		for i := 0; i < len(resultRunes)-1; i++ {
			for j := 0; j < len(resultRunes)-i-1; j++ {
				if resultRunes[j] > resultRunes[j+1] {
					resultRunes[j], resultRunes[j+1] = resultRunes[j+1], resultRunes[j]
				}
			}
		}
	}

	for _, r := range resultRunes {
		z01.PrintRune(r)
	}
	z01.PrintRune('\n')
}

Example of output :

$ go run . --insert=4321 --order asdad
1234aadds
$ go run . --insert=4321 asdad
asdad4321
$ go run . asdad
asdad
$ go run . --order 43a21
1234a
$ go run .
--insert
  -i
         This flag inserts the string into the string passed as argument.
--order
  -o
         This flag will behave like a boolean, if it is called it will order the argument.
$ go run . -h
--insert
  -i
         This flag inserts the string into the string passed as argument.
--order
  -o
         This flag will behave like a boolean, if it is called it will order the argument.
$ go run . --help
--insert
  -i
         This flag inserts the string into the string passed as argument.
--order
  -o
         This flag will behave like a boolean, if it is called it will order the argument.
```

### 1. Как безопасно парсить префиксы аргументов (`--insert=` и `-i=`)?
Если аргумент содержит значение через знак равно (`--insert=4321`), нам нужно отрезать префикс и забрать хвост:
- Длина префикса `"--insert="` равна 9 символов.
- Мы обязаны **сначала** проверить длину строки: `len(arg) >= 9`. Если этого не сделать и сразу написать `arg[:9]`, на коротких словах (например, `"hi"`) программа упадёт в панику: `panic: slice bounds out of range`.
- Если префикс совпал (`arg[:9] == "--insert="`), мы забираем значение с 9-го символа до конца: `insertStr = arg[9:]`.
- Для короткого флага `"-i="` длина равна 3: `len(arg) >= 3 && arg[:3] == "-i="`, значение: `arg[3:]`.

### 2. Логика объединения и сортировки символов
1. Сначала склеиваем основную строку и вставку: `baseStr + insertStr`. По ТЗ вставка добавляется в конец базовой строки.
2. Преобразуем в срез рун `resultRunes := []rune(...)`.
3. Если флаг `orderFlag == true`, запускаем пузырьковую сортировку по рунам, которая расставляет все символы в ASCII порядке.

### Итерации:
Запуск: `go run . --insert=4321 --order asdad`
`args = ["--insert=4321", "--order", "asdad"]`

- **Шаг 1 (разбор аргументов в цикле):**
  - Аргумент 0: `"--insert=4321"` $\rightarrow$ длина $13 \ge 9$, префикс `arg[:9]` равен `"--insert="`. Сохраняем `insertStr = "4321"`.
  - Аргумент 1: `"--order"` $\rightarrow$ совпадает с условием `arg == "--order"`. Ставим `orderFlag = true`.
  - Аргумент 2: `"asdad"` $\rightarrow$ не является флагом. Записываем в `baseStr = "asdad"`.
- **Шаг 2 (склейка):**
  - `resultRunes = []rune("asdad" + "4321") = ['a', 's', 'd', 'a', 'd', '4', '3', '2', '1']`.
- **Шаг 3 (сортировка, так как `orderFlag == true`):**
  - Циклы пузырька сравнивают руны: цифры `'1'`, `'2'`, `'3'`, `'4'` перемещаются в начало, за ними идут буквы `'a'`, `'a'`, `'d'`, `'d'`, `'s'`.
  - Итог среза: `['1', '2', '3', '4', 'a', 'a', 'd', 'd', 's']`.
- **Шаг 4:** Печать рун и `'\n'`. Экран показывает: `1234aadds`.


[rotatevowels](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-06/rotatevowels?event=1081)
Write a program that checks the arguments for vowels.

If the arguments contain vowels (for this exercise y is not considered a vowel) the program has to "mirror" the position of the vowels in the arguments (see the examples).

If the number of arguments is less than 1, the program displays a new line ("\n").

If the arguments do not have any vowels, the program just prints the arguments.
```go
import (
	"os"
	
	"github.com/01-edu/z01"
)

func isVowel(r rune) bool {
	return r == 'a' || r == 'e' || r == 'i' || r == 'o' || r == 'u' ||
		r == 'A' || r == 'E' || r == 'I' || r == 'O' || r == 'U'
}

func main() {
	args := os.Args[1:]
	if len(args) == 0 {
		z01.PrintRune('\n')
		return
	}
	
	var allRunes []rune
	for i, arg := range args {
		for _, r := range arg {
			allRunes = append(allRunes, r)
		}
		if i < len(args)-1 {
			allRunes = append(allRunes, ' ')
		}
	}
	
	left := 0
	right := len(allRunes) - 1
	
	for left < right {
		for left < right && !isVowel(allRunes[left]) {
			left++
		}
		for left < right && !isVowel(allRunes[right]) {
			right--
		}
		if left < right {
			allRunes[left], allRunes[right] = allRunes[right], allRunes[left]
			left++
			right--
		}
	}
	
	for _, r := range allRunes {
		z01.PrintRune(r)
	}
	z01.PrintRune('\n')
}


Example of output :

$ go run . "Hello World" | cat -e
Hollo Werld$
$ go run . "HEllO World" "problem solved"
Hello Werld problom sOlvEd
$ go run . "str" "shh" "psst"
str shh psst
$ go run . "happy thoughts" "good luck"
huppy thooghts guod lack
$ go run . "aEi" "Ou"
uOi Ea
$ go run .

$
```

### 1. Объединение аргументов в один общий срез рун
По условию гласные буквы должны «зеркально» меняться местами **через всю строку и между разными аргументами** (например, первая гласная первого аргумента меняется с последней гласной последнего аргумента).
Поэтому мы сначала собираем все аргументы в единый список символов `allRunes`:
- Добавляем руны текущего слова через `append`.
- Между словами добавляем пробел: `if i < len(args)-1 { allRunes = append(allRunes, ' ') }`.

### 2. Двусторонний указатель с фильтрацией согласных
Вместо переворота всех букв подряд мы двигаем два указателя:
1. `left := 0` шагает слева направо. Внутренний цикл `for left < right && !isVowel(allRunes[left])` перепрыгивает все согласные буквы и пробелы, пока не упрётся в гласную.
2. `right := len(allRunes) - 1` шагает справа налево. Внутренний цикл `for left < right && !isVowel(allRunes[right])` перепрыгивает согласные справа, пока тоже не найдёт гласную.
3. Когда оба указателя остановились на гласных, они меняются местами:  
   `allRunes[left], allRunes[right] = allRunes[right], allRunes[left]`.
4. Делаем `left++` и `right--` и продолжаем поиск следующей пары.

### Итерации:
Запуск: `go run . "aEi" "Ou"`
Общий срез после сборки аргументов: `['a', 'E', 'i', ' ', 'O', 'u']`.
Индексы: `0:'a', 1:'E', 2:'i', 3:' ', 4:'O', 5:'u'`.

| Шаг | `left` | Руна слева | `right` | Руна справа | Действие | Состояние среза |
| :---: | :---: | :---: | :---: | :---: | :--- | :--- |
| **1** | `0` | `'a'` (гласная) | `5` | `'u'` (гласная) | Обмен рун `[0]` и `[5]` $\rightarrow$ `left=1, right=4` | `['u', 'E', 'i', ' ', 'O', 'a']` |
| **2** | `1` | `'E'` (гласная) | `4` | `'O'` (гласная) | Обмен рун `[1]` и `[4]` $\rightarrow$ `left=2, right=3` | `['u', 'O', 'i', ' ', 'E', 'a']` |
| **3** | `2` | `'i'` (гласная) | `3` | `' '` (не гласная) | Правый цикл делает `right--` $\rightarrow$ `right=2` | `left=2, right=2` |
| **Стоп** | `2` | - | `2` | - | Условие `left < right` ($2 < 2$) ложно $\rightarrow$ выход из цикла | `['u', 'O', 'i', ' ', 'E', 'a']` |

Печать рун на экран: `uOi Ea`. Все гласные зеркально отразились, а пробел остался на месте!
