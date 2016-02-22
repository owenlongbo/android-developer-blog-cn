# 让你的应用服务器接入谷歌登录

> wizChen翻译 原文链接[http://android-developers.blogspot.jp/2016/01/using-google-sign-in-with-your-server.html](http://android-developers.blogspot.jp/2016/01/using-google-sign-in-with-your-server.html)

来自 Laurence Moroney, 主要开发人员

使用Google登录是Android博客系列的第三部分，你可以在你的Android应用上使用世界级的安全登录服务。在[第一部分](http://android-developers.blogspot.com/2015/11/improvements-to-sign-in-with-google.html)，我们讨论了谷歌登录给你的应用所带来的用户体验的提升。[第二部分](http://android-developers.blogspot.com/2015/12/api-updates-for-sign-in-with-google.html)我们更深入的分析出客户端改为Google登录API会让你编写代码更加的轻松。

在这篇博客中，我们将会演示如何在你的服务器后端使用谷歌登录验证。使用这种验证方式，用户可以安全的登录去访问他们在你服务器上的数据。

### 在服务器上使用凭证

首先，我们来看一下一个用户登录你的应用会发生什么。考虑一下这种情况：你开发的一个应用是基于用户位置给用户派送食物的。他们登录你的应用，应用就可以拿到用户的信息。然后你就可以把他们的地址和订单存储在你的数据库服务器。

除非你的服务器端是被一些验证机制保护的，否则攻击者就可以通过简单猜测你的用户邮件地址（和密码）来读写用户的数据。

![情景1：第三方可以通过一封假邮件欺骗你的服务器](http://3.bp.blogspot.com/-lQZJjntOEGM/Vpfdl7rh32I/AAAAAAAACfE/-aDkDz0s_sA/s640/image00.png)

这不仅仅是极糟糕的用户体验，也使用户的数据被盗取或者恶意使用。当用户登录应用时，你可以通过从谷歌拉取token传送给你的服务器验证来阻止这样的情况。你的服务器将会验证这个谷歌给你的真实token，然后（通过验证后）给应用（基于你的用户设置，见下图）和用户传送真实正确的数据。在这一点上你的服务器可以得知是不是你的真实用户发起了数据请求，而不是一个恶意攻击者。这样之后才能响应需要的细节（请求）。

![情景2：第三方假的token将被拒绝](http://1.bp.blogspot.com/-QURiFFrHAC4/VpffFrjHD0I/AAAAAAAACfQ/1AzRGwcFYgU/s640/image01.png)

让我们看一下做这些（登录验证）的步骤：

**步骤一：** 在应用登录谷歌后将可以得到一个ID的token。这儿有一个非常简单的[示例](https://github.com/lmoroney/google-services/tree/master/android/signin)。要得到这个token，请求token的方法应该在创建GoogleSignInOptions对象后调用。

```

 GoogleSignInOptions gso = new GoogleSignInOptions.Builder(GoogleSignInOptions.DEFAULT_SIGN_IN)  

         .requestIdToken(getString(R.string.server_client_id))  

         .requestEmail()  

         .build();  

```



这就需要你从自己的服务器上拿到一个客户端的ID。关于这方面的具体细节可以看[这儿](https://developers.google.com/identity/sign-in/android/start?utm_campaign=android_discussion_googlesignin_011415&utm_source=anddev&utm_medium=blog)。

一旦你的应用上拿到这个token，你就可以通过HTTPS把它POST给你的服务器然后验证它（是否合法）。

(*) 这个ID token是一个JSON Web格式的token，遵循[RFC7519](https://tools.ietf.org/html/rfc7519)。这些都是开源的，双方之间都以行业标准确保安全。

**步骤2：** 你的服务器将收到来自客户端发送的token。你可以用[谷歌API客户端](https://developers.google.com/identity/sign-in/android/backend-auth?utm_campaign=android_discussion_googlesignin_011415&utm_source=anddev&utm_medium=blog#using-a-google-api-client-library)提供的方法去验证token是否合法，特别的一点是，验证结果是谷歌给出的，而接受对象是你的服务器。

你可以在你的服务器代码上使用[GoogleIdTokenVerifier](https://developers.google.com/api-client-library/java/google-api-java-client/reference/1.19.1/com/google/api/client/googleapis/auth/oauth2/GoogleIdTokenVerifier?utm_campaign=android_discussion_googlesignin_011415&utm_source=anddev&utm_medium=blog)这个类来验证这个token从而来拉取需要的用户身份数据。‘sub’这个字段（可以通过getSubject()得到）提供了一个稳定不变的字符串标识符可以用来验证用户身份，即便他们改了邮件地址，你可以将它存入到你的数据库。其他的ID token字段也是可以访问的，包括姓名，邮件地址和图片资源地址。这个小程序[案例](https://raw.githubusercontent.com/lmoroney/serverauth/master/LmauthtestServlet.java)使用了提供的库在谷歌App引擎上来测试。这些库允许你本地验证token而不用再次发起网络请求。

```

 GoogleIdTokenVerifier verifier = new GoogleIdTokenVerifier.Builder(transport, jsonFactory)  

      // Here is where the audience is set -- checking that it really is your server  

      // based on your Server’s Client ID  

      .setAudience(Arrays.asList(ENTER_YOUR_SERVER_CLIENT_ID_HERE))  

      // Here is where we verify that Google issued the token  

      .setIssuer("https://accounts.google.com").build();  

 GoogleIdToken idToken = verifier.verify(idTokenString);  

 if (idToken != null) {  

      Payload payload = idToken.getPayload();  

      String userId = payload.getSubject();   

      // You can also access the following properties of the payload in order  

      // for other attributes of the user. Note that these fields are only  

      // available if the user has granted the 'profile' and 'email' OAuth  

      // scopes when requested. Even when requested, some fields may be null.  

      // String email = payload.getEmail();  

      // boolean emailVerified = Boolean.valueOf(payload.getEmailVerified());  

      // String name = (String) payload.get("name");  

      // String pictureUrl = (String) payload.get("picture");  

      // String locale = (String) payload.get("locale");  

      // String familyName = (String) payload.get("family_name");  

      // String givenName = (String) payload.get("given_name");  

```

记住，如果你有一个应用的后端服务器是通过使用GoogleAuthUtil类来得到token的，你应该把他改到上面提到的最新的ID token验证库和机制。我们将会在以后的博客中给出最佳实践的建议。

这篇博客示例了怎么使用验证技术去确保用户得到真实的身份。在下一篇博客中，我们将会讲到使用谷歌登录API来授权等，这样用户就可以通过你的应用和后台服务来享受谷歌的服务，比如谷歌驾驶。

在这个[网站](https://developers.google.com/identity/)你可以了解到更多的谷歌认证技术。
