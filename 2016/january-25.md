# Player Analytics的新特性帮助你更好的理解用户的行为

> smallSohoSolo翻译 原文链接：[http://android-developers.blogspot.hk/2016/01/new-features-to-better-understand.html](http://android-developers.blogspot.hk/2016/01/new-features-to-better-understand.html)

发送自 Lily Sheringham, Google Play市场开发者

Google Play游戏服务包括Player Analytics，一个在Google Play控制台中供开发者免费使用的报告工具，帮助你分析理解用户的进展，开支和流失。现在你可以看见一个使用Player Analytics的适用方案：试用新的[示范游戏](https://play.google.com/apps/publish/?#BusinessDriversPlace:gt=1059826392430)在Google Play控制台，他是我们在[Auxbrain](https://play.google.com/store/apps/developer?id=Auxbrain+Inc&hl=en_GB)的帮助下制作的，Auxbrain是[Zombie Highway 2](https://play.google.com/store/apps/details?id=com.auxbrain.zh2&hl=en_GB)的开发者，这个[示范游戏](https://play.google.com/apps/publish/?#BusinessDriversPlace:gt=1059826392430)使用了来自于一个真实游戏的随机且匿名的数据，并且让你体验到我们今天宣传的新特性。
Note：你需要一个[Google Play开发者账号](https://support.google.com/googleplay/android-developer/answer/6112435)去访问这个示例程序

### 使用预测分析去运营玩家在他们流失之前

为了帮助你更好的理解玩家的行为，我们用预测功能扩展了Player Analytics中的Player Stats API，这个流失预测功能会尽可能的返回用户将要流失的数据，即，停止玩游戏。以至于你能更新新的游戏内容去召回即将流失的玩家。另外，消费预测功能将会尽可能的返回用户即将进行的消费的数据，你可以在这基础上做一些事情，比如提供离线购买服务或者基于这些分析展示一些广告

### 在新的渠道报告中创建新的图表去快速可视化预测事件队列

渠道报告中现在允许你创建一个渠道图表基于任何的预测事件，例如成就，消费和任何自定义事件。例如，你可以为教学的每一个步骤输出自定义事件，并且使用渠道报告去可视化你的用户在你教学中的退出位置。

![image](http://2.bp.blogspot.com/-ROsTzjmFOE8/VqZZbDalxuI/AAAAAAAAChI/8h3ARxIlwpk/s1600/image00.png)

### 用队列报告测量和比较变化带来的影响和新用户积累的数据

队列报告允许你采集任何事件，例如会话，累计支出和自定义事件，并且可以通过新用户所积累下来的数据去给你的游戏模式提供有价值的改变。例如，你可以预览用户在你更新之前和更新之后的使用行为，这允许你测量和比较更新带来的影响。例如，如果你翻倍你游戏商店中所有道具的价格，你可以在图表中看到用户在你更新之前的数据和更新之后的数据比较。

![image](http://3.bp.blogspot.com/-z1IumLkBm3A/VqZZgnJmEaI/AAAAAAAAChQ/QX9kkrGOcZs/s1600/image01.png)

### Player Stats API更新了对C++，iOS SDK和Unity插件的支持

我们已经更新了对C++，iOS SDK和Unity插件，他们现在均支持Player Stats API，包括基础的用户统计和消费和流失的预测功能。你可以检出[示例程序](https://play.google.com/apps/publish/?#BusinessDriversPlace:gt=1059826392430)和[学习更多Google Play服务知识](https://developers.google.com/games/services/?utm_campaign=play%20services_discussion_analytics_012516&utm_source=anddev&utm_medium=blog).你现在也可以看看[来自于游戏公司Auxbrain的顶级建议去帮助你使用Google Play服务获取成功](http://android-developers.blogspot.co.uk/2015/11/developer-tips-for-success-with-player.html)