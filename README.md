# gorm

powerful orm framework for go, supporting pq/mysql/sqlite3.

## Install

`go get -u github.com/geego/gorm`

## Examples

```go
  package main

  import (
    "fmt"
    "github.com/geego/gorm"
    _ "github.com/go-sql-driver/mysql"
  )

  // Model Struct
  type User struct {
    Id   int    `orm:"auto"`
    Name string `orm:"size(100)"`
  }

  func init() {
    // register model
    gorm.RegisterModel(new(User))

    // set default database
    gorm.RegisterDataBase("default", "mysql", "root:root@/my_db?charset=utf8", 30)
  }

  func main() {
    o := gorm.NewOrm()

    user := User{Name: "slene"}

    // insert
    id, err := o.Insert(&user)

    // update
    user.Name = "astaxie"
    num, err := o.Update(&user)

    // read one
    u := User{Id: user.Id}
    err = o.Read(&u)

    // delete
    num, err = o.Delete(&u) 
  }
```

## License

Inspired by `beego` and under [BSD License](./LICENSE)
