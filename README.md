# gorm

powerful orm framework for go, supporting pq/mysql/sqlite3.

## License
  - full go type support
  - easy for usage, simple CRUD operation
  - auto join with relation table
  - cross DataBase compatible query
  - Raw SQL query / mapper without orm model
  - full test keep stable and strong

## Install
```
go get github.com/geego/gorm
```

## How to use
### Simple Usage
```
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
    orm.RegisterModel(new(User))

    // set default database
    orm.RegisterDataBase("default", "mysql", "root:root@/my_db?charset=utf8", 30)
  }

  func main() {
    o := orm.NewOrm()

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

fork form [beego/orm](https://github.com/astaxie/beego/tree/master/orm)

orm source code is licensed under the Apache Licence, Version 2.0 (http://www.apache.org/licenses/LICENSE-2.0.html). this library base on beego orm. thanks beego team and astaxie.
