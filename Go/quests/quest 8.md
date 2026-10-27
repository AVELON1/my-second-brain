
[boolean](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-08/boolean?event=1081)
Create a new directory called `boolean`.
- The code below must be copied into a file called `main.go` inside of the `boolean` directory.
    
- The necessary changes must be applied for the program to work.
```go
import (
	"os"

	"github.com/01-edu/z01"
)

type boolean int

const (
	yes boolean = 1
	no  boolean = 0
)

const (
	EvenMsg = "I have an even number of arguments"
	OddMsg  = "I have an odd number of arguments"
)

func printStr(s string) {
	for _, r := range s {
		z01.PrintRune(r)
	}
	z01.PrintRune('\n')
}

func even(nbr int) int {
	if nbr%2 == 0 {
		return 1
	}
	return 0
}

func isEven(nbr int) boolean {
	if even(nbr) == 1 {
		return yes
	} else {
		return no
	}
}

func main() {
	lengthOfArg := len(os.Args) - 1
	
	if isEven(lengthOfArg) == 1 {
		printStr(EvenMsg)
	} else {
		printStr(OddMsg)
	}
}
```

### 1. Что принципиально нового в Квесте 8?
Квест 8 знакомит с фундаментом архитектуры Go:
1. Создание собственных типов данных (`type`).
2. Неизменяемые константы (`const`).
3. Структуры (`struct`) и указатели на них.
4. Работа с реальной файловой системой диска (`os.ReadFile`, чтение и ошибки `error`).
5. Стандартные системные потоки (`os.Stdin`, `os.Stdout`) и коды завершения программ (`os.Exit(1)`).

### 2. Пользовательские типы (`type boolean int`) и блок `const`
- `type boolean int` создаёт новый тип данных `boolean`, основанный на `int`. Это позволяет явно разграничивать сущности в программе.
- Блок `const (...)` объявляет неизменяемые значения, которые вычисляются на этапе компиляции:
  - `yes boolean = 1` и `no boolean = 0` работают как наши кастомные логические значения.
  - Текстовые константы `EvenMsg` и `OddMsg` хранят готовые системные сообщения, чтобы не писать длинные строки повторно внутри логики.
- `lengthOfArg := len(os.Args) - 1`: вычитаем 1, потому что нулевой аргумент — это путь к самому бинарнику, а считаем мы только введённые пользователем слова.

### Итерации:
1. Запуск: `go run . "not" "odd"`
   - `os.Args` содержит `["./main", "not", "odd"]`. Длина 3.
   - `lengthOfArg = 3 - 1 = 2`.
   - `isEven(2)`:
     - `even(2)`: $2 \% 2 == 0 \rightarrow 1$.
     - `even(2) == 1` $\rightarrow$ возвращает константу `yes` (значение `1`).
   - Проверка `isEven(2) == 1` истинна $\rightarrow$ печать константы `EvenMsg`: `"I have an even number of arguments"`.

2. Запуск: `go run . "not even"`
   - Аргумент один: `"not even"` (в кавычках терминал считает это одним словом!).
   - `lengthOfArg = 2 - 1 = 1`.
   - `isEven(1)`: $1 \% 2 == 1 \rightarrow$ возвращает `no` (`0`).
   - Условие ложно $\rightarrow$ печать `OddMsg`: `"I have an odd number of arguments"`.


[point](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-08/point?event=1081)
Create a new directory called `point`.
- The code below must be copied into a file called `main.go` inside the `point` directory.
    
- The necessary changes must be applied so that the program works.
    
- The function `setPoint()` must work with `int`.
```go
import "github.com/01-edu/z01"

type point struct {
	x int
	y int
}

func setPoint(ptr *point) {
	ptr.x = '*'
	ptr.y = '*' / ('c' - 'a')
}

func main() {
	points := &point{}
	
	setPoint(points)
	
	out := []rune{
		'x', ' ', '=', ' ',
		'0' + ('e' - 'a'), '0' + ('c' - 'a'),
		',', ' ', 'y', ' ', '=', ' ',
		'0' + ('c' - 'a'), '0' + ('b' - 'a'),
		'\n',
	}
	
	for _, r := range out {
		z01.PrintRune(r)
	}
}
```

### 1. Что такое структуры (`struct`)?
Структура — это составной тип данных, который объединяет несколько связанных переменных (полей) под одним именем:
```go
type point struct {
    x int
    y int
}
```
Точка на плоскости описывается двумя координатами: `x` и `y`.
- `points := &point{}` создаёт в памяти новую пустую структуру и возвращает её адрес (указатель `*point`).
- Обращение к полям через указатель: в Go не нужно писать `(*ptr).x`, синтаксис `ptr.x` автоматически разыменовывает указатель и записывает значение прямо в ячейку структуры.

### 2. Секрет задачи: почему в коде нет цифр?
В тесте бассейна на эту задачу стоит фильтр, который **запрещает использовать цифры `0..9` в исходном коде**!
Поэтому значения `42` и `21` спрятаны через ASCII-коды рун:
- Символ `'*'` в таблице ASCII имеет код **`42`**. Значит, `ptr.x = '*'` записывает число `42`!
- Буква `'c'` имеет код 99, а `'a'` — код 97. Значит, `'c' - 'a' = 99 - 97 = 2`.
- Выражение `ptr.y = '*' / ('c' - 'a')` делит 42 на 2 и получает **`21`**!
- Срез рун `out` аналогично собирает строку `"x = 42, y = 21\n"`:
  - `'0' + ('e' - 'a')` = $48 + (101 - 97) = 48 + 4 = 52$ (символ `'4'`).
  - `'0' + ('c' - 'a')` = $48 + (99 - 97) = 48 + 2 = 50$ (символ `'2'`).
  - `'0' + ('b' - 'a')` = $48 + (98 - 97) = 48 + 1 = 49$ (символ `'1'`).

### Итерации:
1. Создаётся переменная структуры `points` в памяти: `{x: 0, y: 0}`.
2. Вызов `setPoint(points)`:
   - `ptr.x = 42` (код `'*'`).
   - `ptr.y = 42 / 2 = 21`.
   - В памяти структура `points` стала `{x: 42, y: 21}`.
3. Цикл печатает руны из массива `out`:
   - Печатает `'x'`, `' '`, `'='`, `' '`
   - Печатает `'4'`, `'2'`
   - Печатает `','`, `' '`, `'y'`, `' '`, `'='`, `' '`
   - Печатает `'2'`, `'1'`
   - Печатает `'\n'`
4. Экран показывает: `x = 42, y = 21`.


[displayfile](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-08/displayfile?event=1081)
Write a program that displays, on the standard output, the content of a file given as argument.
```go
import (
	"fmt"
	"os"
)

func main() {
	args := os.Args[1:]
	
	if len(args) == 0 {
		fmt.Println("File name missing")
		return
	}
	
	if len(args) > 1 {
		fmt.Println("Too many arguments")
		return
	}
	
	content, err := os.ReadFile(args[0])
	if err != nil {
		return
	}
	
	fmt.Print(string(content))
}
```

### 1. Чтение файлов с диска: `os.ReadFile` и возврат ошибок
Функция `os.ReadFile(filename)` читает файл целиком из файловой системы.
В Go принята идиома **множественного возврата значений**:
```go
content, err := os.ReadFile(args[0])
```
1. `content` имеет тип `[]byte` — это сырые байты, прочитанные из файла.
2. `err` имеет тип `error`. Если файл успешно прочитан, `err == nil`. Если файла не существует или нет прав доступа, `err` содержит описание системной ошибки.
3. Проверка `if err != nil` — стандартная защита от сбоев в Go: если произошла ошибка, мы прерываем работу через `return`.

### 2. Перевод байтов в строку: `string(content)`
Поскольку `os.ReadFile` возвращает срез байт `[]byte`, перед печатью на экран мы преобразуем его в текст через `string(content)` и выводим через `fmt.Print`.

### Итерации:
1. **Случай 1 (без параметров):**
   - Запуск: `go run .`
   - `len(args) == 0` истинно $\rightarrow$ печать `"File name missing"`, `return`.
2. **Случай 2 (передали 2 файла):**
   - Запуск: `go run . quest8.txt main.go`
   - `len(args) = 2 > 1` истинно $\rightarrow$ печать `"Too many arguments"`, `return`.
3. **Случай 3 (передали 1 файл):**
   - Запуск: `go run . quest8.txt`
   - `len(args) = 1` $\rightarrow$ обе проверки пройдены.
   - `os.ReadFile("quest8.txt")` читает байты файла, `err == nil`.
   - `fmt.Print(string(content))` выводит содержимое файла на экран.


Write a program that behaves like a simplified `cat` command.

- The options do not have to be handled.
    
- If the program is called without arguments it should take the standard input (stdin) and print it back on the standard output (stdout).
```go
import (
	"io"
	"os"
	
	"github.com/01-edu/z01"
)

func printStr(s string) {
	for _, r := range s {
		z01.PrintRune(r)
	}
}

func main() {
	args := os.Args[1:]
	
	if len(args) == 0 {
		_, _ = io.Copy(os.Stdout, os.Stdin)
		return
	}
	
	for _, arg := range args {
		content, err := os.ReadFile(arg)
		if err != nil {
			printStr("ERROR: " + err.Error() + "\n")
			os.Exit(1)
		}
		printStr(string(content))
	}
}
```

### 1. Что такое стандартные потоки `Stdin` и `Stdout`?
В операционных системах каждая запущенная программа имеет три стандартных потока:
- `os.Stdin` (Standard Input) — поток ввода (клавиатура или левая часть пайпа `|`).
- `os.Stdout` (Standard Output) — поток вывода (терминал или правая часть перенаправления `>`).
- `os.Stderr` (Standard Error) — поток для сообщений об ошибках.

Если аргументов нет (`len(args) == 0`), команда `cat` должна работать в интерактивном режиме: читать всё, что вводит пользователь, и сразу печатать обратно на экран.
Функция `io.Copy(os.Stdout, os.Stdin)` перекачивает данные напрямую из ввода в вывод байт за байтом, пока ввод не закроется (например, по нажатию `Ctrl+D` или `Ctrl+C`).

### 2. Системные ошибки и код выхода `os.Exit(1)`
- `err.Error()` возвращает текстовую строку системной ошибки (например, `"open abc: no such file or directory"`).
- `os.Exit(1)`: завершает процесс с кодом ошибки `1`. Обычный `return` завершает программу с кодом `0` (успех). В терминале статус последней команды проверяется через `echo $?`: если там `0` — всё прошло успешно, если `1` — произошёл сбой.

### Итерации:
1. Запуск через конвейер: `cat quest8.txt | go run .`
   - `len(args) == 0`.
   - Срабатывает `io.Copy(os.Stdout, os.Stdin)`: данные из трубы перенаправляются в `Stdout`. На экран выводится текст файла.
2. Запуск с несуществующим файлом: `go run . abc`
   - `os.ReadFile("abc")` возвращает ошибку `err != nil`.
   - Программа печатает `"ERROR: open abc: no such file or directory\n"`.
   - `os.Exit(1)` немедленно завершает работу программы со статусом 1.


[ztail](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-08/ztail?event=1081)
Write a program that behaves like a simplified `tail` command that takes at least one file as an argument.
The only option to be handled is `-c` and will be used in all the tests as the first argument, with positive values.
For this program the `os` package can be used.
Handle the errors by returning a non-zero exit status but process all the files.
If several files are given, print a newline and the file name between each one of them (see below).
```go
import (
	"fmt"
	"os"
)

func atoi(s string) int {
	n := 0
	for _, r := range s {
		if r >= '0' && r <= '9' {
			n = n*10 + int(r-'0')
		}
	}
	return n
}

func main() {
	if len(os.Args) < 4 {
		return
	}
	
	numBytes := atoi(os.Args[2])
	files := os.Args[3:]
	hasError := false
	
	for i, file := range files {
		data, err := os.ReadFile(file)
		if err != nil {
			fmt.Printf("%s\n", err.Error())
			hasError = true
			continue
		}
		
		if len(files) > 1 {
			if i > 0 {
				fmt.Printf("\n")
			}
			fmt.Printf("==> %s <==\n", file)
		}
		
		start := len(data) - numBytes
		if start < 0 {
			start = 0
		}
		
		fmt.Printf("%s", string(data[start:]))
	}
	
	if hasError {
		os.Exit(1)
	}
}
```

### 1. Разбор аргументов утилиты `tail -c`
По условию вызов всегда имеет структуру:
`./ztail -c <число_байт> <файл1> [файл2...]`
- `os.Args[0]`: имя программы.
- `os.Args[1]`: флаг `"-c"`.
- `os.Args[2]`: количество байт для среза с конца (`numBytes := atoi(os.Args[2])`).
- `os.Args[3:]`: срез со всеми путями файлов (`files`).

### 2. Обработка ошибок без остановки программы (`continue`)
В отличие от `cat`, где мы сразу делали `os.Exit(1)`, утилита `tail` **обязана обработать все файлы**, даже если один из них не открылся!
- Если файл не найден (`err != nil`), программа выводит ошибку `fmt.Printf("%s\n", err.Error())`.
- Мы ставим флаг `hasError = true` и выполняем `continue` — пропускаем печать содержимого этого файла и **сразу переходим к следующему файлу в цикле**.
- И только в самом конце программы, когда все файлы обработаны, если `hasError == true`, вызываем `os.Exit(1)`.

### 3. Математика хвоста файла (`start := len(data) - numBytes`)
Нам нужны последние `numBytes` байт файла:
- Индекс старта: `start := len(data) - numBytes`.
- Защита от коротких файлов: если файл содержит всего 2 байта, а запросили 10 (`start = 2 - 10 = -8`), условие `if start < 0` выравнивает `start = 0`, чтобы не получить панику выхода за границы среза.
- Печатаем срез: `data[start:]`.

### 4. Разделители заголовков между файлами
Если файлов несколько (`len(files) > 1`):
- Для каждого файла печатается шапка: `==> имя_файла <==`.
- Начиная со второго файла (`i > 0`), перед шапкой печатается пустая строка `\n`.

### Итерации:
Запуск: `go run . -c 4 file1.txt nonexisting.txt file2.txt`
`numBytes = 4`. `files = ["file1.txt", "nonexisting.txt", "file2.txt"]` (`len = 3 > 1`).

1. **Файл 0 (`file1.txt`, содержит `"abcdef\n"`):**
   - Успешно прочитан.
   - `i = 0` $\rightarrow$ печатает шапку `==> file1.txt <==\n`.
   - `len(data) = 7`. `start = 7 - 4 = 3`.
   - Печатает срез `data[3:]` $\rightarrow$ `"ef\n"`.
2. **Файл 1 (`nonexisting.txt`):**
   - `os.ReadFile` возвращает ошибку $\rightarrow$ печатает `"open nonexisting.txt: no such file or directory\n"`.
   - Ставит `hasError = true`.
   - `continue` переходит к файлу 2.
3. **Файл 2 (`file2.txt`, содержит `"123456\n"`):**
   - Успешно прочитан.
   - `i = 2 > 0` $\rightarrow$ печатает `\n`, затем `==> file2.txt <==\n`.
   - Печатает последние 4 байта $\rightarrow$ `"456\n"`.
4. Цикл завершён.
5. `hasError == true` $\rightarrow$ программа вызывает `os.Exit(1)` и завершается с кодом ошибки 1.
