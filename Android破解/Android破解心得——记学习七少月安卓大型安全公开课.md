原文链接：http://www.cnblogs.com/kexing/archive/2018/03/30/8457859.html

## 第一课 

讲解了关于在安卓破解之中环境的配置及所需要用到的软件，重要的软件是`Androidkiller`，`安卓逆向助手`

## 第二课

讲解了java与smali的关系，从smail角度详细的分析了一个简单的HelloWorld的apk

## 第三课

讲解了二次破解

对于某些破解网站，从其网站下载之后在手机上打开之后，会有提示，这就需要我们安装其的app客户端才能实现破解，二次破解即可绕开此验证进入游戏

去安装盒子，去除toast提示，去除背景图片

安装盒子的那个apk是放在asset文件夹之中，当用户安装游戏（从该网站下载的破解版本），就会将该盒子的apk释放在sdcard上。

之后，进入游戏通过`context.getPackage.getPackageInfo`的方法（根据包名在获得的info中寻找，找到返回true，若没有找到则是返回false），检测当前用户手机是否安装有盒子.

如果没有安装，则是提示用户安装，用户不安装则是不给进入游戏界面，安装用到的就是之前释放出来，放在sdcard中的那个盒子apk

## 第四课

application类是比入口类要提前加载

asset资源文件夹常常用来放一些隐藏性的东西

使用了别的app来加密

jar使用安卓逆向助手的jd打开，如果打不开，可能只是使用jar调用，或者是被加密了

打开之后发现是一个apk的文件目录，可以将其扩展名改为apk进行反编译

可以发现，toast其实是在里面的，我们直接修改之后，进行回编，之后，如果是将我们回编的这个apk改为jar再次放进之前的apk之中，有极大可能会出错，为什么呢？因为可能在原始的apk中会有对这个jar的签名验证，所以，我们换种思路，将回编apk中的classdex放入之前的jar中，之后再放入原始的apk中，这样就行了

破解要抓住要点，采用修改较少的方法，这样不容易出错

## 去除横幅广告

直接在AndroidManiFest中删除其对应的activity ，搜索字符串删除即可 有米（youmi） 多游（duoyou）

删除activity只是简单的去除，实际上app中还是会显示横幅，需要做到彻底的删除，两种方法，一种是去上层去除对广告显示方法的调用，第二种则是清空该广告显示方法，记得需要返回（搜索横幅中的内容定位到该显示方法）

不过大多数的广告都是全屏广告，不能通过上面的方法来达成我们的目的，因为全屏广告其实是一张ImageView，是在activity文件之中动态生成的布局，涉及到布局动态变化，所以，我们得在smail代码中寻找关键的语句来到达成我们的目的

### 内购破解 三个点

监听类listener

关键判断函数 onBillingfinish payresult

具体的成功 取消 失败函数

分支过多，不适合改成跳转，可以直接修改值

move p1,p2 将p2的值赋值给p1