---
title: Wi-Fi 热点卸载插件
description: Wi-Fi 热点卸载插件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20040efa4db89c77653b4477f93414fb0ca2fca0
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207747"
---
# <a name="wi-fi-hotspot-offloading-plugin"></a>Wi-Fi 热点卸载插件

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]

若要启用 Wi-fi 卸载，请创建并安装热点插件。 本主题讨论开发热点插件时要考虑的一些问题。 它还提供了要作为插件包的一部分实现的插件 Api 的一般说明。

## <a name="planning-the-plugin"></a>规划插件

开始开发插件之前，请确保解决以下问题：

### <a name="supported-authentication-methods"></a>支持的身份验证方法

确定插件将支持的网络所需的身份验证方法。 热点卸载框架支持三类网络：

* 使用 WISPr 1.0 或某种变体的网络通过 HTTP 对用户和/或设备进行身份验证。 这些网络由以下功能表示：
  * **HS_FLAG_CAPABILITY_NETWORK_AUTH_HTTP**
* 使用 EAP-SIM/也称/亦 "对设备进行身份验证的网络。 这些网络由以下功能表示：
  * **HS_FLAG_CAPABILITY_NETWORK_AUTH_EAP_SIM**
  * **HS_FLAG_CAPABILITY_NETWORK_AUTH_EAP_AKA**
  * **HS_FLAG_CAPABILITY_NETWORK_AUTH_EAP_AKA_PRIME**

  对于基于 EAP 的网络，该插件还可以通过使用 **HS_FLAG_CAPABILITY_NETWORK_CUSTOM_REALM** 功能来指定自定义领域。

* 不需要任何身份验证或网络的网络，此插件具有独立的身份验证机制，无需任何设备凭据。 这些网络由以下功能表示：
  * **HS_FLAG_CAPABILITY_NETWORK_AUTH_NO_SIM**

### <a name="hidden-networks"></a>隐藏的网络

在初始化时，隐藏网络必须预先指定，因为网络在扫描结果中不可见。 由于隐藏网络的电源和隐私含义，框架最多支持一个隐藏网络。 因此，如果另一个插件还请求连接到隐藏网络，则将拒绝第二个插件的请求。 如果插件需要配置隐藏网络，则必须指定该网络的 **HS_FLAG_CAPABILITY_NETWORK_TYPE_HIDDEN** 功能。

对于所有其他网络，该插件应该指定 **HS_FLAG_CAPABILITY_NETWORK_TYPE_VISIBLE** 的功能。

### <a name="user-interface-display-strings"></a>用户界面显示字符串

插件用来与用户通信的自定义 UI 显示字符串必须存储在一个字符串表中 () .rc 文件中。 插件必须将字符串 Id 传递到热点卸载服务，以使其能够加载相应的字符串。 目前支持以下显示字符串：

* 提供程序名称 (最大 **HS_CONST_MAX_PROVIDER_NAME_LENGTH** 长度) 
* 网络名称 (最大 **HS_CONST_MAX_NETWORK_DISPLAY_NAME_LENGTH** 长度) 
* "高级" 页上的消息 (最大 **HS_CONST_MAX_ADVANCED_PAGE_STRING_LENGTH** 长度) 
* 使用 HSHostSendUserMessage 函数传递给用户的任何其他字符串 (最 **大 \_ 路径** 长度) 。 有关详细信息，请参阅 [HS_HOST_SEND_USER_MESSAGE](/previous-versions/dn789353(v=vs.85))。

**注意：** 有关 Wi-fi 热点卸载功能和常量的详细信息，请参阅 [Wi-fi 热点卸载常数](/previous-versions/mt800328(v=vs.85))。

## <a name="implementing-the-plugin"></a>实现插件

插件作为 DLL 实现。 函数 [HSPluginGetVersion](/previous-versions/dn789345(v=vs.85)) 和 [HSPluginInitPlugin](/previous-versions/dn789346(v=vs.85)) 必须在插件 DLL 的 .def 文件中指定，或者在函数实现中添加 "__declspec (dllexport) " 关键字来公开。

## <a name="initialization"></a>初始化

插件 Api 将按以下顺序在初始化时调用：

### <a name="hsplugingetversion"></a>HsPluginGetVersion

插件应返回其版本信息，以验证插件版本是否与主机设备版本匹配。 当前版本存储在常量 **HS_CONST_HOST_CURRENT_API_VERSION**中。

### <a name="hsplugininitplugin"></a>HSPluginInitPlugin

这是主初始化函数。 它为插件提供以下信息：

* 每次调用任何热点插件主机时要使用的插件的上下文句柄 ( * * HS_HOST_ \* \\ * * * ) 函数
* 主机当前使用的版本号 (**dwVerNumUsed**) 
* 有关设备的信息 (**pDeviceIdentity**) 
* 可用于插件的 OS 功能，指定为 HS_FLAG_CAPABILITY_NETWORK_ * * 类型 (**dwHostCapabilities**) 
* 插件用来回调主机 (**pHotspotHostHandlers** 的函数的处理程序) 

此插件会将以下信息返回到热点插件主机：

* 指向结构的指针，该结构包含 (**pHotspotPluginAPIs**) 的插件 api 列表。 有关详细信息，请参阅 [HOTSPOT_PLUGIN_APIS](/previous-versions/dn789344(v=vs.85))。
* 指向结构的指针，该结构包含 (**pPluginProfile**) 的插件配置文件。 有关详细信息，请参阅 [HS_PLUGIN_PROFILE](/previous-versions/dn789365(v=vs.85))。 

该配置文件包含插件所需的所有功能。 这由将适用的功能标志值与 (HS_FLAG_CAPABILITY_NETWORK_ \*) 使用按位 "或" 运算组合而得出的单个值表示。 如果插件指定了 "HS \_ 标志 \_ 功能 \_ 网络 \_ 身份验证 \_ HTTP 功能" 或 "hs \_ 标志 \_ 功能 \_ 网络 \_ 身份验证 \_ " 功能，则必须将 \_ \* **HS_PLUGIN_PROFILE**结构的**dwSupportedSIMCount**成员设置为支持的 sim 数。 此插件还必须通过设置其**HS_PLUGIN_PROFILE**结构的**dwNumNetworksSupported**成员来指定它所支持的网络总数。

### <a name="hspluginqueryhiddennetwork-optional"></a>HsPluginQueryHiddenNetwork [可选]

如果该插件指定了 **HS_FLAG_CAPABILITY_NETWORK_TYPE_HIDDEN** 功能，并且该设备可支持隐藏网络，则该功能由热点插件主机调用，以从插件获取隐藏的网络信息。 有关详细信息，请参阅 [HS_PLUGIN_QUERY_HIDDEN_NETWORK](/previous-versions/dn789367(v=vs.85))。

### <a name="hspluginquerysupportedsims-optional"></a>HsPluginQuerySupportedSIMs [可选]

如果插件为 **dwSupportedSIMCount**指定非零值，则热点插件主机会调用此函数。 调用时， **pNetworkIdentity** 参数应为 NULL，并且需要提供插件所支持的所有 sim 的列表。 以后还可以调用此函数来确定与每个热点网络关联的 Sim (此时， **pNetworkIdentity** 将为非 NULL) 。 插件必须提供支持的 Sim 列表。 有关详细信息，请参阅 [HS_PLUGIN_QUERY_SUPPORTED_SIMS](/previous-versions/dn789368(v=vs.85))。

## <a name="run-time"></a>运行时

当网络变得可见时，热点插件主机会查询每个网络的插件，以确定它是否是热点网络。

### <a name="hspluginishotspotnetwork"></a>HSPluginIsHotspotNetwork

热点插件主机调用此函数来确定指定的网络是否为热点网络。 它通过 [HS_NETWORK_IDENTITY](/previous-versions/dn789356(v=vs.85)) 结构传递有关网络 (SSID、身份验证类型、密码) 的标识信息。 插件必须返回一个指示网络类型的 [eHS_NETWORK_STATE](/previous-versions/dn756756(v=vs.85)) 枚举值。 如果是热点网络，则有关网络的信息将通过 [HS_NETWORK_PROFILE](/previous-versions/dn789357(v=vs.85)) 结构返回。 有关详细信息，请参阅 [HS_PLUGIN_IS_HOTSPOT_NETWORK](/previous-versions/dn789363(v=vs.85))。

### <a name="hspluginquerysupportedsims-optional"></a>HsPluginQuerySupportedSIMs [可选]

如果插件在调用[HS_PLUGIN_IS_HOTSPOT_NETWORK](/previous-versions/dn789363(v=vs.85))的*HS_NETWORK_PROFILE*参数中指定了 " **hs \_ 标志功能 \_ \_ 网络 \_ 身份验证 \_ HTTP** " 或 " **hs \_ 标志功能" \_ \_ 网络 \_ 身份验证 \_ EAP** ，则热点插件主机将调用此函数。 在此实例中调用时，pNetworkIdentity 参数应为非 NULL，并且插件必须为 pNetworkIdentity 中指定的网络提供支持的 Sim 列表。 有关详细信息，请参阅 [HS_PLUGIN_QUERY_SUPPORTED_SIMS](/previous-versions/dn789368(v=vs.85))。

### <a name="hspluginquerycellularexceptionhosts-optional"></a>HSPluginQueryCellularExceptionHosts [可选]

如果插件返回的[HS_NETWORK_PROFILE](/previous-versions/dn789357(v=vs.85))结构的 " **dwNumCellularExceptions** " 字段设置为非零值，则热点插件主机将调用此函数。 调用时，该插件必须返回蜂窝持有者主机的列表。 有关详细信息，请参阅 [HS_PLUGIN_QUERY_CELLULAR_EXCEPTION_HOSTS](/previous-versions/dn789366(v=vs.85))。

## <a name="connect-time"></a>连接时间

当网络被认为是可连接的，或者用户选择了网络时，将发生以下调用序列：

### <a name="hspluginpreconnectinit"></a>HSPluginPreConnectInit

热点插件主机调用此函数以通知插件正在连接到由插件返回的 [HS_NETWORK_IDENTITY](/previous-versions/dn789356(v=vs.85)) 结构中指定的热点网络。 有关详细信息，请参阅 [HS_PLUGIN_PRE_CONNECT_INIT](/previous-versions/dn789364(v=vs.85))。

### <a name="hspluginstartpostconnectauth"></a>HSPluginStartPostConnectAuth

L2 连接完成后，热点插件主机会调用此函数以通知插件启动身份验证。 从以前对**HSPluginPreConnectInit**的调用中提供了*pConnectContext*、 *pNetworkIdentity*和*pNetworkProfile* ，但也提供了*dwConnectionId*和*pSIMData*。 在调用主机的 **HSHostPostConnectAuthCompletion** 处理程序时，该插件必须存储连接 ID 并使用它来通知操作系统身份验证结果，并且如果需要向用户发送消息，则还必须在对 **HSHostSendUserMessage** 的调用中使用。 **PSIMData**结构包含有关在身份验证期间插件可能需要的 SIM 配置的附加信息。 如果该插件返回 Success，则必须在5分钟内调用 **HSHostPostConnectAuthCompletion** ，否则连接将断开。

## <a name="disconnect-and-reset"></a>断开连接并重置

当网络断开连接时，无论是由某些用户或设备操作显式断开，还是由于外部因素而隐式断开，都将调用以下函数：

### <a name="hspluginstoppostconnectauth"></a>HSPluginStopPostConnectAuth

热点插件主机调用此函数以终止网络身份验证，因为设备将要断开与网络的连接。 有关详细信息，请参阅 [HS_PLUGIN_STOP_POST_CONNECT_AUTH](/previous-versions/dn789372(v=vs.85))。

### <a name="hsplugindisconnectfromnetwork"></a>HSPluginDisconnectFromNetwork

热点插件主机调用此函数以通知插件设备将从网络断开连接。 有关详细信息，请参阅 [HS_PLUGIN_DISCONNECT_FROM_NETWORK](/previous-versions/dn789361(v=vs.85))。

### <a name="hspluginreset"></a>HSPluginReset

热点插件主机调用此函数，将插件重置为其初始 (刚刚加载) 状态。 有关详细信息，请参阅 [HS_PLUGIN_RESET](/previous-versions/dn789369(v=vs.85))。

## <a name="periodic-calls"></a>定期调用

根据插件设置的特定参数，将定期调用以下函数：

### <a name="hspluginsendkeepalive-optional"></a>HSPluginSendKeepAlive [可选]

热点插件主机按插件返回的[HS_NETWORK_PROFILE](/previous-versions/dn789357(v=vs.85))结构的 " **dwKeepAliveTimeMins** " 成员中指定的频率调用此函数。 有关详细信息，请参阅 [HS_PLUGIN_SEND_KEEP_ALIVE](/previous-versions/dn789370(v=vs.85))。

### <a name="hsplugincheckforupdates-optional"></a>HSPluginCheckForUpdates [可选]

热点插件主机按[HS_PLUGIN_PROFILE](/previous-versions/dn789365(v=vs.85))结构的**dwProfileUpdateTimeDays**成员中指定的频率调用此函数。 

## <a name="unloading-the-plugin"></a>卸载插件

### <a name="hsplugindeinit"></a>HSPluginDeinit

热点插件主机调用此函数，以使插件能够刷新任何未保存的信息并在卸载之前关闭任何打开的句柄。 将在 *UnloadReason* 参数中提供卸载的原因。 有关详细信息，请参阅 [HS_PLUGIN_DEINIT](/previous-versions/dn789360(v=vs.85))。

## <a name="plugin-installation-package"></a>插件安装包

插件安装包应包含以下内容：

### <a name="the-plugin-dll-file"></a>插件 DLL 文件

Dll 文件必须经过签名并置于**Programs\HotspotHost \\ ** < *providername*> 中，其中 <*providername*> 是 DLL 提供程序的名称。 

有关对 DLL 进行签名的信息，请参阅 [对二进制文件和包](/previous-versions/windows/hardware/code-signing/dn789217(v=vs.85))进行签名。 

对于 DLL 文件的命名没有特定的约定，因此，请确保注册表中的文件路径是正确的。 例如，可以在包中指定注册表信息，如下所示：

```xml
<RegKeys>
        <RegKey KeyName="$(hklm.software)\Microsoft\Windows Phone\HotspotOffload\Plugins\<ProviderName>">
          <RegValue Name="PluginRank" Type="REG_DWORD" Value="00000005" />
          <RegValue Name="PluginPath" Type="REG_SZ" Value="%SystemDrive%\Programs\HotspotHost\Orange\<ProviderName>\<HotspotPlugin.dll>" />
        </RegKey>
      </RegKeys>
```

### <a name="registry-configuration"></a>注册表配置

所需的注册表设置保存在创建的新条目中： **HKEY_LOCAL_MACHINE \software\microsoft\windows Phone\HotspotOffload\Plugins \\ ** *ProviderName*。

*ProviderName* 对于插件提供程序或移动运营商必须是唯一的。

以下值必须保存在注册表项下：

| 名称 | 类型 | 说明 |
| --- | --- | --- |
| PluginPath | [REG_SZ] | DLL 的名称和完整路径。 |
| PluginRank | [REG_DWORD] | 1到250之间的任何正值，均为 Microsoft) 保留 (0。 值越小，表示优先级越高。 如果两个插件具有相同的排名，则热点服务将随机设置优先级。 |

### <a name="data-files-that-contain-connection-specific-information-such-as-a-list-of-ssids-encrypted-credentials-etc-optional"></a>包含特定于连接的信息的数据文件，如 Ssid 列表、加密的凭据等。 [可选]

应将数据文件保存在：下 `Data\SharedData\HotspotHost\Plugins\<ProviderName>` 。