#UIScrollView 和 Auto Layout 
>  UIScrollView 在 Auto Layout 是一个很特殊的 view，对于 UIScrollView 的 subview 来说，它的 leading/trailing/top/bottom space 是相对于 UIScrollView 的 contentSize 而不是 bounds 来确定的，所以当你尝试用 UIScrollView 和它 subview 的 leading/trailing/top/bottom 来互相决定大小的时候，就会出现「Has ambiguous scrollable content width/height」的 warning。 
因为 UIScrollView 本身的 leading/trailing/top/bottom 变得不好用，所以我习惯的做法是在 UIScrollView 和它原来的 subviews 之间增加一个 content view，这样做的好处有：

> * 不会在 storyboard 里留下 error/warning
* 为 subview 提供 leading/trailing/top/bottom，方便 subview 的布局
* 通过调整 content view 的 size（可以是 constraint 的 IBOutlet）来调整 contentSize
* 不需要 hard code 与屏幕尺寸相关的代码
* 更好地支持 rotation

为了实现在UIScrollView子视图Label根据内容自动撑满并且可滚动，按照上文的思路实现一个间的DEMO。试图结构如下：

> ***UIView --> UIScrollView --> UIView -->UILabel***

NSLayoutConstraints如下：

![](https://image.ibb.co/kDH6XF/Screen_Shot_2017_08_04_at_2_34_59_PM.png)
