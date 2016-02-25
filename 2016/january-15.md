# 在Google Play开发者控制台为你的应用和应用产品创建优惠码

> wizChen翻译 原文链接：[http://android-developers.blogspot.jp/2016/01/create-promo-codes-for-your-apps-and-in.html](http://android-developers.blogspot.jp/2016/01/create-promo-codes-for-your-apps-and-in.html)

来自Yoshi Tamura，Google Play产品经理

在过去的六个多月，Google Play开发者控制台已经添加了许多新的工具，去帮助你在Google Play上提升你的应用或者游戏收入。我们[改进的beta测试](http://android-developers.blogspot.com/2015/07/iterate-faster-on-google-play-with.html)能帮助你收集更多的反馈好让你修复这些问题。[存储清单实验](http://android-developers.blogspot.com/2015/10/learn-top-tips-from-kongregate-to.html)让你在应用的Play Store列表上跑A/B测试。[普遍的应用活动](http://android-developers.blogspot.com/2015/10/go和ogle-play-developer-console.html)和[用户获取](https://support.google.com/googleplay/android-developer/answer/6263332)的性能报告帮助你增加用户量，更好的了解你的市场。

今天开始，你可以在Google Play上生成和分发[优惠码](https://support.google.com/googleplay/android-developer/answer/6321495)给当前的和新的用户，驱动他们来参与。在促销活动选项卡下的开发者控制台，你可以为你的应用程序，游戏和应用产品设置优惠码在自己的营销市场分发（每个应用每季度上至500次）。考虑一下使用优惠码来奖励忠诚的用户和吸引新用户吧。

### 怎么使用优惠码

1. 在开发者控制台选择你的应用
2. 在促销标签下选择**新建促销**

	![](http://3.bp.blogspot.com/-FUh5VUlK1ds/VpqNPD5bMSI/AAAAAAAACgE/fFRiCXCALms/s1600/Dev%2BCosnole%2BBlog.png)
	
3. 在你没有分发优惠码之前审查和接受服务的附加条款。
4. 选择[可用的选项](https://support.google.com/googleplay/android-developer/answer/6321495),然后生成并下载您的优惠码。
5. 通过你的营销渠道分发你的优惠码，比如社交网络，电子邮件，应用的beta测试用户，或者直接在你的应用和游戏上。
6. 用户可以用多种方式来兑换优惠码，包括：<br>
    a. 在Google Play，使用兑换菜单选项<br>
    b. 从你的应用中。在重定向到你的应用之前他们会被引导至Play的校验流程。<br>
    c. 通过以下链接嵌入优惠码(参见下面的提示)。<br>
    
关于在你的应用和游戏中嵌入优惠码的更多细节，请参见在Google Play开发者帮助中心的[这篇文章](https://support.google.com/googleplay/android-developer/answer/6321495)。

### 制作最优惠促销码的小贴士

在运行一个成功的推广之前必须要记住这几件事：

- 每个应用每个季度最多有500次的优惠码分发。
- 你可以将你的代码嵌入到一个URL,这样用户就不需要输入他们了(例如,你在一封电子邮件中发送优惠码)。您可以使用URL:https://play.google.com/store?code={CODE} ({CODE}是事先生成好的促销码)。
- 在应用产品中使用促销码，你应该在你的应用中[实现In-app Promotions](http://developer.android.com/google/play/billing/billing_promotions.html?utm_campaign=play%20games_discussion_promocodes_011516&utm_source=anddev&utm_medium=blog)。记住促销码不能被用于订阅。
- 审查和遵守[促销码的服务条款](https://play.google.com/about/promo-code-developer-terms.html)。

我们希望你找到有意思的方式去使用这些优惠码来发掘新用户和鼓励老粉丝。学习了解更多关于使用这些工具和最佳实践在Google Play上来提升你的业务，下载我们新版开发者手册，["Google Play上应用成功的秘密"](https://play.google.com/store/books/details?id=O2a5CgAAQBAJ)。 
