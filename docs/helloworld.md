<h1>helloworld</h1>  

----------

## 开发环境搭建  

1.	从官网下载Mbuilder5 IDE，sprite客户端（apk和ipa）和代码同步小工具SpriteHttpServer.exe。  

2.	在手机上安装sprite.apk或者aprite.ipa，注意ios提供的是企业版，可以直接通过手机助手进行安装，安装后需要手动的在“设置-通用-描述文件与设备管理”对应用添加信任。  

3.	随便在某个磁盘下创建一个文件目录，然后在目录里面创建一个apps目录，然后再把SpriteHttpServer.exe同步小工具放在和apps同级的目录下。  

<img  src="image/hw_1.png" /> 

4.	要保证手机和自己的开发电脑在同一个wifi内，并且可以网通。  

5.	然后开启SpriteHttpServer.exe。

 
##  新建项目    

1.	在apps目录下创建一个名为app.json的文件（文件名固定写法），然后编写如下json内容：  

<img  src="image/hw_2.png" />   

homeJs:应用的入口js地址，res:前缀是基于apps目录开始；  

orientation:横竖屏设置，portrait:竖屏（默认）、landscape:横屏、device:支持横竖屏切换；  

syncip:设置同步小工具所在开发电脑的IP地址，一般情况就是自己电脑的ip地址。  

syncname：设置同步小工具服务器名称，随便定义。  

由于app.json这个文件不会被同步，所以暂时需要手动的拷贝到手机对应的目录里，通过手机助手找到对应目录spirte/apps:  

Ios手机对应目录：
<img  src="image/hw_5.png" />    

android手机对应目录：  

<img  src="image/hw_15.png" />  


2.	创建程序入口文件home.js  

该文件名和文件路径和app.json里面指向的保存一致即可，上图示例中home.js文件是直接放在apps根目录下。然后编写home.js里面的内容代码如下：  

```javascript
require.config({
        jsPaths: {
        },
        componentPaths:{
        },
        cssPaths:{
        }
});
var app = require("App");
var window = require("Window");
app.on("launch",function(e,jsonData){
    var type = jsonData.type;
     if(type =="normal"){
        //正常桌面启动
        var json = {};
        json.url = "res:myapp/index.uixml";
        window.open(json);
     }
     else if(type =="app"){
        //其他应用调用启动
     } 
     else if(type =="notification"){
        //推送消息启动
     } 
     else if(type =="localNotification"){
        //本地通知启动
     }
 });

```  

关于home.js里面的配置说明，我们后面会详细介绍，home.js作为程序入口，那么就需要指定一个应用程序的起始页面，示例代码里面指向了res:myapp/index.uixml。  

3.	根据指定的路径创建myapp文件目录，并且创建一个index.uixml文件。  

<img  src="image/hw_3.png" />  
<img  src="image/hw_4.png" />   

Index.uixml页面基本格式如下:  

```html
<page>
    <script>
        <![CDATA[

        ]] >
    </script>
    <style>

    </style>
    <ui>

    </ui>
</page>
```  
其中&lt;page&gt;是uixml页面格式的根节点，没有实际意义。&lt;script&gt;里面写js，&lt;style&gt;里面可以写css，&lt;ui&gt;里面就是页面布局了。  

##  页面布局   

下面开始页面布局，sprite平台中布局容器叫做box，大部分布局效果都用box完成。  

首先在<ui>标签里面放一个box，让box宽高都等于手机屏幕。  

<img  src="image/hw_6.png" /> 

然后在box里面用<text>控件写上文字，并调整下样式让其居中。  

<img  src="image/hw_7.png" /> 

这个时候，可以用手机查看效果，注意：手机端会在页面关闭和程序关闭的时候进行代码同步。如果没有看到效果，尝试多关闭几次页面。  

手机效果如下图：  

<img width="250"  src="image/hw_8.png" />  


##  实现一个动画  

下面我们实现一个动画，让文字从小变大并且选中起来。代码如下：  

```html

<page>
    <script>
        <![CDATA[
        var window = require("Window");
        var document = require("Document");
        var textBox  ; 
        //页面如果加载的时候有控件动画必须放在animator监听页面加载动画结束之后进行
        window.on("animator", function() {
            //文本区域
           textBox =  document.getElement("textBox"); 
            //启动动画
           startTextAnimation(); 
        });
        //文本区域动画
        function startTextAnimation(){
            //设置文本可见
           textBox.setStyle("visibility","visible");
           document.refresh();
            var jsonData = {};
            jsonData.fillAfter = 1;
            var animationSet = new Array();
            //缩放动画
            var scaleAni = {};
            scaleAni.type = "scale";
            scaleAni.duration = 1500;
            scaleAni.curve = "linear";
            scaleAni.scaleFromX = 0.1;
            scaleAni.scaleToX = 1;
            scaleAni.scaleFromY = 0.1;
            scaleAni.scaleToY = 1;
            animationSet.push(scaleAni);
            //旋转动画
            var rotateAni = {};
            rotateAni.type = "rotate";
            rotateAni.duration = 1500;
            rotateAni.curve = "linear";
            rotateAni.fromDegree = 0;
            rotateAni.toDegree = 360;
            animationSet.push(rotateAni);
            jsonData.animationSet = animationSet;
            //启动动画
            textBox.startAnimation(jsonData,function (){
                
            });
        }
        ]]>
    </script>
    <style>
        .rootBox {
            background-color: #0099cc;
            width: fill_screen;
            height: fill_screen;
            justify-content: center;
            align-items: center;
        }
        
        .text {
            color: #33b5e5;
            font-size: 45;
            text-align: center;
        }
        
        .textBox {
            visibility: hidden;
        }
    </style>
    <ui>
        <box class="rootBox">
            <box id="textBox" class="textBox">
                <text class="text">Sprite</text>
                <text class="text">移动开发平台</text>
            </box>
        </box>
    </ui>
</page>

```

效果如下：  

<img width="250"  src="image/hw_9.png" />  

接下来，我们在来做一个定时关闭页面的功能，在页面右上方放一个text用来显示倒计时。  

<img   src="image/hw_10.png" />    

然后给定样式，让其固定在页面右上方。  

<img   src="image/hw_11.png" />   

通过控件id获取到控件对象。  

<img   src="image/hw_12.png" />    

最后在动画结束的回调里面做一个定时器，注意用定时器需要在js导入var Time = require("Time");  

<img   src="image/hw_13.png" /> 

编写定时器代码：

<img   src="image/hw_14.png" />   



