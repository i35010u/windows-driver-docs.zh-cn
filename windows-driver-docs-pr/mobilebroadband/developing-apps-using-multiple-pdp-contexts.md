---
title: 使用多个 PDP 上下文开发应用
description: 使用多个 PDP 上下文开发应用
ms.assetid: 6a977a69-397d-4922-890d-1810dd54dff4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19e2b03402ca37669dfa61ab392d1cb59ee28dfb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381502"
---
# <a name="developing-apps-using-multiple-pdp-contexts"></a>使用多个 PDP 上下文开发应用


数据包数据协议 (PDP) 上下文提供了哪些设备和移动网络可以交换 IP 数据包的数据包数据连接。 根据 3GPP 标准的设备可以有多个 PDP 上下文激活一次。 在 Windows 8.1 和 Windows 10 中，多个 PDP 上下文支持，并能使应用程序在 Windows 8 中支持的 PDP 上下文通过特殊 PDP 上下文到移动网络，以及 internet 进行通信。 可以使用此功能在 Windows 上创建独特的体验和创新的服务。 您还可以与应用程序开发人员开发高质量 VOIP 和视频流为其客户体验的合作伙伴。

下面是演示如何将多个 PDP 上下文的工作方式在 Windows 8.1 和 Windows 10 的图形：

![图 1](images/mb-pdp-fig1.jpg)

使用本主题中的下列部分来了解有关多个 PDP 上下文的详细信息：

-   [关键方案](#key-scenarios)

-   [移动宽带应用程序](#mobile-broadband-apps)

-   [移动宽带设备](#mobile-broadband-devices)

## <a name="key-scenarios"></a>关键方案


多个 PDP 上下文可用于启用高级版服务。

-   **不同的计费**– 你可以通过使用多个 PDP 上下文通过改变数据或计费限制。 例如，Contoso 是为其客户开发的数据的备份应用程序移动运营商。 作为移动运营商，Contoso 可以创建多个 PDP 上下文，并且可以让高级订阅者免费使用应用程序。 所有其他订阅服务器将单独收费，若要使用它。

-   **富通信服务**– 由 GSM 关联，以提供丰富的通信服务，例如增强的通讯簿，创建一个全局计划增强消息传递和丰富调用。 富通信服务在移动操作员和产品/服务的新方法使用现有的资产和功能来提供高质量和创新的通信服务之间提供互操作性。

-   **赞助连接**– 这样，而无需它将针对他们每月的数据使用特定类型的内容的用户。 内容提供程序的排列方式向移动运营商补偿支付它们直接执行了收入共享大或某些其他业务合作。

-   **个人热点**– 连接用作个人热点时，一些移动运营商实施不同的费率。 可以使用多个 PDP 上下文来区分这两个。

## <a name="mobile-broadband-apps"></a>移动宽带应用程序


UWP 移动宽带应用程序可以充分利用多个 PDP 上下文，若要激活的特殊 PDP 上下文和指定用于路由数据流量的规则。 这些应用可以创建特定目标或所有数据流量的规则。

当移动宽带应用需要与网络交换数据时，它会检查可用并已连接网络。 如果移动宽带应用程序具有这些网络的任何特殊的规则，它使用连接管理器 API 来打开特殊的 PDP 上下文。 如果此连接成功，PDP 上下文提供此连接的路由规则，并使用网络 Api 将数据传输。 如果它收到的移动宽带应用应重复这[ **NetworkStatusChanged** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.NetworkInformation#Windows_Networking_Connectivity_NetworkInformation_NetworkStatusChanged)事件以查看是否已更改任何连接，是否需要打开新连接的 PDP 上下文。

![图 2](images/mb-pdp-fig2.jpg)

### <a name="span-idnetworkingapisspanspan-idnetworkingapisspanspan-idnetworkingapisspannetworking-apis"></a><span id="Networking_APIs"></span><span id="networking_apis"></span><span id="NETWORKING_APIS"></span>网络 Api

用于通过使用特殊的 PDP 上下文发送数据，Microsoft Store 应用程序必须使用不同的逻辑基于网络 Api，它使用将数据传输。

### <a name="span-idhttp-basedapisspanspan-idhttp-basedapisspanspan-idhttp-basedapisspanhttp-based-apis"></a><span id="HTTP-based_APIs"></span><span id="http-based_apis"></span><span id="HTTP-BASED_APIS"></span>基于 HTTP 的 Api

基于 HTTP 的 Api，如[ **XMLHTTPRequest**](https://docs.microsoft.com/previous-versions/windows/apps/br229787(v=win.10))， [IXHR2](https://docs.microsoft.com/previous-versions/windows/desktop/ixhr2/ixmlhttprequest2-portal)， [ **Windows.Web.Syndication**](https://docs.microsoft.com/uwp/api/Windows.Web.Syndication)，和[ **Windows.Web.AtomPub**](https://docs.microsoft.com/uwp/api/Windows.Web.AtomPub)，和 Api 基于 Windows HTTP 协议，如 JQuery 和[ **Windows.Web.Http**](https://docs.microsoft.com/uwp/api/Windows.Web.Http)，没有将绑定到特定的接口的功能。 这些 Api，为 Windows 处理通过在策略路由到特殊的 PDP 上下文的数据。 一旦激活特殊 PDP 上下文，应用程序可以指定基于目标和特殊 PDP 上下文的路由规则。 目标可以是域名或 IP 地址，例如 video.fabrikam.com，。 contoso.com 或 123.23.34.333。 指定后的路由规则，如果应用使用的任何更高版本的 HTTP Api 来传输数据，Windows 将数据发送到根据路由规则的特殊 PDP 上下文。 将数据传输完成后应用程序，它应断开连接的特殊 PDP 上下文，并删除路由策略。

**请注意**  
[**后台传输 Api** ](https://docs.microsoft.com/uwp/api/Windows.Networking.BackgroundTransfer)并[HTTP 客户端 (C#) Api](https://docs.microsoft.com/previous-versions/visualstudio/hh193681(v=vs.118))不能使用路由策略。

 

![图 3](images/mb-pdp-fig4.jpg)

### <a name="span-idsocket-basedapisspanspan-idsocket-basedapisspanspan-idsocket-basedapisspansocket-based-apis"></a><span id="Socket-based_APIs"></span><span id="socket-based_apis"></span><span id="SOCKET-BASED_APIS"></span>基于套接字的 Api

中提供的基于套接字的 Api [ **Windows.Networking.Sockets** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Sockets)命名空间，如 TCP、 UDP 和流套接字，提供一种机制将绑定到特定的接口。 当应用使用套接字 Api 时，它应绑定到特定路由数据传输到特殊的 PDP 上下文的接口。 一旦激活特殊 PDP 上下文，则[ **AcquireConnectionAsync** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.ConnectivityManager#Windows_Networking_Connectivity_ConnectivityManager_AcquireConnectionAsync_Windows_Networking_Connectivity_CellularApnContext_) API 提供了向应用程序的接口信息。 它可以使用此信息对某个特定界面绑定和启动的数据传输。

![图 4](images/mb-pdp-fig3.jpg)

### <a name="span-idmultiplepdpcontentapiinfospanspan-idmultiplepdpcontentapiinfospanspan-idmultiplepdpcontentapiinfospanmultiple-pdp-content-api-info"></a><span id="Multiple_PDP_content_API_info"></span><span id="multiple_pdp_content_api_info"></span><span id="MULTIPLE_PDP_CONTENT_API_INFO"></span>多个 PDP 内容 API 信息

Windows 8.1 和 Windows 10 添加了以下 Api 以支持多个 PDP 上下文：

-   [**CellularApnContext** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.CellularApnContext)此类包含用于在网络上指定的访问点的属性。 **CellularApnContext**对象传递与[ **AcquireConnectionAsync** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.ConnectivityManager#Windows_Networking_Connectivity_ConnectivityManager_AcquireConnectionAsync_Windows_Networking_Connectivity_CellularApnContext_)调用来建立与特定的访问点的连接。

-   [**ConnectivityManager::AcquireConnectionAsync** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.ConnectivityManager#Windows_Networking_Connectivity_ConnectivityManager_AcquireConnectionAsync_Windows_Networking_Connectivity_CellularApnContext_)此 API 将激活新的连接指定的访问点名称 (APN) 或 PDP 上下文。 此异步方法，用于请求对某特定的 APN 或 PDP 上下文的相应配置信息的连接的应用。 特殊 APN 激活后，它显示为 Windows 和应用的新虚拟接口。

-   [**ConnectivityManager::AddHttpRoutePolicy** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.ConnectivityManager#Windows_Networking_Connectivity_ConnectivityManager_AddHttpRoutePolicy_Windows_Networking_Connectivity_RoutePolicy_)此方法将添加一个策略用于通过 HTTP 堆栈流量进行路由数据的特殊 PDP 上下文。 应用程序可以指定基于目标，如域名和 IP 地址和特殊 PDP 上下文配置文件的策略。 Windows HTTP 堆栈的数据路由到特殊的 PDP 上下文，一旦创建策略的应用使用的策略。

-   [**ConnectivityManager::RemoveHttpRoutePolicy** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.ConnectivityManager#Windows_Networking_Connectivity_ConnectivityManager_RemoveHttpRoutePolicy_Windows_Networking_Connectivity_RoutePolicy_)此方法将删除以前添加的 HTTP 路由策略。

下面的代码演示如何使用这些 Api 的基于 HTTP 的数据传输：

``` syntax
var connectivity = Windows.Networking.Connectivity;
var currentRoutePolicy = null;
var currentConnectionSession = null;

//  Create PDP context/APN data 
var apnContext                      =   new connectivity.CellularApnContext();
apnContext.accessName               =   "myAPN.com";
apnContext.userName                 =   "APNusername"
apnContext.password                 =   "APNPassword";
apnContext.isCompressionEnabled     =   false;
apnContext.authenticationType       =   connectivity.CellularApnAuthenticationType.none;

//  Request a connection to Windows
connectivity.ConnectivityManager.acquireConnectionAsync(apnContext).done(onConnectionSucceeded, onConnectionFailed);


//  On successful Activation of APN, Windows returns a ConnectionSession object that encapsulates the new connection profile

function onConnectionSucceeded(result
{
    // keep the connectionSession in scope
    currentConnectionSession= result;

    //  create a route policy for the new connection
    currentRoutePolicy = new connectivity.routePolicy(currentConnectionSession.ConnectionProfile, new hostName("video.mydomain.com"),Windows.Networking.DomainNameType.suffix);

    //  indicate the new route policy to the Http stack
    connectivity.connectivityManager.addHttpRoutePolicy(currentRoutePolicy);

    // Backend data interaction with appropriate HTTP APIs (IXHR, Open IFrame etc.)


    // After completing the data transfer remove the Route Policy
    connectivity.connectivityManager.removeHttpRoutePolicy(currentRoutePolicy);
    currentRoutePolicy = null;

    // Disconnect the PDP Context to free up resources
    currentConnectionSession.close();
}
```

下面的代码演示如何使用这些 Api 的基于套接字的数据传输：

``` syntax
// Connect to Special PDP Context
var connectivity = Windows.Networking.Connectivity;
var currentRoutePolicy = null;
var currentConnectionSession = null;

// Create PDP Context/APN Data 
var apnContext = new connectivity.CellularApnContext();

// Create PDP context/APN data 
var apnContext = new connectivity.CellularApnContext();
apnContext.accessName = "myAPN.com";
apnContext.userName = "APNusername"
apnContext.password = "APNPassword";
apnContext.isCompressionEnabled = false;
apnContext.authenticationType = connectivity.CellularApnAuthenticationType.none;

// Request the connection to Windows
connectivity.ConnectivityManager.acquireConnectionAsync(apnContext).done(onConnectionSucceeded, onConnectionFailed);

// On successful activation of an APN, Windows returns a ConnectionSession object that encapsulates the new connection profile
                function onConnectionSucceeded(result) {

// keep the connectionSession in scope
currentConnectionSession = result;

var socket = new Windows.Networking.Sockets.StreamSocket();
var hostName = new Windows.Networking.HostName("www.contoso.com");
var portNumber = "1234";

// Bind the socket to new Special PDP Context Connection
socket.connectAsync(hostName, portNumber, SocketProtectionLevel.PlainSocket, currentConnectionSession.connectionProfile.networkAdapter).done(onSocketConnectionSucceeded, onSocketConnectionFailed);

function onSocketConnectionSucceeded(result)
{
    // Start transferring data using socket APIs

}

// Closing the sockets
socket.close();

// Disconnect the PDP Context to free up resources
currentConnectionSession.close();
```

您的应用程序必须处理[ **NetworkStatusChanged** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.NetworkInformation#Windows_Networking_Connectivity_NetworkInformation_NetworkStatusChanged)事件后才能处理任何网络转换对特殊 PDP 上下文连接。

### <a name="span-idscenariopremiummobilebroadbandappprovidesfreedataaccessusingspecialapnspanspan-idscenariopremiummobilebroadbandappprovidesfreedataaccessusingspecialapnspanspan-idscenariopremiummobilebroadbandappprovidesfreedataaccessusingspecialapnspanscenario-premium-mobile-broadband-app-provides-free-data-access-using-special-apn"></a><span id="Scenario__Premium_mobile_broadband_app_provides_free_data_access_using_special_APN"></span><span id="scenario__premium_mobile_broadband_app_provides_free_data_access_using_special_apn"></span><span id="SCENARIO__PREMIUM_MOBILE_BROADBAND_APP_PROVIDES_FREE_DATA_ACCESS_USING_SPECIAL_APN"></span>方案：高级移动宽带应用程序提供了使用特殊的 APN 的免费数据访问

在此方案中，移动宽带应用提供了使用特殊的 PDP 上下文的免费数据访问。 如果它是免费或它使用特殊的 APN，如果连接到特定的运算符网络，该应用可以使用连接的网络，如 Wi-fi 网络。 下面的示例代码说明了如何应用可以使用多个 PDP 上下文的 Api，将数据传输的特殊 PDP 上下文，如果没有可用的网络连接。

``` syntax
// Reference the namespace
var connectivity = Windows.Networking.Connectivity;

// Current route policy
var currentRoutePolicy = null;
var currentConnectionSession = null;

function onLoad()
{
  // Register for network status change
  connectivity.networkInformation.addEventListener("networkstatuschanged", OnNetworkStatusChange);
  // Process the current status
  handleNetworkChange();
}

//  Handle newtork status changes
function onNetworkStatusChange()
{
  HandleNetworkChange();
}

// On network status change:
//  if there is no connectionPolicy, evaluate a new one
//  if there is a current connectionPolicy ==> verify it is still valid 
//      evaluate a new one if the current connectionPolicy is not valid 
function handleNetworkChange()
{
  if (isCurrentPolicyStillValid())
  {
    //the current policy is still valid.
    return;
  }

  //  No policy or current policy is not good anymore
  //  cleanup any previous configuration
  if (currentRoutePolicy)
  {
    connectivity.ConnectivityManager.removeHttpRoutePolicy(currentRoutePolicy);
    currentRoutePolicy = null;
  }

  //  if a different APN was connected, disconnect it to free up resources
  if (connectionConnectionSession != null)
  {
    connectionConnectionSession.close();
    connectionConnectionSession = null;
  }

  // evaluate connection policy
  startEvaluateConnectionPolicy();
}

//  evaluate if the current connectionPolicy is still valid
function isCurrentPolicyStillValid()
{
  if (null != currentRoutePolicy)
  {
    // a policy is currently in place, let's verify if it is still valid
    var currentProfile = currentRoutePolicy.connectionProfile();
    if (NetworkConnectivityLevel.none != currentProfile.GetNetworkConnectivityLevel())
    {
      // current policy is still good. bail out
      return true;
    }
  }
  return false;
}

// starts the evaluation of a new connection policy
function startEvaluateConnectionPolicy()
{
  // first try to get a free network if it is available
  var queryFilter = new connectivity.connectionProfileFilter();
  queryFilter.networkCostType = connectivity.networkCostType.unrestricted;
  queryFilter.isConnected = true;

  connectivity.networkInformation.findConnectionProfilesAsync(queryFilter).done(onSuccess, onFailure);
}

//  Succesfully retrieved at least one free connection profile
function onSuccess(results)
{
  if(results.count > 0)
  {
  //  Enfore the route to the http stack
  enforceHttpRoutePolicy(results[0]);

  // Backend data interaction with appropriate APIs(Open IFrame etc.)

  }
  else
  {
    onFailure();
  }
}

//  there are no free networks available at this time
function onFailure()
{
  //  create a request to connect a specific APN on the network
  // no free network available, connect
  var apnContext                      =   new connectivity.CellularApnContext();
  apnContext.accessPointName          =   "myAPN.com";
  apnContext.userName                 =   "APNusername"
  apnContext.password                 =   "APNPassword";
  apnContext.isCompressionEnabled     =   false;
  apnContext.authenticationType       =   connectivity.CellularApnAuthenticationType.none;

  //
  //  request the connection to Windows
  connectivity.connectivityManager.acquireConnectionAsync(apnContext).done(onConnectionSucceeded, onConnectionFailed);
}

//  on success Windows returns a ConnectionSession object that encapsulates the new connection profile
function onConnectionSucceeded(result)
{
  // keep the connectionSession in scope
  currentConnectionSession= result;
  //  create a route policy for the new connection
  enforceHttpRoutePolicy(currentConnectionSession.ConnectionProfile,new hostName("video.mydomain.com"),Windows.Networking.DomainNameType.suffix);

  // Backend data interaction with appropriate APIs(Open IFrame etc.)

}

//  Windows was not able to connect the specified APN
function onConnectionFailed()
{
  // display error message and just wait for Network Status Change event to try again
}

//  utility function to enforce a route policy
function enforceHttpRoutePolicy(connectionProfile,targetSuffix)
{
  //  Keep the route request global so we can close it later
  currentRoutePolicy= new connectivity.routePolicy(connectionProfile, targetSuffix);
  //  Indicate the new route policy to the Http stack
  connectivity.connectivityManager.addHttpRoutePolicy(currentRoutePolicy);
}

//  cleanup on shutdown
function onShutdown()
{
  //  Remove the route policy from HttpStack
  connectivity.connectivityManager.removeHttpRoutePolicy(currentRoutePolicy);
  currentRoutePolicy = null;

  //  If a different APN was connected, disconnect it to free up resources
  if(currentConnectionSession!= null)
  {
    currentConnectionSession.close();
  }
}
```

### <a name="span-idscenariomobilebroadbandapprequiresspecialpdpcontextforsubscriptionpurchaseandprovisioningspanspan-idscenariomobilebroadbandapprequiresspecialpdpcontextforsubscriptionpurchaseandprovisioningspanspan-idscenariomobilebroadbandapprequiresspecialpdpcontextforsubscriptionpurchaseandprovisioningspanscenario-mobile-broadband-app-requires-special-pdp-context-for-subscription-purchase-and-provisioning"></a><span id="Scenario__Mobile_broadband_app_requires_special_PDP_Context_for_subscription_purchase_and_provisioning"></span><span id="scenario__mobile_broadband_app_requires_special_pdp_context_for_subscription_purchase_and_provisioning"></span><span id="SCENARIO__MOBILE_BROADBAND_APP_REQUIRES_SPECIAL_PDP_CONTEXT_FOR_SUBSCRIPTION_PURCHASE_AND_PROVISIONING"></span>方案：移动宽带应用订阅购买和设置过程中需要特殊 PDP 上下文

在此方案中，移动宽带应用订阅购买和设置过程中需要特殊的 PDP 上下文。 此应用将激活而不考虑已连接网络的特殊 PDP 上下文。

``` syntax
var connectivity = Windows.Networking.Connectivity;
var currentRoutePolicy = null;
var currentConnectionSession = null;

function onLoad()
{
  // Register for network status change
  connectivity.networkInformation.addEventListener("networkstatuschanged", OnNetworkStatusChange);
  // Process the current status
  handleNetworkChange();
}

function onNetworkStatusChange()
{
  HandleNetworkChange();
}

//  Create the PDP Context/APN Data 
var apnContext                      =   new connectivity.CellularApnContext();
apnContext.providerId               =   "23545";
apnContext.accessPointName          =   "myAPN.com";
apnContext.userName                 =   "APNusername"
apnContext.password                 =   "";
apnContext.isCompressionEnabled     =  false;
apnContext.authenticationType       =   connectivity.CellularApnAuthenticationType.none;

//  Request the connection to Windows
connectivity.connectivityManager.acquireConnectionAsync(apnContext).done(onConnectionSucceeded, onConnectionFailed);

//  On successful connection to PDP Context,  Windows returns a ConnectionSession object that incapsulate the new connection profile
function onConnectionSucceeded(result)
{
  // keep the connectionSession in scope
  currentConnectionSession= result;

  //  create a route policy for the new connection
  currentRoutePolicy = new connectivity.routePolicy(currentConnectionSession.ConnectionProfile, new hostName("video.mydomain.com"),Windows.Networking.DomainNameType.suffix);

  //  indicate the new route policy to the Http stack
  connectivity.connectivityManager.addHttpRoutePolicy(currentRoutePolicy);

  // Backend data interaction with appropriate APIs(Open IFrame etc.)

  // After completing the data transfer remove the Route Policy
  connectivity.connectivityManager.removeHttpRoutePolicy(currentRoutePolicy);
  currentRoutePolicy = null;

  // Disconnect the PDP Context to free up resources
  currentConnectionSession.close();

}

function handleNetworkChange()
{
  // App behavior to handle network 
  var currentProfile = currentRoutePolicy.connectionProfile();
  if (NetworkConnectivityLevel.none != currentProfile.GetNetworkConnectivityLevel())
  {
    // The special PDP Context is disconnected, app should handle this. It can request another connection to special PDP Context or it can show error to the user.
  }
}
```

### <a name="span-idconsiderationsformobilebroadbandappsspanspan-idconsiderationsformobilebroadbandappsspanspan-idconsiderationsformobilebroadbandappsspanconsiderations-for-mobile-broadband-apps"></a><span id="Considerations_for_mobile_broadband_apps"></span><span id="considerations_for_mobile_broadband_apps"></span><span id="CONSIDERATIONS_FOR_MOBILE_BROADBAND_APPS"></span>移动宽带应用程序的注意事项

移动宽带应用程序可以获取每个 PDP 上下文的本地数据使用情况信息和影响 Windows 的特殊 PDP 上下文的策略。

### <a name="span-idlocaldatausagespanspan-idlocaldatausagespanspan-idlocaldatausagespanlocal-data-usage"></a><span id="Local_data_usage"></span><span id="local_data_usage"></span><span id="LOCAL_DATA_USAGE"></span>本地数据使用情况

在 Windows 8 中提供的基于订阅的持续关系及用户通过你的移动宽带应用具有显示当前数据使用情况的功能。 用户可以查看其当前的数据使用情况，并了解其计费周期或会话结束日期，以便做出适当的决策。 若要减少最大程度地在网络上的负载，应定期检查与网络的数据使用情况。 Windows 提供了一个本地的数据使用情况 API，可用于将与数据使用情况向用户显示当前数据使用情况相结合。

特殊的 PDP 上下文提供能够区分到特定应用或服务的数据访问费用。 每个不同的 PDP 上下文被视为本地数据使用情况计数器不同的配置文件。 移动宽带应用程序可以查询每个 PDP 上下文的本地数据使用情况特定时间段，类似于如何将 internet PDP 上下文从事 Windows 8。 此信息可用于向用户显示相应的数据使用体验。

下面的示例代码演示了如何使用网络 Api 来读取所有 PDP 上下文的本地数据使用情况：

``` syntax
// Get the network account ID.
IReadOnlyList<string> networkAccIds = Windows.Networking.NetworkOperators.MobileBroadbandAccount.AvailableNetworkAccountIds;

if (networkAccIds.Count == 0)
{
  rootPage.NotifyUser("No network account ID found", NotifyType.ErrorMessage);
  return;
}

// For the sake of simplicity, assume we want to use the first account.
// Refer to the MobileBroadbandAccount API's how to select a specific account ID.
string networkAccountId = networkAccIds[0];

// Create mobile broadband object for specified network account ID
var mobileBroadbandAccount = Windows.Networking.NetworkOperators.MobileBroadbandAccount.CreateFromNetworkAccountId(networkAccountId);

// Get all connection profiles associated with this network account ID
var connectionProfiles = mobileBroadbandAccount.GetConnectionProfiles();

// Collect local usages for last one hour
DateTime endTime = DateTime.Now;
TimeSpan timeDiff = TimeSpan.FromHours(1);
DateTime startTime = endTime.Subtract(timeDiff);
string message = string.Empty;

foreach (var connectionProfile in connectionProfiles)
{
  // Display local usages for each connection profiles
  DataUsage localUsage = connectionProfile.GetLocalUsage(startTime, endTime);
  message += "Connection Profile Name:  " + connectionProfile.ProfileName + "\n\n";
  message += "Local Data Usage from " + startTime.ToString() + " to " + endTime.ToString() + ":\n";
  message += " Bytes Sent     : " + localUsage.BytesSent + "\n";
  message += " Bytes Received : " + localUsage.BytesReceived + "\n\n";
}

// Print the message string
```

### <a name="span-idpoliciesspanspan-idpoliciesspanspan-idpoliciesspanpolicies"></a><span id="Policies"></span><span id="policies"></span><span id="POLICIES"></span>策略

一些运算符已表明特殊 PDP 上下文使带宽受到限制。 激活特殊 PDP 上下文，但不是具有使用特殊的 PDP 上下文的访问权限的应用，可以创建拒绝服务攻击。 为业务关系的特定应用，应限制特殊 APNs 的使用情况。 你将能够使用特殊的 APN 名称提供 Windows UWP 应用的列表。 Windows 将使用该信息来限制对特殊 Apn 的访问权限。 如果未提供一个列表，Windows 假定特殊 PDP 上下文处于打开状态，所有应用。

**请注意**  这只是为了避免在特殊 PDP 上下文上的额外流量。 您不能作为将应用限制为特殊 PDP 上下文的安全机制依赖于此。 如果你想要限制对特殊 PDP 上下文的访问，则必须在网络上实现某些身份验证或安全机制。 例如，可以使用一个允许仅特定 PDP 上下文特定 IP 地址筛选器。

 

某些移动网络不支持多个 PDP 上下文。 你可以设置是否在网络或不支持多个 PDP 上下文。 如果你的网络不支持多个 PDP 上下文，Windows 不应允许以特殊 APNs 上创建按需连接的应用。 默认情况下，Windows 假定支持多个 PDP 上下文。

下面的 XML 文件示例演示如何使用 Windows 预配的元数据的特殊 PDP 上下文提供的允许的应用列表：

``` syntax
<?xml version="1.0" encoding="utf-8"?>
<CarrierProvisioning xmlns="http://www.microsoft.com/networking/CarrierControl/v1">
  <Global>
    <!-- Adjust the Carrier ID to fit your own ID. Refer to the documentation about Carrier ID's. -->
    <CarrierId>{11111111-1111-1111-1111-111111111111}</CarrierId>
    <!-- Adjust the Susbscriber ID. Refer to the documentation about Subscriber ID's. -->
    <SubscriberId>1234567890</SubscriberId>
  </Global>
  <Extensions>
    <Extensions_v2 xmlns="http://www.microsoft.com/networking/CarrierControl/v2">
      <AdditionalPDPContexts>
        <MultiplePDPContextPolicies MultiplePDPContextSupport="true">
          <PDPContextPolicy>
            <!-- Adjust the profile name -->
            <Name>Contoso1</Name>
            <Context>
              <!-- Adjust the access string to your APN. -->
              <AccessString>Contoso.Contoso1</AccessString>
              <!-- Adjust the UserLogonCred to fit your UserLogonCred. Refer to the documentation about UserLogonCred's. -->
              <UserLogonCred>
                <UserName>user1</UserName>
                <Password>password1</Password>
              </UserLogonCred>
            </Context>
            <AppIDList>
              <!-- Adjust the AppId to your AppId -->
              <AppID>Contoso.Sample1.CS_dsarewaj</AppID>
              <AppID>Contoso.Sample2.CPP_dsarewaj</AppID>
            </AppIDList>
          </PDPContextPolicy>
          <PDPContextPolicy>
            <!-- Adjust the profile name -->
            <Name>Contoso2</Name>
            <Context>
              <!-- Adjust the access string to your APN. -->
              <AccessString>Contoso.Contoso2</AccessString>
              <!-- Adjust the UserLogonCred to fit your UserLogonCred. Refer to the documentation about UserLogonCred. -->
              <UserLogonCred>
                <UserName>user2</UserName>
                <Password>password2</Password>
              </UserLogonCred>
            </Context>
            <AppIDList>
              <!-- Adjust the AppId to your AppId -->
              <AppID>Contoso.Sample3.CS_dsarewaj</AppID>
              <AppID>Contoso.Sample4.CPP_dsarewaj</AppID>
            </AppIDList>
          </PDPContextPolicy>
        </MultiplePDPContextPolicies>
      </AdditionalPDPContexts>
    </Extensions_v2>
  </Extensions>
</CarrierProvisioning>
```

## <a name="span-idaudioandvideostreamingspanspan-idaudioandvideostreamingspanspan-idaudioandvideostreamingspanaudio-and-video-streaming"></a><span id="Audio_and_video_streaming"></span><span id="audio_and_video_streaming"></span><span id="AUDIO_AND_VIDEO_STREAMING"></span>音频和视频流


音频流的应用可以播放音频或视频流使用特殊的 PDP 上下文。 类似于 HTTP Api，应用可以使用以下逻辑来使用播放音频或视频&lt;音频&gt;或&lt;视频&gt;标记。

![流式处理应用程序工作流](images/mb-pdp-fig6.jpg)

可以使用[播放器框架](https://archive.codeplex.com/?p=playerframework)或基于其他视频框架[WinInet](https://docs.microsoft.com/windows/desktop/WinInet/portal) Api。

## <a name="span-idinstantgospanspan-idinstantgospanspan-idinstantgospaninstantgo"></a><span id="InstantGo"></span><span id="instantgo"></span><span id="INSTANTGO"></span>InstantGo


InstantGo 即时关闭用户都希望能在他们的手机的用户体验，提供一个即时。 就像在手机上 InstantGo 使系统保持最新、 最新的且可访问合适的网络可用时。 在低功耗 Pc 平台上的 InstantGo 必须满足特定的 Windows 认证要求。

在 InstantGo 中支持以下方案：

-   使用全新的内容更新动态磁贴

-   接收电子邮件

-   下载文件，或将其上传到网站

-   共享内容，例如在网站上的照片

-   接收即时消息

-   接收 VoIP 呼叫

-   在实时通信

-   播放背景音频和音乐

InstantGo 的详细信息，请参阅[简介 InstantGo](https://docs.microsoft.com/windows-hardware/design/device-experiences/modern-standby)。

移动宽带应用可以使用特殊的 PDP 上下文，使其中一些 InstantGo 方案。 您需要使用以下逻辑来重新连接到特殊的 PDP 上下文，如果它断开连接，因为它超出范围。 当设备进入连接待机电源状态时，Windows 将在 10 分钟后断开与特殊 PDP 上下文的所有连接，并且您的应用程序必须请求重新连接。

有关如何启用后台移动宽带应用中的网络的详细信息，请参阅[后台任务简介](https://www.microsoft.com/download/details.aspx?id=27411)并[背景网络](https://www.microsoft.com/download/details.aspx?id=28999)。

![instantgo 与 pdp 上下文](images/mb-pdp-fig5.jpg)

### <a name="span-idaudiostreaminginbackgroundspanspan-idaudiostreaminginbackgroundspanspan-idaudiostreaminginbackgroundspanaudio-streaming-in-background"></a><span id="Audio_streaming_in_background"></span><span id="audio_streaming_in_background"></span><span id="AUDIO_STREAMING_IN_BACKGROUND"></span>背景中的流式处理音频

音频流式处理应用程序可以通过使用特殊的 PDP 上下文和连接待机电源状态中背景的音频。 有关如何播放音频，在后台的详细信息，请参阅[方法如何播放音频，在后台](https://docs.microsoft.com/previous-versions/windows/apps/hh700367(v=win.10))。

### <a name="span-idreal-timecommunicationappsspanspan-idreal-timecommunicationappsspanspan-idreal-timecommunicationappsspanreal-time-communication-apps"></a><span id="Real-time_communication_apps"></span><span id="real-time_communication_apps"></span><span id="REAL-TIME_COMMUNICATION_APPS"></span>实时通信应用

实时通信应用，例如 VoIP 或聊天应用可以接收唤醒特殊 PDP 上下文上的触发器。 触发器唤醒后，应用在所有时间包括在系统中的连接待机电源状态时触发。 有关如何启用触发器唤醒的详细信息，请参阅[背景网络](https://www.microsoft.com/download/details.aspx?id=28999)。

若要启用此方案中，移动宽带设备应支持唤醒筛选器在特殊 PDP 上下文，如中所述[移动宽带接口模型 (MBIM) 规范](https://docs.microsoft.com/windows-hardware/drivers/network/mb-interface-model)。

## <a name="mobile-broadband-devices"></a>移动宽带设备


若要支持多个 PDP 上下文，移动宽带设备固件必须支持多个 PDP 上下文，如中所定义[MBIM 规范](https://go.microsoft.com/fwlink/?linkid=620028)。 它还必须传递的任何 Windows 硬件认证工具包测试特定于多个 PDP 上下文。

由于此功能是特定的运算符，它是可选的移动宽带设备。 如果你需要此功能，必须使用以下运算符要求中添加多个 PDP 上下文功能：

-   设备固件应支持多个 IP 数据流作为中的详细说明部分 10.5.12.1 [MBIM 规范](https://go.microsoft.com/fwlink/?linkid=620028)。 这包括支持的 Cid 的所有控件实现和 IP 数据流为完整的多个 PDP 上下文的支持。

-   设备固件必须支持多个双重持有者 （IPv4 和 IPv6） PDP 上下文，以供 Windows。

    -   这包括 internet 连接的 1 和其他 PDP 上下文的移动宽带应用程序，根据您的要求。

    -   这不需要固件可能用于 SMS 的设备管理 PDP 上下文和其他管理上下文。

-   设备固件应该能够利用主机操作系统适当地为已在其固件中在内部设备管理的 PDP 上下文的请求。

-   设备固件应该继续抽象 SMS PDP 上下文，并将它们路由通过 SMS Cid 而不考虑其不超过使用持有者。

 

 





