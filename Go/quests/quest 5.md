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
```