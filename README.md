# Swift进行中
###MARK / TODO / FIXME
在 Objective-C 里，预处理指令 #pragma mark 用来把功能区分成有意义的，易于导航的章节。在 Swift 里，没有预处理指令（最接近的是相似的-井号编译配置），但同样可以用注释达到效果 // MARK:。

在 Xcode 6β4 中，以下注释将出现在 Xcode 的代码导航（source navigator）中：

// MARK: (等同于 #pragma，记号后紧跟一个横杠 (-) 会被编译成水平分割线)

// TODO:

// FIXME:

其他常规注释标记，如 NOTE 和 XXX 在 Xcode 中不能被识别。
```
