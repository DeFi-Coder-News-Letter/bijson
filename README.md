# bijson: optimized standard library JSON for Go

Clone of `fastjson` by intel-go, `bijson` has the same API as json from standard library `encoding/json`... and it serializes(deserializes) big.Int to(from) hex strings.

Note: big.Int serialization does not support the `",string"` struct tag

## Getting Started
```
$ go get github.com/torusresearch/bijson
```


## Example
```Go
import (
    "github.com/torusresearch/bijson"
    "math/big"
    "fmt"
)

func main() {
	var jsonBlob = []byte(`[
	{"Num": "9",   "PtrNum": "FF"},
	{"Num": "3",   "PtrNum": "1"}
    ]`)
	type NumStruct struct {
		Num    big.Int
		PtrNum *big.Int
	}
	var numStructs []NumStruct
	err := Unmarshal(jsonBlob, &numStructs)
	if err != nil {
		fmt.Println("error:", err)
	}
	fmt.Printf("%+v", numStructs)
	// Output:
	// [{Num:{neg:false abs:[9]} PtrNum:+255} {Num:{neg:false abs:[3]} PtrNum:+1}]
}
```
## API
API is the same as encoding/json
[GoDoc](https://golang.org/pkg/encoding/json/#Unmarshal)
