# 游戏权限在2016将要被修改了！

> smallSohoSolo翻译 原文链接：[http://android-developers.blogspot.jp/2016/01/play-games-permissions-are-changing-in.html](http://android-developers.blogspot.jp/2016/01/create-promo-codes-for-your-apps-and-in.html)

发送自，Wolff Dobson，开发人员代表

我们正在逐步减少玩家登陆上的冲突和不必要的权限请求通过改变游戏API，新的特性是：

- 玩家现在只需要登陆一次，以后都不需要登陆了
- 玩家再也不用为了使用Play Games Service去升级他们的账号为Google+
- 只要玩家在第一次游戏的时候登陆，他们不需要在未来的任何游戏中登陆，账号会自动登陆。
- 小贴士：玩家可以通过Play Games App中的设置去关闭自动登陆

推荐：

- 玩家第一次登陆之后，开始游戏时候玩家将不会看见任何登陆UI
- 不要为任何特定的游戏定制登陆画面，登陆将会在每次打开游戏的时候自动进行

为了尊重用户的隐私并且避免暴露用户的真实姓名，我们有改变玩家游戏ID的方法

- 对于已经存在的玩家：游戏将会继承他们的Google+ ID（在某些文档中也叫作“player ID”）在他们登陆的时候
- 对于新的玩家：游戏将会给予他一个在之前没有被玩家使用的新的ID

### 潜在问题

大多数游戏应该发现服务无法被中断和改变，这种情况屈指可数，然而，现在被要求有一些改变。

下面是一些问题，伴随着一些解决方案。

他们是：

1. 请求Google+权限范围不成功时
	* Issue:用户在请求不成功的时候，会弹出烦人的同意窗口
	* 解决方案：不要请求任何额外的权限范围，除非你特别需要他们
2. 使用Play Games 玩家ID在非游戏类Google Api
   * Issue:在其他的接口你不会获得有效的返回
   * 解决方案：不要在其他的Google Api中使用其他的游戏ID
3. 使用客户端访问服务端获取Token
   * Issue：你的Token可能不包含你所要查找的信息
   * 解决方案：使用新的GetServerAuthCode API替换他

让我们看一下这些问题的细节

###Issue：请求不必要的权限范围**
早起版本我们的例子和文档像这样创建了一个GoogleApiClient

```java
// Don’t do it this way!  
 GoogleApiClient gac = new GoogleApiClient.Builder(this, this, this)  
           .addApi(Games.API)  
           .addScope(Plus.SCOPE_PLUS_LOGIN) // The bad part  
           .build();  
 // Don’t do it this way!  
```

在这个用例中，开发者请求了plus.login权限，**如果你请求plus.login权限，你的用户将会看到一个确认框**

###解决办法：只请求你需要的权限
在你的GoogleApiClient中去掉请求那些你以后不会用到的无用的权限

```java
 // This way you won’t get a consent screen  
 GoogleApiClient gac = new GoogleApiClient.Builder(this, this, this)  
           .addApi(Games.API)  
           .build();  
 // This way you won’t get a consent screen  
```

###对于Google+的用户

如果你的App使用了Google+的特性，例如请求用户在Google+的社交圈中的真实国家地址，那意味着只有新用户将会被请求使用G+信息去使用你的游戏（存在已经注册游戏的用户，但是他没有同意使用此权限）

要求Google+杭虎使用你的游戏，你需要更改你的游戏Gpi使用依照此方法：

```java
 .addApi(Games.API, new GamesOptions.Builder()  
                       .setRequireGooglePlus(true).build())  
```

这将会保证你的游戏会继续请求必要的权限，继而获取到用户的真实社交位置和姓名。

###Issue：使用游戏ID作为其他的ID

如果你调用Games.getCurrentPlayerId() API，返回的是在你游戏中经过鉴定的游戏玩家的信息。传统情况下，这个值将会被放进他的Api中，例如Plus.PeopleApi.load，但是在新的模型中，它将失效。**游戏ID将仅仅在用户使用游戏的时候被获取到**

###解决方案：不要混用ID

我们看见过一个通用的模式：

- 使用GoogleAuthUtil去获取一个可靠的Token
- 发送这个Token给服务端
- 在服务端，Google验证求情，最通用的办法是请求[https://www.googleapis.com/oauth2/v1/tokeninfo](https://www.googleapis.com/oauth2/v1/tokeninfo)，然后查看返回值

首先，这不是被推荐的做法，并且在以后也不会被推荐

为什么不要这样做：

- 他要求你的App去了解当前使用者的信息，并且会保持请求GET_ACCOUNTS权限。在Android M中中，在你的App运行时将会要求用户去分享他们的信息，这是很吓人的
- Token信息不是为了这个场景设计的，这个设计主要是作为一个调试工具，并不是一个生产环境下的Api，那意味着这个Api被调用的频率会被限制。
- Token中所携带的user_id可能不会是新模型的id，并且即时当前是相同的，这个值将不会跟新用户的Player ID相同。
- Token会在不确定的时候到期（令牌的过期时间不会被保证）
- 在服务端使用客户端令牌去请求数据会受到额外的检查，以确保他不在不同的应用程序中被使用

###解决方案：使用新的GetServerAuthCode工作流

幸运的是，解决方案是已知的，并且基本上和我们[推荐的服务端鉴定方案](https://developers.google.com/identity/sign-in/web/server-side-flow?utm_campaign=play%20games_discussion_permissions_012316&utm_source=anddev&utm_medium=blog)是一样的.

1. 更新你的Google Play Service SDK版本到8.4.87以上
2. 创建一个Server ID如果你没有的话
	1. 去Google Play开发者控制台并且选择你的项目
	2. 在左侧导航栏选择，API Manager，接着选择证书
	3. 选择New Credentials，然后选择OAuth Client ID 
	4. 选择Web Application，然后填写一些你的应用的有效信息
	5. 这个Web Application的Cliend Id就是你的服务端使用的ID
3. 在你的游戏中，用常用的方法连接GoogleApiClient
4. 连接之后，调用Api：
	1. Games.getGamesServerAuthCode(googleApiClient, “your_server_client_id”)
	2. 如果你在之前使用了GoogleAuthUtil，你可能会大概像这样开一个后台线程：

	```java
	 // Good way  
	 {  
	      GetServerAuthCodeResult result =   
	           Games.getGamesServerAuthCode(gac, clientId).await();  
	      if (result.isSuccess()) {  
	           String authCode = result.getCode();  
	            // Send code to server.  
	   }  
	 }  
	 // Good way  
	```

5. 发送登陆信息给你的服务端，和往常一样
6. 在你的服务端，制作一个RPC对https://www.googleapis.com/oauth2/v4/token，去用登陆码交换访问Token，有可能会用到[Google Apis Client Library](https://developers.google.com/discovery/libraries?hl=en?utm_campaign=play%20games_discussion_permissions_012316&utm_source=anddev&utm_medium=blog)
	1. 你需要提供server client ID，server client secret（当你在开发者控制台中创建server client ID时会被列出），和登陆码
	2. 具体更多信息请查看:[https://developers.google.com/identity/protocols/OAuth2WebServer?utm_campaign=play%20games_discussion_permissions_012316&utm_source=anddev&utm_medium=blog#handlingresponse](https://developers.google.com/identity/protocols/OAuth2WebServer?utm_campaign=play%20games_discussion_permissions_012316&utm_source=anddev&utm_medium=blog#handlingresponse)
	3. 有可能的是：你需要使用[Google Apis Client Library](https://developers.google.com/discovery/libraries?hl=en?utm_campaign=play%20games_discussion_permissions_012316&utm_source=anddev&utm_medium=blog)去让这个流程更加的容易
7. 一旦你获取到了访问的Token，你现在可以使用Token调用www.googleapis.com/games/v1/applications/<app_id>/verify/
	1. 把Token放在Hearder中像这样，
	
		```java
		“Authorization: OAuth <access_token>”
		```
		
	2. 返回值将会包含用户的Player ID，这个ID是当前用户的正确ID
	3. 这个Token也可以被用于在服务端和服务端之间请求。

Note：如果将Token发给你的web app,这个Api仅仅会返回一个200.

###总结

这将会非常的清晰，如果你什么都不做，除非你非常明确的依赖Google+特性，在功能上你将看不到任何的改变，并且会有一个顺畅的登陆体验

如果你这样做：
	1. 不使用他们请求Google+权限，这是一个好主意从现在开始停止使用他们
	2. 发送Token给你的服务端，我们建议你使用getGamesServerAuthCode()去替换他。

非常感谢，请制作更加精彩的游戏吧！