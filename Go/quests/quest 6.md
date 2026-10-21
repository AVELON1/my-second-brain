
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