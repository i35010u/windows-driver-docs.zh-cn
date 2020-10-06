---
title: 使用多个 PDP 上下文开发应用
description: 使用多个 PDP 上下文开发应用
ms.assetid: 6a977a69-397d-4922-890d-1810dd54dff4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b1e01c1b1f227356bcf08a183d18884a5346c02
ms.sourcegitcommit: 20eac54e419a594f7cea766ee28f158559dfd79c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "91754872"
---
# <a name="developing-apps-using-multiple-pdp-contexts"></a>使用多个 PDP 上下文开发应用

数据包数据协议 (PDP) 上下文提供一个数据包数据连接，通过该连接，设备和移动网络可以交换 IP 数据包。 根据3GPP 标准，一次可以有一个设备激活多个 PDP 上下文。 在 Windows 8.1 和 Windows 10 中，支持多个 PDP 上下文，并使应用能够通过特殊的 PDP 上下文与 Windows 8 中支持的 internet PDP 上下文通信。 你可以使用此功能在 Windows 上创建与众不同的体验和创新性服务。 你还可以与应用程序开发人员合作，为客户开发优质的 VOIP 和视频流体验。

下面是一个图，其中显示了多个 PDP 上下文在 Windows 8.1 和 Windows 10 中的工作方式：

![图 1](images/mb-pdp-fig1.jpg)

使用本主题中的下列部分来详细了解多个 PDP 上下文：

- [关键方案](#key-scenarios)

- [移动宽带应用](#mobile-broadband-apps)

- [移动宽带设备](#mobile-broadband-devices)

## <a name="key-scenarios"></a>关键方案

可以使用多个 PDP 上下文来启用高级服务。

- **区分计费** –您可以使用多个 PDP 上下文改变数据或计费限制。 例如，Contoso 是为其客户开发了数据备份应用的移动运营商。 作为移动运营商，Contoso 可以创建多个 PDP 上下文，让高级订户免费使用该应用。 所有其他订阅者单独收费以使用它。

- **丰富的通信服务** –由 GSM 关联创建的全球计划，提供丰富的通信服务，例如增强的电话簿、增强的消息传递和更多的调用。 丰富的通信服务跨移动运营商提供互操作性，并提供新的方法来使用现有资产和功能来提供高质量和创新性的通信服务。

- **赞助连接性** –这允许用户使用特定类型的内容，而无需考虑其每月数据使用量。 内容提供商通过直接支付移动运营商、开展收入共享交易或进行一些其他业务安排，来补偿移动运营商。

- **个人热点** –当使用连接作为个人热点时，某些移动运营商会对不同的费率收费。 可以使用多个 PDP 上下文区分这两者。

## <a name="mobile-broadband-apps"></a>移动宽带应用

UWP mobile 宽带应用可以利用多个 PDP 上下文来激活特殊的 PDP 上下文并指定路由数据流量的规则。 这些应用可以为特定目标或所有数据流量创建规则。

当移动宽带应用需要与网络交换数据时，它会检查可用网络和连接的网络。 如果移动宽带应用对于这些网络中的任何一种都有特殊规则，它将使用连接管理器 API 来打开特殊的 PDP 上下文。 如果此连接成功，则 PDP 上下文会为此连接提供路由规则并使用网络 Api 传输数据。 如果移动宽带应用收到 [**NetworkStatusChanged**](/uwp/api/Windows.Networking.Connectivity.NetworkInformation#Windows_Networking_Connectivity_NetworkInformation_NetworkStatusChanged) 事件，以查看是否有任何连接已更改以及是否需要为新连接打开 PDP 上下文，则应该重复此操作。

![图 2](images/mb-pdp-fig2.jpg)

### <a name="networking-apis"></a>网络 Api

若要使用特殊的 PDP 上下文发送数据，Microsoft Store 应用程序必须基于用于传输数据的网络 Api 使用不同的逻辑。

### <a name="http-based-apis"></a>基于 HTTP 的 Api

基于 HTTP 的 Api，如[**XMLHTTPRequest**](/previous-versions/windows/apps/br229787(v=win.10)) [**、**](/uwp/api/Windows.Web.Syndication) [IXHR2](/previous-versions/windows/desktop/ixhr2/ixmlhttprequest2-portal)、 [**AtomPub**](/uwp/api/Windows.Web.AtomPub)和基于 windows HTTP 协议的 api （如 JQuery 和[**windows**](/uwp/api/Windows.Web.Http)），不能绑定到特定的接口，也不能绑定到特定的接口。 对于这些 Api，Windows 使用策略来处理将数据路由到特殊的 PDP 上下文。 激活特殊的 PDP 上下文后，应用可根据目标和特殊的 PDP 上下文指定路由规则。 目标可以是域名或 IP 地址，如 video.fabrikam.com、contoso.com 或123.23.34.333。 指定路由规则后，如果应用使用上述任何 HTTP Api 来传输数据，则 Windows 将基于路由规则将数据发送到特殊的 PDP 上下文。 应用传输完数据后，应该断开特殊的 PDP 上下文的连接，并删除路由策略。

>[!NOTE]
>[**后台传输 api**](/uwp/api/Windows.Networking.BackgroundTransfer) 和 [HTTP 客户端 (c # ) api](/previous-versions/visualstudio/hh193681(v=vs.118)) 不能使用路由策略。

![图 3](images/mb-pdp-fig4.jpg)

### <a name="socket-based-apis"></a>基于套接字的 Api

[**Windows.**](/uwp/api/Windows.Networking.Sockets) socket 命名空间中提供的基于套接字的 api （例如 TCP、UDP 和流套接字）提供绑定到特定接口的机制。 应用使用套接字 Api 时，应绑定到特定的接口，以便将数据路由到特殊的 PDP 上下文。 激活特殊的 PDP 上下文后， [**AcquireConnectionAsync**](/uwp/api/Windows.Networking.Connectivity.ConnectivityManager#Windows_Networking_Connectivity_ConnectivityManager_AcquireConnectionAsync_Windows_Networking_Connectivity_CellularApnContext_) API 将向应用提供接口信息。 它可以使用此信息绑定到特定的接口并开始传输数据。

![图 4](images/mb-pdp-fig3.jpg)

### <a name="multiple-pdp-content-api-info"></a>多个 PDP 内容 API 信息

Windows 8.1 和 Windows 10 添加了以下 Api 以支持多个 PDP 上下文：

- [**CellularApnContext**](/uwp/api/Windows.Networking.Connectivity.CellularApnContext) 此类包含用于指定网络上的访问点的属性。 **CellularApnContext**对象与[**AcquireConnectionAsync**](/uwp/api/Windows.Networking.Connectivity.ConnectivityManager#Windows_Networking_Connectivity_ConnectivityManager_AcquireConnectionAsync_Windows_Networking_Connectivity_CellularApnContext_)调用一起传递，以建立与特定访问点的连接。

- [**ConnectivityManager：： AcquireConnectionAsync**](/uwp/api/Windows.Networking.Connectivity.ConnectivityManager#Windows_Networking_Connectivity_ConnectivityManager_AcquireConnectionAsync_Windows_Networking_Connectivity_CellularApnContext_) 此 API 为指定接入点名称激活新连接 (APN) 或 PDP 上下文。 此异步方法允许应用使用适当的配置信息请求连接到特定 APN 或 PDP 上下文。 激活专用接入点后，它将显示为 Windows 和应用的新虚拟接口。

- [**ConnectivityManager：： AddHttpRoutePolicy**](/uwp/api/Windows.Networking.Connectivity.ConnectivityManager#Windows_Networking_Connectivity_ConnectivityManager_AddHttpRoutePolicy_Windows_Networking_Connectivity_RoutePolicy_) 此方法添加一个策略，该策略将由 HTTP stack 通信用来将数据路由到特殊的 PDP 上下文。 应用可以基于目标指定策略，例如域名和 IP 地址，以及特殊的 PDP 上下文配置文件。 应用创建策略后，Windows HTTP stack 使用策略将数据路由到特殊的 PDP 上下文。

- [**ConnectivityManager：： RemoveHttpRoutePolicy**](/uwp/api/Windows.Networking.Connectivity.ConnectivityManager#Windows_Networking_Connectivity_ConnectivityManager_RemoveHttpRoutePolicy_Windows_Networking_Connectivity_RoutePolicy_) 此方法删除以前添加的 HTTP 路由策略。

下面的代码演示如何将这些 Api 用于基于 HTTP 的数据传输：

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

下面的代码演示如何使用这些 Api 进行基于套接字的数据传输：

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

您的应用程序必须处理 [**NetworkStatusChanged**](/uwp/api/Windows.Networking.Connectivity.NetworkInformation#Windows_Networking_Connectivity_NetworkInformation_NetworkStatusChanged) 事件，才能处理特殊的 PDP 上下文连接上的任何网络转换。

### <a name="scenario-premium-mobile-broadband-app-provides-free-data-access-using-special-apn"></a>方案：高级移动宽带应用使用特殊 APN 提供免费数据访问

在此方案中，移动宽带应用使用特殊的 PDP 上下文提供免费的数据访问。 该应用程序使用连接的网络（如 Wi-fi 网络）（如果它是免费网络），或者如果连接到特定的操作员网络，则使用特殊接入点。 下面的示例代码演示了在没有任何可用网络连接的情况下，应用如何使用多个 PDP 上下文 Api 在特殊的 PDP 上下文中传输数据。

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

### <a name="scenario-mobile-broadband-app-requires-special-pdp-context-for-subscription-purchase-and-provisioning"></a>方案：移动宽带应用需要特殊的 PDP 上下文才能进行订阅购买和预配

在这种情况下，移动宽带应用需要特殊的 PDP 上下文来购买和预配订阅。 此应用将激活特殊的 PDP 上下文，而不考虑连接的网络。

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

### <a name="considerations-for-mobile-broadband-apps"></a>移动宽带应用的注意事项

移动宽带应用可以获取每个 PDP 上下文的本地数据使用情况信息，并会影响带有特殊 PDP 上下文策略的 Windows。

### <a name="local-data-usage"></a>本地数据使用情况

在 Windows 8 中，您可以通过移动宽带应用程序与用户进行基于订阅的实时关系，此应用程序可以显示当前的数据使用情况。 用户可以查看其当前数据使用情况，并了解他们的计费周期或会话结束日期以做出适当的决策。 为了尽可能减少网络上的负载，应定期检查网络的数据使用情况。 Windows 提供了本地数据使用情况 API，你可以使用该 API 与数据使用进行合并，以向用户显示当前的数据使用情况。

特殊的 PDP 上下文使你能够将数据访问费用区分给某些应用程序或服务。 为本地数据使用计数器将每个不同的 PDP 上下文视为不同的配置文件。 移动宽带应用可以在特定的持续时间内查询每个 PDP 上下文的本地数据使用情况，这与 internet PDP 上下文在 Windows 8 中的工作方式类似。 您可以使用此信息向用户显示适当的数据使用体验。

下面的示例代码演示如何使用网络 Api 来读取所有 PDP 上下文的本地数据使用情况：

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

### <a name="policies"></a>策略

某些操作员指出，特殊的 PDP 上下文的带宽有限。 激活特殊 PDP 上下文但无权使用特殊 PDP 上下文的应用可能会造成拒绝服务攻击。 应将特殊 APNs 的使用限制为具有业务关系的特定应用。 可以向 Windows 提供具有特殊 APN 名称的 UWP 应用列表。 Windows 将使用此信息来限制对特定 APNs 的访问。 如果未提供列表，Windows 会假定为所有应用打开了特殊的 PDP 上下文。

>[!NOTE]
>这只是为了避免特殊的 PDP 上下文的额外流量。 不能将此作为将应用限制为特殊 PDP 上下文的安全机制。 如果要限制对特殊 PDP 上下文的访问，必须在网络上实施一些身份验证或安全机制。 例如，你可以使用只允许特定 PDP 上下文的特定 IP 地址的筛选器。

某些移动网络不支持多个 PDP 上下文。 你可以设置网络是否支持多个 PDP 上下文。 如果你的网络不支持多个 PDP 上下文，Windows 将不允许应用在特定 APNs 上创建按需连接。 默认情况下，Windows 假设你支持多个 PDP 上下文。

下面的示例 XML 文件演示如何使用 Windows 预配元数据为特殊的 PDP 上下文提供允许的应用列表：

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

## <a name="audio-and-video-streaming"></a>音频和视频流

音频流式处理应用可以使用特殊的 PDP 上下文播放音频或视频流。 类似于 HTTP Api，你的应用程序可以通过使用 &lt; 音频 &gt; 或 &lt; 视频标记来使用以下逻辑播放音频或视频 &gt; 。

![流式处理应用工作流](images/mb-pdp-fig6.jpg)

您可以基于[WinInet](/windows/desktop/WinInet/portal) Api 使用[播放机框架](https://archive.codeplex.com/?p=playerframework)或其他视频框架。

## <a name="instantgo"></a>InstantGo

InstantGo 提供用户在电话上期望的即时启动的用户体验。 就像在手机上一样，InstantGo 使系统可以在合适的网络可用时保持最新、最新和可访问性。 低能耗 Pc 平台上的 InstantGo 必须满足特定的 Windows 认证要求。

InstantGo 支持以下方案：

- 更新包含新内容的动态磁贴

- 接收电子邮件

- 下载文件，或将文件上传到网站

- 在网站上共享内容，如照片

- 接收即时消息

- 接收 VoIP 呼叫

- 实时通信

- 播放背景音频和音乐

有关 InstantGo 的详细信息，请参阅 [InstantGo 简介](/windows-hardware/design/device-experiences/modern-standby)。

你的移动宽带应用可以使用特殊的 PDP 上下文来实现其中某些 InstantGo 方案。 如果因超出范围而断开连接，则需要使用以下逻辑重新连接到特殊的 PDP 上下文。 设备进入连接待机电源状态后，在10分钟后，Windows 会断开与特殊 PDP 上下文的所有连接，应用程序必须再次请求连接。

![带有 pdp 上下文的 instantgo](images/mb-pdp-fig5.jpg)

### <a name="audio-streaming-in-background"></a>后台音频流

音频流式处理应用程序可以通过使用特殊的 PDP 上下文，在后台和处于连接状态的待机电源状态中播放音频。 有关如何在后台播放音频的详细信息，请参阅 [如何在后台播放音频](/previous-versions/windows/apps/hh700367(v=win.10))。

### <a name="real-time-communication-apps"></a>实时通信应用

实时通信应用（如 VoIP 或聊天应用）可以在特殊的 PDP 上下文上收到唤醒触发器。 唤醒触发器允许在任何时间（包括系统处于连接待机电源状态时）触发应用。

若要启用此方案，移动宽带设备应支持针对特殊 PDP 上下文的唤醒筛选器，如 [移动宽带接口模型 (MBIM) 规范](../network/mb-interface-model.md)中所述。

## <a name="mobile-broadband-devices"></a>移动宽带设备

为了支持多个 PDP 上下文，移动宽带设备的固件必须支持多个 PDP 上下文，如 [MBIM 规范](https://www.usb.org/document-library/mobile-broadband-interface-model-v10-errata-1-and-adopters-agreement)中所定义。 它还必须传递特定于多个 PDP 上下文的任何 Windows 硬件认证工具包测试。

由于此功能是特定于操作员的，因此对于移动宽带设备是可选的。 如果需要此功能，必须在操作员要求中添加多个 PDP 上下文功能，如下所示：

- 设备固件应支持多个 IP 数据流，如 [MBIM 规范](https://www.usb.org/document-library/mobile-broadband-interface-model-v10-errata-1-and-adopters-agreement)的10.5.12.1 部分中所述。 这包括支持 Cid 和 IP 数据流的所有控制实现，完全支持多个 PDP 上下文。

- 设备固件必须支持多个双载荷 (IPv4 & IPv6) PDP 上下文以供 Windows 使用。

  - 这包括1个用于 internet 连接，并根据你的要求提供额外的 PDP 上下文。

  - 这不需要设备托管的 PDP 上下文，固件可能会将其用于短信和其他管理上下文。

- 设备固件应能够正常利用主机操作系统请求，以实现已在其固件内部进行设备管理的 PDP 上下文。

- 设备固件应继续抽象的短信 PDP 上下文，并通过 SMS Cid 路由它们，而不考虑在下面使用的持有者。