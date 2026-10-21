
[boolean](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-08/boolean?event=1081[displayfile](https://01.tomorrow-school.ai/intra/qairu/piscinego/quest-08/displayfile?event=1081))
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

## Code to be copied
func printStr(s string) {
	for _, r := range s {
		z01.PrintRune(r)
	}
	z01.PrintRune('\n')
}

func isEven(nbr int) boolean {
	if even(nbr) == 1 {
		return yes
	} else {
		return no
	}
}

func main() {
	if isEven(lengthOfArg) == 1 {
		printStr(EvenMsg)
	} else {
		printStr(OddMsg)
	}
}

Usage

$ go run . "not" "odd"
I have an even number of arguments
$ go run . "not even"
I have an odd number of arguments
```

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

Code to be copied

func setPoint(ptr *point) {
	ptr.x = 42
	ptr.y = 21
}

func main() {
	points := &point{}
	setPoint(points)
	fmt.Printf("x = %d, y = %d\n",points.x, points.y)
}

Usage

$ go run .
x = 42, y = 21
```



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

Usage :

$ go run .
File name missing
$ echo 'Almost there!!' > quest8.txt
$ go run . quest8.txt main.go
Too many arguments
$ go run . quest8.txt
Almost there!!
```


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

$ echo '"Programming is a skill best acquired by practice and example rather than from books" by Alan Turing' > quest8.txt

$ cat <<EOF> quest8T.txt
"Alan Mathison Turing was an English mathematician, computer scientist, logician, cryptanalyst. Turing was highly influential in the development of theoretical computer science, providing a formalisation of the concepts of algorithm and computation with the Turing machine, which can be considered a model of a general-purpose computer. Turing is widely considered to be the father of theoretical computer science and artificial intelligence."
EOF

$ go run . abc
ERROR: open abc: no such file or directory
exit status 1

$ go run . quest8.txt
"Programming is a skill best acquired by pratice and example rather than from books" by Alan Turing

$ go run . quest8.txt abc
"Programming is a skill best acquired by pratice and example rather than from books" by Alan Turing
ERROR: open abc: No such file or directory

$ cat quest8.txt | ./cat
"Programming is a skill best acquired by pratice and example rather than from books" by Alan Turing

$ go run .
Hello
Hello
^C

$ go run . quest8.txt quest8T.txt
"Programming is a skill best acquired by pratice and example rather than from books" by Alan Turing
"Alan Mathison Turing was an English mathematician, computer scientist, logician, cryptanalyst. Turing was highly influential in the development of theoretical computer science, providing a formalisation of the concepts of algorithm and computation with the Turing machine, which can be considered a model of a general-purpose computer. Turing is widely considered to be the father of theoretical computer science and artificial intelligence."
```

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

Usage

If file1.txt & file2.txt contains :

abcdefghijklmnopqrstuvwxyz

Note that the files above end with a new line.

Normal cases :

$ go run . -c 4 file1.txt
xyz
$ go run . -c 4 file1.txt file2.txt
==> file1.txt <==
xyz

==> file2.txt <==
xyz

Error cases :

$ go run . -c 4 file1.txt nonexisting1.txt file2.txt nonexisting2.txt
==> file1.txt <==
xyz
open nonexisting1.txt: no such file or directory

==> file2.txt <==
xyz
open nonexisting2.txt: no such file or directory
$ echo $?
1
```