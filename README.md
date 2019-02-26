# KeepLive 进程保活实践
保活是什么，简单的说就是让你的App不会被轻易杀死，一直留存在用户的后台执行一些产品上相关的业务。
Android 系统为了保持系统运行流畅，在内存不足时，会将一些进程 kill ，以释放一部分内存。但是有些产品是有即时性的，在收到消息、推送等都是要立刻通知到用户。由此就出现了android的种种黑科技和奇葩操作来保障App的存活。
本文总结了当前保活圈里最常用的方法，其中也含有大厂用到过的方法。并且在本文探索的过程中梳理了关于保活内容的相关知识点（进程种类，AIDL，如何查看oom_adj等）无论是刚刚开始探索这个功能的小白，还是已经在保活圈里摸爬滚打的大佬都适合收藏。 文中若有不足之处，还请多多指教修改。

## 文章目录
* 编程语言  
    * 脚本语言  
        * Python  
        
1. 保活功能相关基础内容

 *  进程优先级介绍
  * 系统回收进程内存机制LMS简介
 1.3 查看oom_adj的方法
2. 进程保活的关键保活和复活

 2.1 保活分析
 2.2 在什么情况下进程会被杀死
 2.3 保活常用手段
 2.4 复活常用方法
3. 具体保活方案的实现过程

 3.1 单Service的提高进程的优先级
 3.2通过监听锁屏和开屏广播，使用“1”像素Activity提升优先级
 3.3通过JobScheduler的方式复活Service
 3.4通过在后台播放无声的音乐
 3.5 双进程守护方案
 3.6 双App相互拉活方案
4. 保活方案实现效果统计

 4.1 双进程守护方案
 4.2 监听锁屏广播打开1像素Activity
 4.3 后台播放无声的音乐
 4.4 使用JobScheduler唤醒Service
 4.5 混合使用的效果，并且在通知栏弹出通知
 
5.总结

链接地址：[Android进程保活演绎（从基础知识到深入探索）](https://www.jianshu.com/p/7bd16771c81e)


