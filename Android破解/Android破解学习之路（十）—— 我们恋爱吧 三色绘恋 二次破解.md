原文链接：http://www.cnblogs.com/kexing/archive/2018/10/08/9756260.html
## 前言
好久没有写破解教程了（我不会告诉你我太懒了），找到一款恋爱游戏，像我这样的宅男只能玩玩恋爱游戏感觉一下恋爱的心动了。。

这款游戏免费试玩，但是后续章节得花6元钱购买，我怎么会有钱呢，而且身在吾爱的大家庭里，不破解一波怎么对得起我破解渣渣的身份呢！

哟，还是支付宝购买的，直接9000大法，但是破解的时候没有成功，可能是支付的关键代码在so文件中把，自己还不是很熟悉IDA破解so，所以就撤了，网上找到了别人的破解版本，直接就是解锁版本的。

但是，这破解版的有点奇葩，第一次打开可以正常进入，第二次打开就卡在了它的logo上（破解者加了一个界面显示logo，就是类似XX侠），把它软件下载之后，再次点击就可以正常进入游戏了，支付宝内购破解我破不了，二次破解我总行吧，**我的目的就是不用安装APP也能进入游戏**

## 破解思路

1. 既然第一次可以正常进入，第二次就无法进入，肯定是第二次进入的时候做了个验证

2. 破解者加的那个logo界面，应该是有跳转到正常游戏界面的代码，我们直接在logo界面执行跳转代码，跳转到游戏界面

3. 打开游戏的时候直接跳过logo界面，进入游戏主界面

## 破解开始

### 思路1

首先，直接丢进Androidkiller中反编译，这款游戏没有加壳，好说，我们由工程信息的入口进到入口界面，展开方法，可以看到许多方法，由于我们猜想是第二次进入的时候做了验证，那么我们就查找一下方法最末尾为Z（代表着此方法返回的是一个Boolean值），**可以看到图中红色方框，末尾为Z，名字也是确定了我们的思路没有错，判断是否第一次进入**

![](https://img2018.cnblogs.com/blog/1210268/201810/1210268-20181008183156047-1642278610.png)

破解很简单，我们只需要让此方法直接返回一个true的值即可解决

![](https://img2018.cnblogs.com/blog/1210268/201810/1210268-20181008183327406-1534453807.png)

**测试是通过的，这里就不放图了**

### 思路2

第一种的方法尽管成功了，但是觉得不太完美，我们看一下能不能直接跳转到游戏的主界面，搜索intent（android中跳转界面都是需要这个intent来完成），没有找到结果，找到的几个都不是跳转到主界面的代码（这游戏的主界面就是MainActivity）

**思路2失败**

### 思路3

思路2失败了，我们还有思路3，首先介绍一下，android的APP，主界面是在AndroidManifest.xml这个文件中定义的

我们直接搜索入口类`VqsSdkActivity`,搜索中的第一个正是我们需要的

![](https://img2018.cnblogs.com/blog/1210268/201810/1210268-20181008183947356-2061532897.png)

点进入就可以看到，定义游戏的启动界面的关键代码，红色框中

![](https://img2018.cnblogs.com/blog/1210268/201810/1210268-20181008184227128-1842557591.png)

我们把这行代码剪切到MainActivity那边去（我们直接搜索MainActivity就可以定位到AndroidManifest中的具体位置）

![](https://img2018.cnblogs.com/blog/1210268/201810/1210268-20181008184506044-285183206.png)

嗯，**测试通过**

再加些东西吧，加个弹窗，名字也改一下吧，大功告成！！

## 测试截图

![](https://img2018.cnblogs.com/blog/1210268/201810/1210268-20181008190243066-722810495.png)

![](https://img2018.cnblogs.com/blog/1210268/201810/1210268-20181008190305048-1472327702.png)

![](https://img2018.cnblogs.com/blog/1210268/201810/1210268-20181008190320039-176199715.png)


## 下载链接
原版破解版： 链接: https://pan.baidu.com/s/1uvjRCkf2hPdI8vI467Vh5g 提取码: p718

二次破解版本： 链接: https://pan.baidu.com/s/128RH5ij3LRjsZPoG3vTTgQ 提取码: vbmv