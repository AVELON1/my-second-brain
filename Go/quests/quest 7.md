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

