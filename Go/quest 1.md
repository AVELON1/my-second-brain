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
