#术语、定义和缩略语

----------
<h2 id="cid_0">术语</h2>

 <table>
    <tr>
        <th>名称</th>
        <th>解释</th>
        <th>描述</th>
    </tr>
    <tr>
        <td>EDN</td>
        <td>ExMobi开发者中心</td>
        <td>开发者中心网站：https://www.exmobi.cn</td>
    </tr>
<tr>
        <td>基座</td>
        <td>烽火公司定期发布的ExMobi客户端版本</td>
        <td>烽火公司定期发布的ExMobi客户端版本，包括Android、iOS和WP8等不同平台的版本，其中没有应用插件，烽火公司同时发布了一套可以在PC电脑上运行的模拟器程序，即pc版本基座，方便开发和调试。</td>
    </tr>
<tr>
        <td>应用插件</td>
        <td>使用MBuilder新建的ExMobi工程文件，经过开发者开发后，能在基座中运行的代码集合</td>
        <td>使用MBuilder新建的ExMobi工程文件，经过开发者开发后，能在基座中运行的代码集合，一套应用插件代码可以在Android、iOS和Windows phone等平台上运行，真正实现跨平台。开发者在开发和调试阶段，可以通过MBuilder中提供的ExMobi模拟器模仿真机中的运行效果，避免了繁琐的打包、安装等操作。开发者在应用发布阶段，可选择本地生成应用演示安装包，也可以在EDN中，将应用插件与基座一起打包，最终生成应用包。应用插件还可以上传到ExMobi服务端，在服务端运行应用插件的服务端部分功能。</td>
    </tr>
<tr>
        <td>应用</td>
        <td>开发者在EDN中将ExMobi基座和应用插件打包生成的应用包文件</td>
        <td>发者在EDN中将ExMobi基座和应用插件打包生成的应用包文件，包文件是zip格式，其中的data子目录里面含有不同平台的应用程序文件，android平台是apk文件，iOS平台是ipa文件, WP8平台是xap文件，ExMobi服务端提供的应用管理功能可以支持应用的发布、下载、升级等功能，项目正式发布时，可以将应用包上传到服务端，用户访问http://ip:port/d地址即可下载应用，最终完成移动应用的发布。用户在手机上安装成功后，即可使用应用。</td>
    </tr>
<tr>
        <td>客户端</td>
        <td>泛指安装在移动设备上的应用程序，ExMobi应用也属于客户端</td>
        <td></td>
    </tr>
<tr>
        <td>服务端</td>
        <td>安装部署在linux或Windows系统中的ExMobi平台，该平台与客户端通信，并提供管理、运营、统计、数据集成、文档转换、推送等一系列管理和数据处理服务</td>
        <td></td>
    </tr>
<tr>
        <td>标签体</td>
        <td>开始标签和结束标签中间的内容，如&lt;div&gt;123&lt;div&gt;中的123和&lt;a&gt;连接&lt;/a&gt;中的文字都是标签体
        <td></td>
    </tr>
<tr>
        <td>BCS</td>
        <td>基础核心服务</td>
        <td>ExMobi服务端的核心服务组件，负责客户端对接、应用执行、对接业务系统，数据集成等工作，同时负责根据具体请求调用其他子服务</td>
    </tr>
<tr>
        <td>DCS</td>
        <td>文档转换服务</td>
        <td>提供将文档转换成图片、html的功能</td>
    </tr>
<tr>
        <td>PNS</td>
        <td>推送通知服务</td>
        <td>提供应用推送功能</td>
    </tr>
<tr>
        <td>EMP</td>
        <td>移动应用平台企业管理门户</td>
        <td>所有ExMobi服务端的组件都受EMP管理，同时支持应用插件管理、应用管理、设备鉴权、系统配置和统计等功能</td>
    </tr>
<tr>
        <td>WMS</td>
        <td>微信管理服务</td>
        <td>提供与微信平台对接，微信公众号发布，微信自定义菜单构建，自动回复配置，html5模块开发等功能</td>
    </tr>
<tr>
        <td>MPS</td>
        <td>管理端代理组件子系统</td>
        <td>代理管理端实际执行服务发布，运行池创建，运行池状态获取等功能。</td>
    </tr>
<tr>
        <td>工程模式</td>
        <td>ExMobi平台服务端正式部署在服务器中，正式交付使用的运行模式</td>
        <td></td>
    </tr>
<tr>
        <td>开发模式</td>
        <td>应用开发人员使用ExMobi平台服务端做应用开发及测试的运行模式</td>
        <td></td>
    </tr>
</table>

<h2 id="cid_1">缩略语</h2>

<table>
<tr><th>缩略语</th><th>英文全称</th><th>中文全称</th></tr>
<tr>
<td>MAXML</td>
<td>MobileApplication eXtensible Markup Language</td>
<td>移动应用扩展标识语言</td>
</tr>
<tr>
<td>UIXML</td>
<td>User InterfaceeXtensible Markup Language</td>
<td>用户界面可扩展标识语言</td>
</tr>
<tr>
<td>HTTP</td>
<td>HyperText Transfer Protocol</td>
<td>超文本传输协议</td>
</tr>
<tr>
<td>Aa</td>
<td>Agile Adaptation</td>
<td>敏捷适配</td>
</tr>
</table>