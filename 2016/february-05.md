# Android Studio 2.0 - Beta

>smallSohoSolo翻译 原文链接[http://android-developers.blogspot.jp/2016/02/android-studio-20-beta.html](http://android-developers.blogspot.jp/2016/02/android-studio-20-beta.html)

来自 [JamalEason](https://www.google.com/+JamalEason),Android产品经理
 
Android Studio 2.0是最新的官方Android IDE发行版，专注于提升了构建速度和虚拟机速度来增强App
开发体验。打造了新的特性，像"即时运行功能"，他能让你更快的编辑并且即时看到代码变化，还有新的更快的Android虚拟机， Android Studio 2.0是你不想错过的更新。正在准备最后的发行版，你可以在[Beta release channel](http://tools.android.com/download/studio/beta)下载到Android Studio 2.0 Beta。总的来说，Android Studio 2.0 release有一下新特性：

 - *在Bate版中存在* **即时运行功能（Instant Run）**：能够更快的编写和部署程序
 - *在Bate版中存在* **Android模拟器（Android Emulator）** [Brand new emulator](http://android-developers.blogspot.com/2015/12/android-studio-20-preview-android.html)甚至比真实的设备还要快，并且存在一个新的用户接口。
 - *在Bate版中存在* **Google App 索引集成和测试（Google App Indexing Integration & Testing）**：添加[App Indexing](http://g.co/AppIndexing/AndroidStudio)进你的App，帮助你重新吸引用户，在第一个Android Studio 2.0预览版中，你能在你的代码中添加索引代码。在测试版中，你现在可以在IDE中测试和验证你App中的Url链接。
 - **Fast ADB**：用platform-tools 23.1.0提供的ADB能使安装和推送文件快5倍！
 - **GPU预览器（GPU Profiler Preview）**：对于图形增强的应用，你现在可以直观地通过你的OpenGL ES代码一步步去优化你的应用程序或游戏。
 - **继承了IntelliJ 15（Integration of IntelliJ 15）**：Android Studio是基于高效的IntelliJ编辑器。查看IntelliJ的新特性[这里](https://www.jetbrains.com/idea/whatsnew/)

 通过这个视频来看看Android Studio2.0的亮点
 [视频传送门,需要翻墙](https://youtu.be/xxx3Fn7EowU?list=PLWz5rJ2EKKc_w6fodMGrA1_tsI3pqPbqa)

### 即时运行功能

 我们第一看见[带有即时运行功能的版本](http://android-developers.blogspot.com/2015/11/android-studio-20-preview.html)是在11月份,这个最新的测试版包含了一个新的能力名为Cold Swap。“即时运行功能”在Andrid Studio 2.0中允许你非常快速的改变你正在正式设备或者虚拟机中运行的App，取代了每更改一行代码都要重新构建和部署的问题，Android Studio2.0将会尝试去增量构建并且仅仅推送改变或者增加的代码和资源。取决于你代码的改变，你能在一秒钟之内看见你改变的结果。你能简单的更新你的app通过最新的Gradle插件 ( 'com.android.tools.build:gradle:2.0.0-beta2’ )，这个新特性能让你在你修改代码的时候节约时间，如果你的项目正在处于即时运行中，你能看见一个闪电的图标在你的Run按钮上
 
 ![](https://4.bp.blogspot.com/-DBI2jT5129Y/VrT23xFifmI/AAAAAAAACjY/KsyAKxaos10/s1600/image06.png)

 在这个情况下，Android Studio2.0会审查你的代码当你第一次构建和部署你的app在你的设备上以决定在什么位置置换代码和资源，即时运行特性会在最大的基础上更新你的app，并且自动的使用以下三种函数之一去更新你的app。

 - Hot Swap：当函数被更改的时候（包括构造函数），改变会被Hot Swap，你的程序会正常的运行，并且新的更改会在函数被下一次调用的时候应用，
 - Warm Swap：当资源被更改的时候，会使用Warm Swap。他比较像Hot Swap，但是当前的Activity会重启，你在屏幕上会看见一个由Activity重启而导致的轻微的闪烁。
 - *新的特性* Cold Swap：他将会很快的重启整个程序。典型的代码结构改变，包括更改类的层次，函数的签名，静态资源的初始化，或者变量的改变。Cold Swap会生效，当你的target api大于等于21的时候。

### App Indexing

 在Android Studio2.0中支持App Indexing现在更加的简单了，App Indexing让你的app呈现在使用google搜索的用户面前，它通过索引你在Mainifest文件中提供的URL Pattern的和使用API调用来让你的程序中的内容提供给现有的和新的用户。特别的是，当你给你的app内容中添加URL的之后，你的用户能通过google搜索到的结果直接跳转到App中的内容页面。

 - **Code Generation（代码生成器）** 在Android Studio 2.0预览版中引入了，你能在AndroidManifest.xml或者Activity method中点击它（或者去Code → Generate…→ App Indexing API Code）去添加Http url的代码在你的Mainifest文件或者程序中
 
 ![](https://4.bp.blogspot.com/-O_SXnqoLMI8/VrT_1TwFAEI/AAAAAAAACj8/WFRMQtxcjTE/s1600/image01.png)

 - *在Bate版中存在* **URl测试和验证（URL Testing & Validation）** 在新的Android Studio 2.0 Beta中现在可以验证并且检查你用构建工具添加的Url的返回结果了（Tools → Android → Google App Indexing Test）学些更多关于App Indexing索引[在这里](http://g.co/AppIndexing/AndroidStudio)
 
 ![](https://1.bp.blogspot.com/-EG5o4HbkjI8/VrUBAGnYLoI/AAAAAAAACkI/V13CcOVHtzw/s1600/image00.png)

 ![](https://1.bp.blogspot.com/--56gUtBaOdk/VrUBQBIdaXI/AAAAAAAACkM/lF_0u0SliPY/s1600/image05.png)

### Android模拟器

 *在Bate版中存在* [新的更快的Adnroid模拟器](http://android-developers.blogspot.com/2015/12/android-studio-20-preview-android.html)包括很多修复和对这次的测试发行版的增强。值得注意的是，我们在模拟器的功能菜单中更新了旋转控制和多点触控支持以使用pinch & zoom手势去帮助测试App。使用多点触控特性，按住Alt键并且点击鼠标右键在点的中心或者左击你的鼠标并且拖动去缩放
图片

 ![](https://4.bp.blogspot.com/-w0KlXxaj-Bg/VrT3cvcuNzI/AAAAAAAACjs/RCwQO4nbb_w/s1600/image07.gif)

### 接下来是什么

 Android Studio 2.0是一个重要的发行版，并且现在是一个好的时机去使用他的新特性在你的工作中，测试发行版接近稳定发行版的质量，含有相对较少的bug。但是在这些测试发行版中，bug仍然存在，所以如果你发现一个问题，让我们知道以至于我们可以去修复他。如果你准备使用Android Studio，你能检查更新在测试通道通过顶部菜单(Help → Check for Update [Windows/Linux] , Android Studio → Check for Updates [OS X])，当你更新好了测试版，你能使用新版本的Android Studio和Android模拟器。

 联系我们，Android Studio开发团队，在[Google+](https://plus.google.com/communities/114791428968349268860)
