# Marshmallow和用户数据

>smallSohoSolo翻译 原文链接[http://android-developers.blogspot.jp/2016/02/marshmallow-and-user-data.html](http://android-developers.blogspot.jp/2016/02/marshmallow-and-user-data.html)

发送自 Joanna Smith，Advocate和Giles Hogben的开发者, 任职于Google隐私团队。

Marshmallow设计了很多改变去帮助你的App去管理用户数据，目的是让开发者能更加轻松的做对的事，所以Android 6.0 Marshmallow我们让你的一切在控制之中。

这篇文章强调了在你的App运行时候请求权限和硬件管理的时候如何**获取用户的信任**，并且给你指明了[最好的实践](http://developer.android.com/training/best-permissions-ids.html?utm_campaign=android_discussion_marshmallow_020116&utm_source=anddev&utm_medium=blog)案例去澄清你的App的目的。

###权限上的改变

在Marshmallow中，**权限已经从安装时请求移到了运行时请求**，这在SDK23中是强制性的改变，那意味着在Android6.0中这将到所有的开发者和程序，你的App无论如何都要更新，所以你应该好好想想怎么做。

运行时权限意味着你的App现在可以在当前的上下文中请求敏感数据，这给你一个机会去解释为什么需要这条权限

权限现在也被以群为单位组织起来，所以现在用户可以在不理解技术术语的情况下在请求权限的时候做一个明智的决定。因为用户有了选择的权利，他们现在可以决定不给予一个权限，或者撤回一个以前授予的权限。所以你的App需要去考虑请求权限失败之后的问题，还有做好在用户拒绝你之后的交互。

###标识符的改变

另一个影响用户信任的方面就是用用户的数据去做对的事。在Marshmallow中，我们为了引导开发者这么做关闭了许多数据的访问权限。

最明显的是**本地Wifi和蓝牙的MAC地址将不可获取**，getMacAddress()函数和BluetoothAdapter.getDefaultAdapter().getAddress()函数现在都会返回02:00:00:00:00:00。

然而，**Google play服务现在提供实例ID**，可以标记一个正在设备中运行的应用程序实例，实例ID可以很可靠的替换设备唯一的硬件ID，这个ID不会因为重置或者返厂而被更改。详情查看Google开发者的这篇文章，[What is Instance ID?](https://developers.google.com/instance-id/?utm_campaign=android_discussion_marshmallow_020116&utm_source=anddev&utm_medium=blog)。

###接下来是什么

用户的信任度很大程度上依赖于他们感受到的和看到的，处理不当的权限和标识控制会增加用户被追踪的风险。并且会让用户感觉你的App并不关心用户。所以为了帮助你解决这个问题，我们做了新的方案去帮助开发者让他们的用户感受到他们的app在做正确的事。

- 理解[权限和用户数据是怎么联系的](http://developer.android.com/training/articles/user-data-overview.html?utm_campaign=android_discussion_marshmallow_020116&utm_source=anddev&utm_medium=blog)
- 学习更多[关于权限使用最好的实践](http://developer.android.com/training/articles/user-data-permissions.html?utm_campaign=android_discussion_marshmallow_020116&utm_source=anddev&utm_medium=blog)
- 发现[关于唯一标示的最好实践](http://developer.android.com/training/articles/user-data-ids.html?utm_campaign=android_discussion_marshmallow_020116&utm_source=anddev&utm_medium=blog)，清晰的展现除了在Marshmallow上的变化

多么愉快的编程体验！希望你的App会让用户更加开心~~
