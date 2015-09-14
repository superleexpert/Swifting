# Swift进行中
##MARK / TODO / FIXME 的使用
在 Objective-C 里，预处理指令 #pragma mark 用来把功能区分成有意义的，易于导航的章节。在 Swift 里，没有预处理指令（最接近的是相似的-井号编译配置），但同样可以用注释达到效果 // MARK:。

在 Xcode 6β4 中，以下注释将出现在 Xcode 的代码导航（source navigator）中：

// MARK: (等同于 #pragma，记号后紧跟一个横杠 (-) 会被编译成水平分割线)

// TODO:

// FIXME:

其他常规注释标记，如 NOTE 和 XXX 在 Xcode 中不能被识别。
##weak和unowned的作用和区别
如果您是一直写 Objective-C 过来的，那么从表面的行为上来说 unowned 更像以前的 unsafe_unretained，而 weak 就是以前的 weak。用通俗的话说，就是 unowned 设置以后即使它原来引用的内容已经被释放了，它仍然会保持对被已经释放了的对象的一个 "无效的" 引用，它不能是 Optional 值，也不会被指向 nil。如果你尝试调用这个引用的方法或者访问成员属性的话，程序就会崩溃。而 weak 则友好一些，在引用的内容被释放后，标记为 weak 的成员将会自动地变成 nil (因此被标记为 @weak 的变量一定需要是 Optional 值)。关于两者使用的选择，Apple 给我们的建议是如果能够确定在访问时不会已被释放的话，尽量使用 unowned，如果存在被释放的可能，那就选择用 weak。

[来自这里](http://swifter.tips/retain-cycle/)
##闭包Closure
示例：

    {  
       (a:Int,b:Int)->Int in  
  
       return a+b  
    }  
闭包与函数的主要区别是少了func函数名;所以,函数与闭包的主要区别就是闭包是匿名的.

闭包的使用：闭包赋值给一个变量之后,该变量可以直接当函数使

    var plus =  
    {  
        (a:Int,b:Int)->Int in  
  
        return a+b  
    }  

##泛型
在尖括号里写一个名字来创建一个泛型函数或者类型。

func repeatItem<Item>(item: Item, numberOfTimes: Int) -> [Item] {
    var result = [Item]()
    for _ in 0..<numberOfTimes {
        result.append(item)
    }
    return result
}
repeatItem("knock", numberOfTimes:4)
你也可以创建泛型函数、方法、类、枚举和结构体。

// Reimplement the Swift standard library's optional type
enum OptionalValue<T> {
    case None
    case Some(T)
}
var possibleInteger: OptionalValue<Int> = .None
possibleInteger = .Some(100)
在类型名后面使用where来指定对类型的需求，比如，限定类型实现某一个协议，限定两个类型是相同的，或者限定某个类必须有一个特定的父类

func anyCommonElements <T, U where T: SequenceType, U: SequenceType, T.Generator.Element: Equatable, T.Generator.Element == U.Generator.Element> (lhs: T, _ rhs: U) -> Bool {
    for lhsItem in lhs {
        for rhsItem in rhs {
            if lhsItem == rhsItem {
                return true
            }
        }
    }
    return false
}
anyCommonElements([1, 2, 3], [3])


