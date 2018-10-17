# swift

## closure

```sh
//正常func並呼叫
func show() -> () {
    print("this is func.")
}
show()
let show1 = show
show1()

//改成closure in 是為了區分參數跟程式碼區塊
let show = {
    () -> () in
    print("this is closure.")
}
show()

//closure省略() -> () 及 in
let show = {
    print("this is closure.")
}
show()
```
