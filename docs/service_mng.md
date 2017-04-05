# 服务与管理端集成场景介绍 

----------

<h2 id="cid_0">应用访问服务授权与鉴权</h2>  

ExMobi-server提供了应用访问服务鉴权的流程，服务发布到ExMobi平台后，客户端提出服务的访问时需要做限制时，可以通过应用访问服务授权与鉴权功能实现。

开发应用访问服务鉴权流程序列图：  

![开发应用访问服务鉴权流程序列图](image/service_mng_101_1.jpg)  

服务处理鉴权逻辑示意图：  

![服务处理鉴权逻辑示意图](image/service_mng_101_2.png) 

<h3 id="cid_0_0">引入依赖库</h2>   

在服务工程的WEB-INF/lib目录下引入exmobi-access.jar和exmobi-mng.jar。  


<h3 id="cid_0_1">定义服务鉴权逻辑</h3>   

<h4 id="cid_0_1_0">配置filter实现</h4>    

配置CheckServiceTokenFilter，以下配置，定义了 http://ip:port/myservice/account/* 的地址都需要走CheckServiceTokenFilter执行，也就是匹配该地址的请求都要做应用访问服务鉴权。 

```xml
<filter>
	<filter-name>CheckServiceTokenFilter</filter-name>
	<filter-class>com.fiberhome.access.checkservicetoken.CheckServiceTokenFilter</filter-class>
</filter>
<filter-mapping>
	<filter-name>CheckServiceTokenFilter</filter-name>
	<url-pattern>/account/*</url-pattern>
</filter-mapping>

```

<h4 id="cid_0_1_1">自定义逻辑调用API实现</h4>    

exmobi-access.jar包中提供了CheckServiceToken类，其定义的checkServiceToken()方法即是满足自定义逻辑情况下也可以实现应用访问服务鉴权功能的，CheckServiceTokenFilter类实际也是调用了这个CheckServiceToken类的checkServiceToken()方法。因此，如果开发者不想使用平台提供默认的CheckServiceTokenFilter，也可以自己定义filter或SpringMVC的拦截器，调用CheckServiceToken类，可以实现相同的逻辑。  

<h3 id="cid_0_2">获取平台访问token</h3>   

如果是ExMobi客户端，可以直接调用应用访问服务鉴权API，向管理端 https://ip:port/api/getAccessToken 地址发起getAccessToken请求，以获取到访问token值。

如果是原生开发的应用，可以集成ExMobi发布的应用访问服务SDK，支持iOS/Android两个版本，向管理端 https://ip:port/api/getAccessToken 地址发起getAccessToken请求，以获取到访问token值。

获取访问token的接口的详细定义，请参照[ExMobi6服务接入指南](https://gitdocument.exmobi.cn/exmobi6server-accessguide/index.html)教程的“/api/getAccessToken应用获取访问服务token接口”章节。

<h3 id="cid_0_3">访问服务</h3>  

获取到访问token后，即可携带token访问服务，详细接口定义，请参照[ExMobi6服务接入指南](https://gitdocument.exmobi.cn/exmobi6server-accessguide/index.html)教程的“访问服务”章节。  

<h2 id="cid_1">服务参数配置</h2>  

章节[服务配置文件config.xml](https://gitdocument.exmobi.cn/exmobiserver-begin/service_package.html#cid_1)介绍了服务参数配置文件，同时章节[Exmobi-business.jar](https://gitdocument.exmobi.cn/exmobiserver-begin/service_api.html#cid_7)中提供了服务参数获取的API。那么在实际开发过程中如何配置和使用服务参数配置功能？  

首先在web工程中class目录下引入config.xml配置文件，同时	代码中调用获取参数API获取对应的参数并在页面中展示处理。  

config.xml配置信息如下：  

```xml
<?xml version="1.0" encoding="UTF-8"?>
<config>
	<group id="self" name="自定义参数配置">
		<paralist>
			<param>
				<paraKey>pathdomain</paraKey>
				<paraValue>192.168.160.125:8088</paraValue>
				<paraName>公司Path系统地址</paraName>
				<paraMemo>公司Path系统地址</paraMemo>
				<paraRule></paraRule>
			</param>
			<param>
				<paraKey>dcsserver</paraKey>
				<paraValue>http://192.168.160.167:8001/services/dcsService/</paraValue>
				<paraName>dcs引擎地址</paraName>
				<paraMemo>dcs引擎地址</paraMemo>
				<paraRule></paraRule>
			</param>
		</paralist>
	</group>
</config>

```

代码中调用获取服务参数api——ParamConfig类获取参数  

![ParamConfig类获取参数](image/service_mng_102_1.png)  

其次通过通过管理界面上传并发布服务，

![通过管理界面上传并发布服务](image/service_mng_102_2.png)  

通过管理界面【参数配置】可以对参数进行管理配置，  

![管理界面配置参数](image/service_mng_102_3.png)   

总结，服务可以通过配置文件配置本地参数，同时可以通过管理界面对本地参数配置进行管理及新增自定义参数。  


<h2 id="cid_2">服务页面授信与平台集成</h2>  

服务页面授信与平台集成的目的是为了能够在平台管理中方便快捷的访问服务中的相关界面，进行相应的功能查看和操作。  

第一步：上传服务，并将服务下发到相应的容器中。直接访问服务的管理主页提示登录，如下图  

![上传服务](image/service_mng_103_1.png)  

第二步：通过平台界面配置服务授信页面访问地址，希望通过授信在平台界面中免登录直接进行访问

![配置服务授信](image/service_mng_103_2.png)  

![配置服务授信](image/service_mng_103_3.png)  

![配置服务授信](image/service_mng_103_4.png)  

第三步：验证能否通过配置的授信页面进行访问进入服务管理界面  

![验证服务授信](image/service_mng_103_5.png)  

![验证服务授信](image/service_mng_103_6.png)  

总结，通过上面的几个步骤发现同样是请求服务管理主页，通过页面授信平台就可以访问服务管理主页。  

通过抓包发现直接请求和平台管理界面请求地址是有区别的。平台管理界面请求在原有的基础上带上了参数
token=eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJFeE1vYmktRU1QLVNTTy1Ub2tlbiJ9.tZjDiUeRO85U8WWCExsNgBhzmzIdE6h1Nlulo2HRhuo。服务通过校验token是否有效来确认当前请求是否可信。以下为服务部分示例代码在登录校验过滤器中判断是否可信，开发该功能需要引入ExMobi-access.jar及其依赖jar，关键部分示例如下：  

```java
import java.io.IOException;
import java.io.OutputStream;
import java.nio.charset.Charset;
import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import org.apache.log4j.Logger;
import com.fiberhome.access.trustwebchecker.TrustWebChecker;

/**
 * 服务页面访问授信使用示例
 * 
 * @author Administrator
 *
 */
public class LoginFilter implements Filter
{

/**
 * 日志信息
 */
private static Logger log = Logger.getLogger(LoginFilter.class);

@Override
public void init(FilterConfig arg0) throws ServletException
{
}

@Override
public void doFilter(ServletRequest arg0, ServletResponse arg1, FilterChain arg2)
	throws IOException, ServletException
{
	HttpServletRequest reqeust = (HttpServletRequest) arg0;
	HttpServletResponse response = (HttpServletResponse) arg1;
	String path = reqeust.getServletPath();
	if (path.startsWith("/login.mvc") || path.startsWith("/logincheck.mvc"))
	{// 登录请求及登录校验url放行
		arg2.doFilter(arg0, arg1);
		return;
	}

	// 判断是否登录成功
	String islogin = (String) reqeust.getSession().getAttribute("login");
	if ("true".equals(islogin))
	{
		arg2.doFilter(arg0, arg1);
		return;
	}

	/****** 授信逻辑判断开始 ******/
	String checkresult = (String) reqeust.getSession().getAttribute("checkresult");
	if ("1".equals(checkresult))
	{// 判断当前会话是否已经授信过
		arg2.doFilter(arg0, arg1);
		return;
	}
	String token = reqeust.getParameter("token");
	if (token != null)
	{// 发现请求中带有token，调用对应的API进行判断授信访问请求是否可信
		TrustWebChecker trustWebChecker = new TrustWebChecker();
		if (1 == trustWebChecker.check(token))
		{// 校验通过 可信放行，并将当前校验结果放入到当前会话中，后续请求均默认可信
			reqeust.getSession().setAttribute("checkresult", "1");
			arg2.doFilter(arg0, arg1);
			return;
		}
		else
		{// 校验不通过 不可信  响应提示消息
			log.error("服务页面访问授信校验未通过 !");
			response.setCharacterEncoding("UTF-8");
			response.setContentType("application/json");
			OutputStream out = response.getOutputStream();
			String rspinfo = "{\"resultCode\":" + 0 + ",\"resultMessage\":\"服务页面访问授信校验未通过!\"  }";
			out.write(rspinfo.getBytes(Charset.forName("UTF-8")));
			out.flush();
			out.close();
			return;
		}
	}
	/****** 授信逻辑判断结束 ******/

	// 跳转到登录页面
	reqeust.getRequestDispatcher("login.mvc").forward(arg0, arg1);
}

@Override
public void destroy()
{

}

}

```

<h2 id="cid_3">设备信息采集</h2>  

服务可以通过ExMobi-access.jar中对应的设备信息采集API进行设备信息采集并上报至平台管理端，如何实现设备的信息采集，详细看如下示例。  

示例一：通过平台提供的过滤器com.fiberhome.access.registerdevice.RegisterDeviceFilter在服务的web.xml中进行配置，针对某个地址进行过滤采集相应的设备信息并自行上报至平台管理端。  

```xml
<!-- 引入设备采集能力 -->
<filter>
	<filter-name>RegisterDeviceFilter</filter-name>
	<filter-class>com.fiberhome.access.registerdevice.RegisterDeviceFilter</filter-class>
</filter>
<filter-mapping>
	<filter-name>RegisterDeviceFilter</filter-name>
	<url-pattern>/login</url-pattern>
</filter-mapping>
```  

示例二：开发者也可以根据具体的业务场景进行设备信息上报，自行上报的代码片段如下：  

```java
// 构建待上报的设备信息
List<DeviceInfo> deviceInfoList = new ArrayList<DeviceInfo>();
DeviceInfo info = new DeviceInfo();
info.setMsisdn("msisdn");
info.setUsername("name");
info.setEsn("esn");
info.setPin("pin");
info.setImsi("imsi");
info.setOs("os");
info.setOsVersion("osversion");
info.setPlatformId("platformid");
info.setClientVersion("clientversion");
info.setClientId("appid");
deviceInfoList.add(info);

// 上报设备信息
RegisterDevice registerDevice = new RegisterDevice();
registerDevice.registerDeviceInfo(deviceInfoList);

```