|swift學習筆記 |
| ------ |
## function 內外部標籤
```sh
func show (name:String) {
    print("我是\(name)王")
}
//呼叫函式帶標籤內外標籤一樣
show(name: "寶寶")

func show0 (who name:String) {
    print("我是無敵\(name)王")
}
//呼叫函式帶外部標籤
show0(who:"寶寶")

func show1 (_ name:String) {
    print("我是超級\(name)王")
}
//呼叫函式不帶標籤
show1("寶寶")

```
```sh
//結果
我是寶寶王
我是無敵寶寶王
我是超級寶寶王
```
## closure

```sh
//正常func並呼叫
func show() -> () {
    print("this is func.")
}
show()
let show1 = show
show1()
```
```sh
//改成closure in 是為了區分參數跟程式碼區塊
let show = {
    () -> () in
    print("this is closure.")
}
show()
```
```sh
//closure省略() -> () 及 in
let show = {
    print("this is closure.")
}
show()
```
```sh
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
```
```sh
//呼叫repeatTask 傳入closure參數,如此可以省略eat、sleep function的定義
repeatTask(count: 2, task: {() -> () in
    let message = "吃飯"
    print(message)
})
repeatTask(count: 1, task: {() -> () in
    let message = "睡覺"
    print(message)
})
```
```sh
//呼叫repeatTask 傳入closure參數並簡化() -> () in
repeatTask(count: 2, task: {
    let message = "吃飯"
    print(message)
})
repeatTask(count: 1, task: {
    let message = "睡覺"
    print(message)
})
```
```sh
//trailing closure尾隨閉包,將上面closure的參數名省略及獨立程式碼區塊到最後面,提升程式可讀性
repeatTask(count: 2) {
    let message = "吃飯"
    print(message)
}
repeatTask(count: 1) {
    let message = "睡覺"
    print(message)
}
```
```sh
//帶參數closure
let listen = {(singer: String, song: String) -> () in
    let message = "聽 \(singer) 唱 \(song)"
    print(message)
}
listen("五月天", "離開地球表面")
```
## generic
```sh
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
//定義可以傳入一個型別的泛型
class LittlePrince<T> {
    var pet: T?
}
let prince = LittlePrince<Fox>()
prince.pet = Fox()
prince.pet?.run()

let prince2 = LittlePrince<Rabbit>()
prince2.pet = Rabbit()
prince2.pet?.jump()
```
```sh
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

```
## access control 權限管理 共５種
- swift不只可以針對屬性property及方法function權限控管，像class、struct、enum、protocol、initializer...亦可．

| 權限修飾詞 | 敘述 | 限制 |
| ------ | ------ | ------ |
| open | 最公開的權限，可讓別的模組使用，例如framework函式庫，主要是要讓其他app也可以使用 | 僅能用於class的屬性及方法 |
| public | 相較於open權限，可宣告於struct、enum宣告的型別，並讓其他模組使用 | 宣告為public的class僅能讓同一個模組中的class繼承，宣告為public的屬性property及方法function僅能讓同一個模組中的class覆寫 |
| internal | 沒特別註明修飾詞，預設即為internal | 只能在定義的模組內使用 |
| fileprivate | 檔案私有權限 | 只能在宣告的檔案裡使用 |
| private | 私有權限 | 最私密的權限，只能在宣告的地方使用 |

## error handling
- 自定義一個錯誤enum須遵守swift內建的error協定
```sh
//程式寫不好的錯誤原因
enum ProgrammingError: Error {
    case lazyProblem
    case PlayTooMuchProblem
    case PracticeTooLessProblem
    case CanNotUnderstandProblem
}
```

