# MukioPlayer的最大不足 #

是那个由as3手工写出的具有近千行的GUI代码文件:CommentListSender.as
而且,flash Component V2年代久远,难以考证.

# 解决方案:使用Flex构建UI #

得益于Gumbo组件架构,使用Flex构建UI已成为享受,不用再为添加一个新模式的弹幕发送界面而头疼了.

没有把Bili的新弹幕模式加入到net版本中,因为没有写出发送界面.

设计一个新的弹幕模式所需要的相关环节:
  * 格式的解析[发送]
  * 显示模块
  * 输入界面

# 设计正在进行中 #

最近才起步
  * 四种界面布局:normal,wideScreen,fullScreen,fullScreen(in Browser),各种尺寸下都可以自由伸缩(全屏的不可以)
  * JWPlayer v5.3
  * Flex SDK 4.1
  * 用户弹幕中的E3ScriptEngine