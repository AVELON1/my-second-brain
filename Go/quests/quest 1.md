1
Write a program that prints the decimal digits in ascending order (from `0` to `9`) on a single line.

A line is a sequence of characters preceding the end of line character (`'\n'`).

```GO
package main

import "github.com/01-edu/z01"

func main() {
    for i := '0'; i <= '9'; i++ {
        z01.PrintRune(i)
    }
    z01.PrintRune('\n')
}
```

2
Write a function that prints `'T'` (true) on a single line if the `int` passed as parameter is negative, otherwise it prints `'F'` (false).
```GO
package piscine

import "github.com/01-edu/z01"

func IsNegative(nb int) {
	if nb < 0 {
		z01.PrintRune('T')
	} else {
		z01.PrintRune('F')
	}
	z01.PrintRune('\n')
}
```

### Разбор и итерации

#### Задача 1 (`printdigits`)
- Цикл `for i := '0'; i <= '9'; i++` стартует с руны `'0'` (код `48`) и на каждом шаге увеличивает код на `1`, пока не дойдёт до `'9'` (код `57`).
- После завершения цикла один раз печатается перенос строки `z01.PrintRune('\n')`, чтобы все цифры остались на одной линии.

**Итерации цикла:**
- Шаг 1: `i = '0'` (`48`) $\rightarrow$ условие `'0' <= '9'` истинно $\rightarrow$ печатает `0`, `i++` делает `'1'`.
- Шаг 2: `i = '1'` (`49`) $\rightarrow$ печатает `1`, `i++` делает `'2'`.
- ...
- Шаг 10: `i = '9'` (`57`) $\rightarrow$ печатает `9`, `i++` делает код `58` (символ `':'`).
- Стоп: код `58 <= 57` ложно $\rightarrow$ выход из цикла и печать `'\n'`. Итог на экране: `0123456789`.

#### Задача 2 (`isnegative`)
- Функция принимает параметр `nb int` и проверяет знак числа через `if nb < 0`.
- Перенос строки `z01.PrintRune('\n')` вынесен **за пределы** `if / else`, потому что он нужен в обоих случаях — так мы не дублируем одну и ту же строчку дважды.

**Итерации (проверка разных вызовов):**
1. Вызов `IsNegative(-5)`:
   - Проверка `-5 < 0` $\rightarrow$ `true` $\rightarrow$ заходит в блок `if`, печатает `'T'`, пропускает `else`, печатает `'\n'`.
2. Вызов `IsNegative(0)`:
   - Проверка `0 < 0` $\rightarrow$ `false` (ноль не отрицательный!) $\rightarrow$ перепрыгивает в `else`, печатает `'F'`, затем `'\n'`.
3. Вызов `IsNegative(12)`:
   - Проверка `12 < 0` $\rightarrow$ `false` $\rightarrow$ перепрыгивает в `else`, печатает `'F'`, затем `'\n'`.
