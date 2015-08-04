# 脚本引擎 #

脚本引擎来自[SparkProject](http://www.libspark.org/wiki/WikiStart/en),为一日本开源组织

脚本引擎支持ECMAScript3.0语法的一个子集

包括:

  * 变量
  * 数组
  * 对象和属性
  * if
  * for,while
  * break,continue
  * with

未实现的举其几例:

  * try/catch/finally
  * for.. in
  * new操作

以上是脚本原作者说明.

我在测试时发现:递归计算结果通常是 **不正确的** ,一般流程的程序大部分时间是正确的.

测试结果:该脚本引擎能满足弹幕脚本的功能
# 脚本说明 #
**不要忘记在语句结束后写分号**<font size='30'>;</font> **## 使用后绑定的契约 ##
> ╱/( ◕‿‿◕ )\╲
  * 在发布脚本之前先在本机上测试.
  * 不写干扰别人正常欣赏弹幕视频的脚本.
## 作用域 ##
变量寄存在全局范围,不要跨弹幕调用函数,局部函数定义只在本弹幕有效.一旦接受了这样的设定还是挺可爱的./(oωo)\**

## 全局变量 ##
### Math ###
Math对象,JavaScript中的Math对象
## 全局方法 ##
### p(text),print(text) ###
在输出窗口打印

例子
```
p('Hello World!');
//将输出
//Hello World!
```
# 弹幕播放器API(暂定) #

## Player ##

Player包括了视频播放器的各种操作
#### Player.play() ####
播放
#### Player.pause() ####
暂停
#### Player.seek(time) ####

参数:time:Number

跳转,time为跳转时间,单位为秒
#### Player.time ####
当前视频的时间,单位为秒

## Display,D ##
包括了舞台弹幕的操作
### 方法 ###
### 弹幕预览功能 ###
一个脚本弹幕相当于多个非脚本弹幕,并且包括一些逻辑判断和计算

#### Displaycmt(text,color=0xffffff,size='middle',mode='toLeft') ####
普通的三式弹幕预览

参数: text 文本

参数: color 颜色

参数: size 字号,small,middle,big

参数: mode 模式,toLeft,top,bottom
#### Display.bili(text,x=0,y=0,color=0xffffff,size=25,rZ=0,rY=0,duration=4.5,inAlpha=1,outAlpha=1) ####
普通版本的Bili弹幕预览

参数: text 文本

参数: x x点坐标

参数: y y点坐标

参数: color 颜色

参数: size 字号

参数: rZ 旋转值

参数: rY 翻转值

参数: duration 总时间

参数: inAlpha 起始透明

参数: outAlpha 结束透明
#### Display.bili2(text,x=0,y=0,color=0xffffff,size=25,rZ=0,rY=0,duration=4.5,inAlpha=1,outAlpha=1,toX=0,toY=0,mDuration=500,delay=0) ####
增强版本的Bili弹幕模式预览

参数: text 文本

参数: x x点坐标

参数: y y点坐标

参数: color 颜色

参数: size 字号

参数: rZ 旋转值

参数: rY 翻转值

参数: duration 总时间

参数: inAlpha 起始透明

参数: outAlpha 结束透明

参数: toX 目标x点坐标

参数: toY 目标y点坐标

参数: mDuration 移动持续时间,毫秒

参数: delay 移动前停留,毫秒
#### Display.zoome(...) ####
未完成
### 字幕生成功能 ###
生成一个完全自定义的弹幕文本对象,操作见 ScriptText
#### Display.createText(name,text) ####
创建一个名称为name的文本对象,内容为text
#### Display.text(name) ####
取得舞台上名称为name的文本对象的引用
#### Display.removeText(name) ####
销毁舞台上名称为name的文本对象
#### Display.clean() ####
销毁舞台上所有文本对象,并把名称库清空
### 属性 ###
#### Display.width ####
弹幕舞台宽度
#### Display.height ####
弹幕舞台高度
## ScriptText ##
为脚本生成的字幕对象,对该对象的属性修改以及方法的调用为自定义弹幕的基本操作

### 属性 ###
#### text ####
#### x ####
#### y ####
#### alpha ####
#### color ####
#### size ####
### 方法 ###
#### show() ####
显示文本.创建后文本需要主动显示.
#### hide() ####
隐藏文本.隐藏后还可以调用show()方法,但是Display.removeText()或者Display.clean()执行后,文本对象已经销毁,无法再调用文本的任何方法.
#### moveTo(x,y,duration=1,complete=null) ####
文本移动函数,使用二次方缓动

参数:x,y 目标坐标

参数:duration 移动花费时间,秒,默认值1秒

参数:complete 动作完成后执行的函数,默认为null

例子:
```
var t = Display.createText('t','Text');
t.show();
t.moveTo(200,200,1,function(){t.moveTo(200,400);});
//创建弹幕
//弹幕在(0,0)显示
//弹幕在1秒内移动到200,200,接着在1秒内移动到200,400
```

## Toolkit,T ##
为脚本弹幕的常用工具集合
### 方法 ###
#### T.hue(value) ####
将0-360的值映射到色相环上,其中,
  * 0 -> 0x0000ff
  * 120 -> 0xff0000
  * 240 -> 0x00ff00
<font color='#0000ff'>■</font><font color='#8f00ef'>■</font><font color='#9f00df'>■</font><font color='#af00cf'>■</font><font color='#bf00bf'>■</font><font color='#cf00af'>■</font><font color='#df009f'>■</font><font color='#ef008f'>■</font><font color='#ff0000'>■</font><font color='#ef8f00'>■</font><font color='#df9f00'>■</font><font color='#cfaf00'>■</font><font color='#bfbf00'>■</font><font color='#afcf00'>■</font><font color='#9fdf00'>■</font><font color='#8fef00'>■</font><font color='#00ff00'>■</font><font color='#00ef8f'>■</font><font color='#00df9f'>■</font><font color='#00cfaf'>■</font><font color='#00bfbf'>■</font><font color='#00afcf'>■</font><font color='#009fdf'>■</font><font color='#008fef'>■</font>

#### T.delay(time=1000)(foo) ####
延迟执行函数

参数:time,延迟时间,毫秒,默认值1000,允许范围0-15\*1000

参数:foo,执行函数,在延迟结束后执行,无参数

例子:
```
T.delay(1000)(function(){p(1);});
T.delay(500)(function(){p(2);});
//将输出
//2
//1
```
#### T.repeat(n=1)(foo) ####
重复执行函数.存在的理由?比for好用一点??

参数:n,重复次数,默认值1

参数:foo,重复执行的函数,有两个参数,第一个是0到n-1的计数,第二个是n本身

例子:
```
T.repeat(5)(function(i,n){p(i+','+n +' ');});
//将输出
//0,5 
//1,5 
//2,5 
//3,5 
//4,5 
```