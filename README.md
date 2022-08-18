# Cheat Sheet Go

## Channels
```go
func main() {
	c := make(chan string)

	for i := 0; i < 12; i++ {
		go sender(c)
	}
	
	go receiver(c)

	for {

	}
}

func sender(c chan string) {
	c <- "ping"
}

func receiver(c chan string) {
	for {
		msg := <-c
		fmt.Println(msg)
		time.Sleep(50 * time.Millisecond)
	}
}
```

## Random
```go
// Random integer between [min and max[
rand.Intn(max-min)+min
```

## JSON
```go
type MyType struct {
	Id int `json:"id"`
	Name string `json:"name"`
}

var data []MyType = []MyType{}
str := "[{\"id\": 1, \"name\": \"bar\"}, {\"id\": 2, \"name\": \"foo\"}]"

err := json.Unmarshal([]byte(str), &data)
if err != nil {
    fmt.Println("Error parsing JSON :", err)
}
```

## HTTP Request
```go
const url string = "https://google.com"

resp, err := http.Get(url)
if err != nil {
    fmt.Printf("Error get request : %s", err)
}

body, err := ioutil.ReadAll(resp.Body)
if err != nil {
    fmt.Printf("Error reading body : %s", err)
}

str := string(body)
```

## Serve static files
```go
port := "3000"
fs := http.FileServer(http.Dir("./static"))
http.Handle("/", fs)
fmt.Println("Listening on", port)
err := http.ListenAndServe(":"+port, nil)
if err != nil {
	fmt.Println("Error serving static files")
}
```

## Delay
```go
time.Sleep(3 * time.Second)
time.Sleep(200 * time.Millisecond)
```
