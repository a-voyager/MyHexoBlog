title: 深入理解Activity(一)
categories: Android
tags: [Android, 深入理解Activity]
---
Hello!大家最近还好吗!现在是2015年11月14日凌晨4点，今天的博客写完了，主要讲的是学习慕课网的Activity专题后的总结，帮助复习一下安卓的Activity，“深入理解Activity”是一个系列，后面还会更新，由浅到深，希望能带给大家一点帮助，也同时记录自己的学习历程。不多说，开始！
# Activity的生命周期
## 对于单个Activity
* 可见状态
```java
onCreate()->onStart()->onResume()
```
* 不可见状态
```java
onPause()->onStop()
onDestroy()
```
* 销毁状态
```java
onDestroy()
```
## 对于多个Activity
不多讲，只注意一点:
每次打开新的Activity总会调用当前的onPause()方法
## 交互设计思想
1. 为什么需要onPause()？是否多此一举？
	用于暂停状态信息，比如暂停音乐视频播放
2. 要注意onStop()方法是在最后执行的，这又是为什么呢
	这是为了防止在创建第二个Activity时造成当前Activity消失黑屏，造成视觉体验不够良好(onStop执行后才处于不可见状态)
## 横竖屏切换
* Bundle对象
	用于保存横竖切换前的状态信息，通过bundle.put()方法
# Activity的两种启动方式
* 显式启动
	直接启动方式就不用说了，直接Intent启动即可，还是简单举个例子吧，举个不常用的Component方式
	```java
	ComponentName cn = new ComponentName(this, other.class);
	intent.setComponent(cn);
	```
* 隐式启动
	什么是隐式启动，其实就是启动其他应用程序的Activity，具体怎么做呢，看代码
1. 首先在被启动Activity中定义inten-filter
	```xml
	<intent-filter>
		<action android:name="www.xxx.com"/>
		<category android:name="......DEFAULT"/>
	</intent-filter>
	```
2. intent中setAction("...")即可


>### 拓展: 启动系统的Activity
```java
//启动浏览器
intent.setAction(Intent.ACTION_VIEW);
Uri url = Uri.parse("http://www.baidu.com");
intent.setData(url);

//启动系统相册
intent.setAction(Intent.ACTION_GET_CONTENT);
intent.setType("image/*");	//重写onActivityForResult()

//发送短信
intent.setAction(Intent.ACTION_SEND);
intent.setType("text/plain");
intent.putExtra(Intent.EXTRA_TEXT, "your sms text");

//打开电话拨号
intent.setAction(Intent.ACTION_VIEW);
Uri url = Uri.parse("12345678901");
intent.setData(url);
```