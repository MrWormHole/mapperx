# MapperX

![MapperX](https://github.com/MrWormHole/mapperx/blob/master/mapperx_logo.png)

## Help us grow
&nbsp;&nbsp; Any issues, PRs or feedbacks are welcome and greatly appreciated, if you enjoyed using mapperx, please consider donating. Here is the Open Collective link....

## What we aim to do
* 1-to-1 struct-struct mapping
* Maps underlying nested structs 
* Maps same types with same variable names by default
* Maps same types with different names by tag specification
* Does use reflection to generate mapperx package

## What we don't aim to do
* Doesn't aim to do aggregation while mapping
* Doesn't map not equal types
* Doesn't use reflection at runtime

## Getting Started
&nbsp;&nbsp; Mapperx heavily relies on code generation. This means that you need to specify 2 arguments source(file path and struct type) and target(file path and struct type)
Then mapperx will generate a directory and a package called mapperx, when you run it. Easiest way to use is to do go generate compiler directive in your definitions at the start of a file. 

```shell
go get -u github.com/MrWormHole/mapperx
```

```go
package main

//go:generate mapperx github.com/yourusername/yourproject/model.Admin github.com/yourusername/yourproject/model.User
type Admin struct {
    Name string
    ID string
    Country string
    Score string `mapperx:"Highscore"`
}

type User struct {
    Name string
    ID string
    Country string
    Highscore string 
}
```

Output file will look something like this

```go
// Code generated by mapperx, PLEASE DO NOT EDIT.
package mapperx

import model "github.com/MrWormHole/mapperx/examples/model"

func mapAdminToUser(admin *model.Admin, user *model.User) {
	user.Name = admin.Name
	user.ID = admin.ID
	user.Country = admin.Country
}
```
