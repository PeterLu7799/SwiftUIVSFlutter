# 轻松对比SwiftUI 和 Flutter

## SwiftUI是什么

![swuftui.png](images/swuftui.png)

今年的WWDC苹果公布了许多大的更新和技术，这其中有一个令开发者非常兴奋的技术就是发布了SwiftUI。一个declarative UI框架用于构建iOS (iPadOS, macOS, watchOS, tvOS)应用。

为什么说开发者会很兴奋，这是因为苹果也加入了现代且先进的declarative UI编程。苹果的开发者们不用再坐在边上看React Native或Flutter带来的如下技术能力：

+ 简化代码
+ 提高开发效率
+ 热更新

Google在今年的I/O‘19大会上也发布了Jetpack Compose，一个新的Android declarative UI框架，可以看出Declarative UI在移动端上的应用越来越多充分说明了它所带来的开发优势。苹果今年宣布SwiftUI正好赶在了这个间隙，也就引起开发者的共鸣。

## Flutter是什么
Flutter是谷歌的移动UI框架，可以快速在iOS和Android上构建高质量的原生用户界面。 Flutter可以与现有的代码一起工作。在全世界，Flutter正在被越来越多的开发者和组织使用，并且Flutter是完全免费、开源的。具有以下特点：

+ Declaraive UI
+ 快速开发
+ 原生的性能
+ 富有表现力，漂亮的用户界面
+ 统一的应用开发体验
+ 访问本地功能和SDK

## Declarative UI是什么

说了很多的declarative UI那具体它什么，它又是怎样工作的哪？众所周知现在的应用程序开发，尤其是UI部分的开发已经变的很复杂，在传统的Objective-C开发的iOS应用中，UI和业务分解不好的UIViewController代码直逼万行甚至几万行，这里大部分是在处理UI展示的数据变化和用户的交互及下面这些UI相关的问题：

+ 事件响应
+ 设备旋转
+ 动态字体大小
+ 黑暗模式
+ 不同主题
+ 用户自定义视图
+ 用户的角色对应视图
+ A/B测试

然后又要添加各种的动画效果来让用户和UI交互起来自然、简单和便捷。所有这些都造成了现在UI开发的复杂性。

在declarative UI之前的”imperative“方式的变成你要做的是：

+ 首先通过UIView构建出登录界面
+ 当用户点击登录按钮时
+ 你会显示一个加载中的View，接着后台请求数据
+ 收据回来后，隐藏加载中的View
+ 重定位到主页或是弹出错误对话框

在这种imperative命令模式中，你根据各种事件去直接更改UI中的各个部分。这种模式的问题是，它看似简单但是在这个界面的业务和状态变的复杂时是很难保证在更新界面时不出现问题。

作为对比的declarative声明模式中，用户界面声明为一个有数据驱动的函数来展示，这里的数据是这个界面的状态(state)，当状态改变时UI会自动通知这个函数来更新展示。所以上面的登录例子变成：如果有用户显示主页，没有用户显示登录页；如果后台处理显示加载中；如果错误显示错误。

下面我们举例说明，如图我们要改变ViewB的子视图从左图到右图

![swuftui.png](images/viewAB.png)

+ Imperative的传统方法，首先找到ViewB的实例然后在它上面修改
	
	```
	ViewB b = getViewB
	b.setColor(red)
	b.clearChildren()
	ViewC c3 = new ViewC(...)
	b.add(c3)
	```
+ Declarative方法，直接返回声明的新ViewB

	```
	if (state) {
		return ViewB(
			color: yellow,
			Childrens: [
				ViewC1,
				ViewC2
			]
		)
	}
	else {
		return ViewB(
			color: red,
			child: ViewC(...),
		)
	}
	```

## 对比两者

接下来我们将通过苹果的SwiftUI课程中创建的应用Landmarks来对比一下SwiftUI和Flutter。为什么选择这个课程用的app哪？是因为网上有开发者用Flutter作了一个高仿的Flutter版的Landmarks应用，这样我们在有的地方就可以利用里面的实现代码做比较，这样更直观。下图是这个app的首页截图对比。

![SwifuUI code](images/flutter_swiftUI.png)


### IDE比较

+ XCode

	![XCode](images/xcode1.png)
	
	XCode对SwiftUI的支持是不用说的，从图中可以看出从左向右依次是工程列表、编辑文件和SwiftUI的预览Canvas。
	
+ Android Studio 

	![Android Studio](images/AndroidStudio1.png)

	左向右依次是工程列表、代码编辑器和Flutter的布局大纲。另外Visual Stuio Code也可以用于Flutter的开发在安装完Flutter的扩展后和Audroid Studio的功能基本一样，只是比Android Studio要轻量级一些。

	我们在苹果的SwiftUI课程中发现Xcode所带的这个预览功能还是十分强大的，在预览上做修改可以直接同步修改代码，并且这个预览界面还有编程的入口，可以通过代码修改预览行为也可以指定预览Canvas的大小或是直接指定设备，这整个过程都不用编译代码。相比Android Studio没有这方面的功能。我们还会在后面具体说一下预览的功能

### UI

+ SwiftUI的View
	
	View是一个Protocal，SwiftUI中的自定义视图都要遵从与这个协议且必须实现body属性来提供你自定义视图的内容和行为。如下图所示代码会在屏幕中间显示文案Hello World!。这里的contenView继承与View接着实现了body属性。另外contenView_Previews结构是用于预览的代码，这里直接创建ContentView，可以直接在右边的预览中看到效果。

	![SwifuUI code](images/xcode_screenshot_1.png)
	
	View还定义了一些操作如：剪切、阴影、描边等。
	
+ Flutter的Widget

	类似的Flutter的UI元素都继承与Widget类，如下代码创建一个无状态的widget在屏幕中间输出Hello World!。它继承与StatelessWidget，StatelessWidget又继承与Widget。这里的build方法是必须实现且返回UI内容的。

	![Flutter code 2](images/flutter_code_2.png)

	可以看到对于declarative UI的SwiftUI和Flutter这里创建一个自定义的UI基本一样，只是Flutter的stateful和stateless在SwiftUI中是没有的。另外Flutter没有实时预览所有也没有预览部分的代码。

### 布局

SwiftUI的Stacks对应Flutter的Flex widgets都是在一维上显示这些子内容。下表是他们对应关系

SwiftUI | Flutter | 描述 
---- | ---- | ----
HStack | Row | 行buju
VStack | Column | 列布局
ZStack | Stack | 重叠布局

如果要实现下面一个Hello world在屏幕中竖向排列居中显示代码如下：

Hello<br/>
World

SwiftUI

![SwifuUI code](images/swiftUI_code_2.png)

Flutter

![SwifuUI code](images/flutter_code_3.png)

从代码可以看出由于SwiftUI没有return语句和children参数而看齐单有简单点。但是Flutter对布局的命名Row、Column和Stack看起来更有感觉。

### 列表

UIKit的Table views在SwiftUI中是List。你可以把所有的子内容放在List里。这对比于UIKit的UITableView去实现多个代理方法是极大的进步。

在Flutter上你可以有多个选择，你可以用ListView来显示多行内容或是用SingleChildScrollView来显示一屏可以滚动的内容。更高级的可以用CustomScrollView它的子视图可以用一系列的Sliver widgets。

### 导航



### 使用Native元素



### 状态管理

+ SwiftUI

+ Flutter

### 总结

+ 代码复杂度

+ 兼容性


## 参考
苹果SwiftUI课程<br/>
https://developer.apple.com/tutorials/swiftui

苹果SwiftUI文档<br/>
https://developer.apple.com/documentation/swiftui

Building the SwiftUI Sample App in Flutter
https://github.com/VGVentures/flutter_landmarks


