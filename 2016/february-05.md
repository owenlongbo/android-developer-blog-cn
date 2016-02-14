# Android Studio 2.0 - Beta

来自 [JamalEason](https://www.google.com/+JamalEason),Android产品经理

Android Studio 2.0是最新的官方Android IDE发行版，专注于提升了构建和虚拟机的速度来增加App
开发体验。打造了新的特性，像"即时运行功能"，他能让你更快的编辑并且看到代码变化，还有新的更快的Android虚拟机， Android Studio 2.0是你不想错过的更新。正在准备最后的发行版，你可以在[Beta release channel](http://tools.android.com/download/studio/beta)下载到Android Studio 2.0 Beta。总的来说，Android Studio 2.0 release有一下新特性：

 - *在Bate版中存在* **即时运行功能（Instant Run）**：能够更快的编码和部署程序
 - *在Bate版中存在* **Android模拟器（Android Emulator）** [Brand new emulator](http://android-developers.blogspot.com/2015/12/android-studio-20-preview-android.html)甚至比真实的设备还要快，并且存在一个新的用户接口。
 - *在Bate版中存在* **Google App Indexing 继承和测试（Google App Indexing Integration & Testing）**：添加[App Indexing](http://g.co/AppIndexing/AndroidStudio)进你的App，帮助你接触用户，在第一个Android Studio 2.0预览版中，你能添加Indexing Code在你的代码中。在测试版中，你能测试并且使你的URL链接在整个IDE内部生效
 - **Fast ADB**：用platform-tools 23.1.0提供的ADB能使安装和推送文件快5倍！
 - **GPU预览器（GPU Profiler Preview）**：对于图形增强的应用，你现在能更加形象的看OpenGL ES代码去优化你的游戏或应用。
 - **继承了IntelliJ 15（Integration of IntelliJ 15）**：Android Studio是基于高效的IntelliJ编辑器。查看IntelliJ的新特性[这里](https://www.jetbrains.com/idea/whatsnew/)

 通过这个视频来看看Android Studio2.0的亮点
 [视频传送门,需要翻墙](https://youtu.be/xxx3Fn7EowU?list=PLWz5rJ2EKKc_w6fodMGrA1_tsI3pqPbqa)

 ### 即时运行功能

 我们第一看见[带有即时运行功能的版本](http://android-developers.blogspot.com/2015/11/android-studio-20-preview.html)是在11月份,这个最新的测试版包含了一个新的能力名为Cold Swap。“即时运行功能”在Andrid Studio 2.0中允许你非常快速的改变你正在正式设备或者虚拟机中运行的App，取代了每更改一行代码都要重新构建和部署的问题，Android Studio2.0将会尝试去增量构建并且仅仅推送改变或者增加的代码和资源。取决于你代码的改变，你能在一秒钟之内看见你改变的结果。你能简单的更新你的app通过最新的Gradle插件 ( 'com.android.tools.build:gradle:2.0.0-beta2’ )，这个新特性能让你在你修改代码的时候节约时间，如果你的项目正在处于即时运行中，你能看见一个闪电的图标在你的Run按钮上
 
 在这个情况下，Android Studio2.0会审查你的代码当你第一次构建和部署你的app在你的设备上以决定在什么位置置换代码和资源，即时运行特性会在最大的基础上更新你的app，并且自动的使用以下三种函数之一去更新你的app。

 - How Swap：当函数被更改的时候（包括构造函数），改变会被热部署，你的程序会正常的运行，并且新的更改会在函数被下一次调用的时候应用，
 - Warm Swap：当资源被更改的时候，会使用Warm Swap。他比较像Hot Swap，但是当前的Activity会重启，你在屏幕上会看见一个由Activity重启而导致的轻微的闪烁。
 - *新的特性* Cold Swap：他将会很快的重启整个程序。典型的代码结构改变，包括更改类的层次，函数的签名，静态资源的初始化，或者变量的改变。Cold Swap会生效，当你的target api大于等于21的时候。

 ###App Indexing

 在Android Studio2.0中支持App Indexing现在更加的简单了，App Indexing让你的app呈现在使用google搜索的用户面前，它通过索引你在Mainifest文件中提供的URL Pattern的和使用API调用来让你的程序中的内容提供给现有的和新的用户。特别的是，当你给你的app内容中添加URL的之后，你的用户能直接转到这些链接通过他们设备上google搜索的结果。

 -
