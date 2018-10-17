|swift學習筆記 |
| ------ |
- closure

```sh
------------------------------------------
//正常func並呼叫
func show() -> () {
    print("this is func.")
}
show()
let show1 = show
show1()
------------------------------------------
//改成closure in 是為了區分參數跟程式碼區塊
let show = {
    () -> () in
    print("this is closure.")
}
show()
------------------------------------------
//closure省略() -> () 及 in
let show = {
    print("this is closure.")
}
show()
------------------------------------------
//closure 傳入function
func repeatTask(count: Int, task: () -> ()) {
    for _ in 1...count {
        task()
    }
}
func eat() {
    let message = "吃飯"
    print(message)
}
func sleep() {
    let message = "睡覺"
    print(message)
}
//呼叫repeatTask 傳入function參數
repeatTask(count: 2, task: eat)
repeatTask(count: 1, task: sleep)
------------------------------------------
//呼叫repeatTask 傳入closure參數,如此可以省略eat、sleep function的定義
repeatTask(count: 2, task: {() -> () in
    let message = "吃飯"
    print(message)
})
repeatTask(count: 1, task: {() -> () in
    let message = "睡覺"
    print(message)
})
------------------------------------------
//呼叫repeatTask 傳入closure參數並簡化() -> () in
repeatTask(count: 2, task: {
    let message = "吃飯"
    print(message)
})
repeatTask(count: 1, task: {
    let message = "睡覺"
    print(message)
})
------------------------------------------
//trailing closure尾隨閉包,將上面closure的參數名省略及獨立程式碼區塊到最後面,提升程式可讀性
repeatTask(count: 2) {
    let message = "吃飯"
    print(message)
}
repeatTask(count: 1) {
    let message = "睡覺"
    print(message)
}
------------------------------------------
//帶參數closure
let listen = {(singer: String, song: String) -> () in
    let message = "聽 \(singer) 唱 \(song)"
    print(message)
}
listen("五月天", "離開地球表面")
------------------------------------------
```
- generic
```sh
------------------------------------------
//generic 泛型
class Fox {
    func run() {
        print("pet is running.")
    }
}
class Rabbit {
    func jump() {
        print("pet is jumping.")
    }
}
class LittlePrince<T> {
    var pet: T?
}
let prince = LittlePrince<Fox>()
prince.pet = Fox()
prince.pet?.run()

let prince2 = LittlePrince<Rabbit>()
prince2.pet = Rabbit()
prince2.pet?.jump()
------------------------------------------
//定義可以傳入兩個型別的泛型
class LittlePrince2<T1, T2> {
    var pet1: T1?
    var pet2: T2?
}
let prince3 = LittlePrince2<Fox, Rabbit>()
prince3.pet1 = Fox()
prince3.pet2 = Rabbit()
prince3.pet1?.run()
prince3.pet2?.jump()

------------------------------------------
```






