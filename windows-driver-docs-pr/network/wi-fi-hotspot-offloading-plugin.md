---
title: Wi-Fi 热点卸载插件
description: Wi-Fi 热点卸载插件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a623890e8de324731d8d748e0288322bc0b0d0d3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382609"
---
# <a name="wi-fi-hotspot-offloading-plugin"></a>Wi-Fi 热点卸载插件

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]

若要启用 Wi-fi 卸载，创建并安装热点插件。 本主题讨论几个问题需要考虑开发热点插件时。 它还提供插件 Api 作为插件包的一部分实现的一般说明。

## <a name="planning-the-plugin"></a>规划插件

在开始之前插件开发，请务必解决以下问题：

### <a name="supported-authentication-methods"></a>支持的身份验证方法

标识通过该插件将支持的网络所需的身份验证方法。 热点卸载框架支持网络的三个的类：

* 使用 WISPr 1.0 或某些变体，以通过 HTTP 执行身份验证的用户和/或设备的网络。 这些网络表示的以下功能：
  * **HS_FLAG_CAPABILITY_NETWORK_AUTH_HTTP**
* 网络使用 SIM/AKA/EAP-AKA ' 设备进行身份验证。 这些网络表示由以下功能：
  * **HS_FLAG_CAPABILITY_NETWORK_AUTH_EAP_SIM**
  * **HS_FLAG_CAPABILITY_NETWORK_AUTH_EAP_AKA**
  * **HS_FLAG_CAPABILITY_NETWORK_AUTH_EAP_AKA_PRIME**

  对于基于 EAP 的网络，该插件还可以指定自定义领域通过使用**HS_FLAG_CAPABILITY_NETWORK_CUSTOM_REALM**功能。

* 不需要任何身份验证或为其插件具有不需要任何设备的凭据的独立的身份验证机制的网络的网络。 这些网络表示的以下功能：
  * **HS_FLAG_CAPABILITY_NETWORK_AUTH_NO_SIM**

### <a name="hidden-networks"></a>隐藏的网络

隐藏的网络必须预先在初始化时，由于网络不是扫描结果中可见。 由于隐藏网络的强大功能和隐私含义，框架将全局支持最多一个隐藏的网络。 因此，如果另一个插件还已请求到隐藏网络的连接，第二个插件的请求将被拒绝。 如果该插件需要隐藏的网络配置，它必须指定**HS_FLAG_CAPABILITY_NETWORK_TYPE_HIDDEN**为该网络的功能。

对于所有其他网络，应指定插件**HS_FLAG_CAPABILITY_NETWORK_TYPE_VISIBLE**功能。

### <a name="user-interface-display-strings"></a>用户界面显示字符串

自定义用户界面显示字符串，该插件用于用户，通信必须存储在字符串表 （在.rc 文件）。 该插件必须向热点卸载服务以使其能够加载相应的字符串传递字符串 Id。 目前，支持下列显示字符串：

* 提供程序名称 (最多**HS_CONST_MAX_PROVIDER_NAME_LENGTH**长度)
* 网络名称 (最多**HS_CONST_MAX_NETWORK_DISPLAY_NAME_LENGTH**长度)
* 在高级页上的消息 (最多**HS_CONST_MAX_ADVANCED_PAGE_STRING_LENGTH**长度)
* 任何其他字符串传递给用户使用 HSHostSendUserMessage 函数 (最多**最大\_路径**长度)。 有关详细信息，请参阅[HS_HOST_SEND_USER_MESSAGE](https://docs.microsoft.com/previous-versions/dn789353(v=vs.85))。

**注意：** 有关的 Wi-fi 热点卸载功能和常量的详细信息，请参阅[Wi-fi 热点卸载常量](https://docs.microsoft.com/previous-versions/mt800328(v=vs.85))。

## <a name="implementing-the-plugin"></a>实现插件

将插件实现为 DLL。 函数[HSPluginGetVersion](https://docs.microsoft.com/previous-versions/dn789345(v=vs.85))并[HSPluginInitPlugin](https://docs.microsoft.com/previous-versions/dn789346(v=vs.85))通过指定插件 DLL 的.def 文件中或通过将"__declspec （dllexport）"关键字添加到它们在必须公开函数实现。

## <a name="initialization"></a>初始化

按以下顺序在初始化时调用的 Api 插件：

### <a name="hsplugingetversion"></a>HsPluginGetVersion

插件应返回其版本信息，以验证插件版本与主机设备版本相匹配。 当前版本存储于常量**HS_CONST_HOST_CURRENT_API_VERSION**。

### <a name="hsplugininitplugin"></a>HSPluginInitPlugin

这是主初始化函数。 它提供到该插件的以下信息：

* 它会调用任何热点插件主机时使用的插件的上下文句柄 (* * HS_HOST_\*\\* * *) 函数
* 当前主机所使用的版本号 (**dwVerNumUsed**)
* 有关设备的信息 (**pDeviceIdentity**)
* 可用的插件指定为 HS_FLAG_CAPABILITY_NETWORK_ * * 类型的操作系统功能 (**dwHostCapabilities**)
* 该插件用来回调到主机的函数的处理程序 (**pHotspotHostHandlers**)

该插件会向热点插件宿主返回以下信息：

* 指向包含的插件 Api 列表的结构的指针 (**pHotspotPluginAPIs**)。 有关详细信息，请参阅[HOTSPOT_PLUGIN_APIS](https://docs.microsoft.com/previous-versions/dn789344(v=vs.85))。
* 指向包含该插件配置文件的结构的指针 (**pPluginProfile**)。 有关详细信息，请参阅[HS_PLUGIN_PROFILE](https://docs.microsoft.com/previous-versions/dn789365(v=vs.85))。 

该配置文件包括所有由插件所需的功能。 这由此得到的组合适用功能标志的值的单个值 (HS_FLAG_CAPABILITY_NETWORK_\*) 通过使用位或运算。 如果该插件指定 HS\_标志\_功能\_网络\_身份验证\_HTTP 功能或 HS\_标志\_功能\_网络\_身份验证\_EAP\_ \*功能， **dwSupportedSIMCount**的成员**HS_PLUGIN_PROFILE**结构必须设置为数受支持的 Sim。 该插件还必须指定它支持通过设置的网络的总数量**dwNumNetworksSupported**的成员及其**HS_PLUGIN_PROFILE**结构。

### <a name="hspluginqueryhiddennetwork-optional"></a>HsPluginQueryHiddenNetwork [Optional]

如果指定了该插件**HS_FLAG_CAPABILITY_NETWORK_TYPE_HIDDEN**功能和设备可以支持隐藏的网络，要获取的隐藏的网络信息的热点插件主机调用此函数插件。 有关详细信息，请参阅[HS_PLUGIN_QUERY_HIDDEN_NETWORK](https://docs.microsoft.com/previous-versions/dn789367(v=vs.85))。

### <a name="hspluginquerysupportedsims-optional"></a>HsPluginQuerySupportedSIMs [可选]

热点插件主机调用此函数，如果该插件指定一个非零值**dwSupportedSIMCount**。 调用时， **pNetworkIdentity**参数应为 NULL，该插件需要提供所有 sims 就支持的插件的列表。 调用此函数可能也更高版本上以标识与每个热点网络相关联的 Sim (在这段时间， **pNetworkIdentity**将为非 NULL)。 该插件必须提供支持 Sim 的列表。 有关详细信息，请参阅[HS_PLUGIN_QUERY_SUPPORTED_SIMS](https://docs.microsoft.com/previous-versions/dn789368(v=vs.85))。

## <a name="run-time"></a>运行的时

当网络变得可见，热点插件主机查询适用于每个网络，以确定它是否热点网络的插件。

### <a name="hspluginishotspotnetwork"></a>HSPluginIsHotspotNetwork

热点插件宿主将调用此函数可确定指定的网络是否热点网络。 通过网络 (SSID，身份验证类型、 密码) 的标识信息[HS_NETWORK_IDENTITY](https://docs.microsoft.com/previous-versions/dn789356(v=vs.85))结构。 该插件必须返回[eHS_NETWORK_STATE](https://docs.microsoft.com/previous-versions/dn756756(v=vs.85))枚举值，该值指示网络的类型。 如果它是热点网络，则通过返回有关网络的信息[HS_NETWORK_PROFILE](https://docs.microsoft.com/previous-versions/dn789357(v=vs.85))结构。 有关详细信息，请参阅[HS_PLUGIN_IS_HOTSPOT_NETWORK](https://docs.microsoft.com/previous-versions/dn789363(v=vs.85))。

### <a name="hspluginquerysupportedsims-optional"></a>HsPluginQuerySupportedSIMs [可选]

热点插件主机调用此函数，如果该插件指定的功能**HS\_标志\_功能\_网络\_身份验证\_HTTP**或**HS\_标志\_功能\_网络\_身份验证\_EAP**中*HS_NETWORK_PROFILE* 到调用参数[HS_PLUGIN_IS_HOTSPOT_NETWORK](https://docs.microsoft.com/previous-versions/dn789363(v=vs.85))。 此实例中调用时，pNetworkIdentity 参数应为非 NULL，并且插件必须提供 SIMs 列表支持 pNetworkIdentity 仅在指定的网络。 有关详细信息，请参阅[HS_PLUGIN_QUERY_SUPPORTED_SIMS](https://docs.microsoft.com/previous-versions/dn789368(v=vs.85))。

### <a name="hspluginquerycellularexceptionhosts-optional"></a>HSPluginQueryCellularExceptionHosts [Optional]

热点插件主机调用此函数，如果**dwNumCellularExceptions**字段[HS_NETWORK_PROFILE](https://docs.microsoft.com/previous-versions/dn789357(v=vs.85))结构，该插件返回设置为非零值。 该插件必须返回调用时的移动电话的持有者主机的列表。 有关详细信息，请参阅[HS_PLUGIN_QUERY_CELLULAR_EXCEPTION_HOSTS](https://docs.microsoft.com/previous-versions/dn789366(v=vs.85))。

## <a name="connect-time"></a>连接时间

当网络被视为可连接，或由用户选择网络时，以下调用顺序发生：

### <a name="hspluginpreconnectinit"></a>HSPluginPreConnectInit

热点插件主机调用此函数来通知与热点网络的连接中指定的插件[HS_NETWORK_IDENTITY](https://docs.microsoft.com/previous-versions/dn789356(v=vs.85))结构，返回的插件，正在进行中。 有关详细信息，请参阅[HS_PLUGIN_PRE_CONNECT_INIT](https://docs.microsoft.com/previous-versions/dn789364(v=vs.85))。

### <a name="hspluginstartpostconnectauth"></a>HSPluginStartPostConnectAuth

L2 连接完成后，热点插件主机调用此函数来通知插件以开始进行身份验证。 提供该插件*pConnectContext*， *pNetworkIdentity*，并*pNetworkProfile*从以前调用**HSPluginPreConnectInit**，但它还提供了*dwConnectionId*并*pSIMData*。 该插件必须存储连接 ID 并将其回调的主机时**HSHostPostConnectAuthCompletion**处理程序以通知操作系统的身份验证结果，以及在调用**HSHostSendUserMessage**如果一条消息需要传达给用户。 **PSIMData**结构包含有关在身份验证过程可以通过该插件需要 SIM 配置的其他信息。 如果该插件返回成功，它必须调用**HSHostPostConnectAuthCompletion**在 5 分钟或连接已断开连接。

## <a name="disconnect-and-reset"></a>断开连接，然后重置

网络断开连接时，显式通过一些用户或设备的操作或由于外部因素而隐式调用以下函数：

### <a name="hspluginstoppostconnectauth"></a>HSPluginStopPostConnectAuth

热点插件主机调用此函数来终止网络身份验证，因为该设备以从网络断开连接。 有关详细信息，请参阅[HS_PLUGIN_STOP_POST_CONNECT_AUTH](https://docs.microsoft.com/previous-versions/dn789372(v=vs.85))。

### <a name="hsplugindisconnectfromnetwork"></a>HSPluginDisconnectFromNetwork

热点插件主机调用此函数来通知该插件的设备将从网络断开连接。 有关详细信息，请参阅[HS_PLUGIN_DISCONNECT_FROM_NETWORK](https://docs.microsoft.com/previous-versions/dn789361(v=vs.85))。

### <a name="hspluginreset"></a>HSPluginReset

热点插件宿主将调用此函数可将该插件重置为其初始 （不仅仅是加载） 状态。 有关详细信息，请参阅[HS_PLUGIN_RESET](https://docs.microsoft.com/previous-versions/dn789369(v=vs.85))。

## <a name="periodic-calls"></a>定期调用

具体取决于特定参数由插件设置定期调用以下函数：

### <a name="hspluginsendkeepalive-optional"></a>HSPluginSendKeepAlive [可选]

热点插件主机调用此函数中指定的频率**dwKeepAliveTimeMins**的成员[HS_NETWORK_PROFILE](https://docs.microsoft.com/previous-versions/dn789357(v=vs.85))结构返回该插件。 有关详细信息，请参阅[HS_PLUGIN_SEND_KEEP_ALIVE](https://docs.microsoft.com/previous-versions/dn789370(v=vs.85))。

### <a name="hsplugincheckforupdates-optional"></a>HSPluginCheckForUpdates [可选]

热点插件主机调用此函数中指定的频率**dwProfileUpdateTimeDays**的成员[HS_PLUGIN_PROFILE](https://docs.microsoft.com/previous-versions/dn789365(v=vs.85))结构。 

## <a name="unloading-the-plugin"></a>卸载插件

### <a name="hsplugindeinit"></a>HSPluginDeinit

热点插件宿主将调用此函数可启用该插件以刷新任何未保存的信息并卸载之前关闭任何打开的句柄。 该插件将提供在卸载的原因*UnloadReason*参数。 有关详细信息，请参阅[HS_PLUGIN_DEINIT](https://docs.microsoft.com/previous-versions/dn789360(v=vs.85))。

## <a name="plugin-installation-package"></a>插件安装包

插件安装包应包括：

### <a name="the-plugin-dll-file"></a>插件 DLL 文件

必须签名 DLL 文件，并将其置于下**Programs\HotspotHost\\** <*ProviderName*>，其中 <*ProviderName*> 是DLL 提供程序名称。 

有关对 DLL 进行签名的信息，请参阅[二进制文件和包签名](https://docs.microsoft.com/previous-versions/windows/hardware/code-signing/dn789217(v=vs.85))。 

没有为命名 DLL 文件，因此确保在注册表中的文件的路径正确是所有所需的任何特定约定。 例如，可以为包中指定的注册表信息：

```xml
<RegKeys>
        <RegKey KeyName="$(hklm.software)\Microsoft\Windows Phone\HotspotOffload\Plugins\<ProviderName>">
          <RegValue Name="PluginRank" Type="REG_DWORD" Value="00000005" />
          <RegValue Name="PluginPath" Type="REG_SZ" Value="%SystemDrive%\Programs\HotspotHost\Orange\<ProviderName>\<HotspotPlugin.dll>" />
        </RegKey>
      </RegKeys>
```

### <a name="registry-configuration"></a>注册表配置

所需的注册表设置保存在下创建一个新条目：**HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Phone\HotspotOffload\Plugins\\**  *ProviderName*。

*ProviderName*必须是唯一的插件提供商或移动运算符。

在注册表项下，必须保存以下值：

| 名称 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- |
| PluginPath | [REG_SZ] | 名称和 DLL 的完整路径。 |
| PluginRank | [REG_DWORD] | 介于 1 至 250，非独占之间的任何正值 （为 Microsoft 保留 0）。 较低的值表示较高的优先级。 如果两个插件具有相同的排名，热点服务任意优先而不是另一个。 |

### <a name="data-files-that-contain-connection-specific-information-such-as-a-list-of-ssids-encrypted-credentials-etc-optional"></a>包含特定于连接的信息，例如列表的 Ssid，加密凭据的数据文件等 [可选]

数据文件应保存在： `Data\SharedData\HotspotHost\Plugins\<ProviderName>`。

