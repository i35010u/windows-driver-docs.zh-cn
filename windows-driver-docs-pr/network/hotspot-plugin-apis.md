---
title: HOTSPOT_PLUGIN_APIS 结构
description: HOTSPOT_PLUGIN_APIS 结构包含热点插件 Api 函数表。
ms.assetid: eee56f84-2c7f-4218-b7ec-b4fc0181d767
keywords:
- HOTSPOT_PLUGIN_APIS 结构与 Windows Vista 一起启动的网络驱动程序
- PHOTSPOT_PLUGIN_APIS 结构指针与 Windows Vista 一起启动的网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fdf2e93ad7904b221b5eb714fb92230329caa28
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349681"
---
# <a name="hotspotpluginapis-structure"></a>热点\_插件\_API 结构

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**热点\_插件\_API**结构包含热点插件 Api 函数表。 此函数表返回由插件时[ **HSPluginInitPlugin** ](hsplugininitplugin.md)调用以初始化该插件。 该表包含函数调用的热点宿主与插件进行通信。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _HOTSPOT_PLUGIN_APIS {
  HS_PLUGIN_QUERY_SUPPORTED_SIMS     HSPluginQuerySupportedSIMs;
  HS_PLUGIN_QUERY_HIDDEN_NETWORK     HSPluginQueryCellularExceptionHosts;
  HS_PLUGIN_IS_HOTSPOT_NETWORK       HSPluginIsHotspotNetwork;
  HS_PLUGIN_PRE_CONNECT_INIT         HSPluginPreConnectInit;
  HS_PLUGIN_START_POST_CONNECT_AUTH  HSPluginStartPostConnectAuth;
  HS_PLUGIN_STOP_POST_CONNECT_AUTH   HSPluginStopPostConnectAuth;
  HS_PLUGIN_DISCONNECT_FROM_NETWORK  HSPluginDisconnectFromNetwork;
  HS_PLUGIN_RESET                    HSPluginReset;
  HS_PLUGIN_SEND_KEEP_ALIVE          HSPluginSendKeepAlive;
  HS_PLUGIN_CHECK_FOR_UPDATES        HSPluginCheckForUpdates;
  HS_PLUGIN_DEINIT                   HSPluginDeinit;
} HOTSPOT_PLUGIN_APIS, *PHOTSPOT_PLUGIN_APIS;
```

<a name="members"></a>成员
-------

**HSPluginQuerySupportedSIMs**  
在插件初始化过程中调用 API。

调用由热点宿主来检索该插件支持的 Sim 的列表。 它可以调用以检索支持的 SIMs 或只是为特定网络 Sim 的完整列表。 有关详细信息，请参阅[ **HS\_插件\_查询\_支持\_SIMS**](hs-plugin-query-supported-sims.md)。

**HSPluginQueryCellularExceptionHosts**  
在插件初始化过程中调用 API。

如果指定该插件，则调用的热点主机**HS\_标志\_功能\_网络\_类型\_HIDDEN**功能通过[**HS\_插件\_配置文件**](hs-plugin-profile.md)结构。 有关详细信息，请参阅[ **HS\_插件\_查询\_HIDDEN\_网络**](hs-plugin-query-hidden-network.md)。

**HSPluginIsHotspotNetwork**  
处理扫描结果时，API 调用。

调用的热点主机以请求插件来识别是否有网络传入*pHiddenNetworkIdentity*参数是热点网络。 有关详细信息，请参阅[ **HS\_插件\_IS\_热点\_网络**](hs-plugin-is-hotspot-network.md)。

**HSPluginPreConnectInit**  
连接过程的 API。

由热点主机以通知的插件，其状态初始化连接时调用。 有关详细信息，请参阅[ **HS\_插件\_PRE\_CONNECT\_INIT**](hs-plugin-pre-connect-init.md)。

**HSPluginStartPostConnectAuth**  
连接过程的 API。

名为热点主机以请求插件以执行任何连接后通过网络设备进行身份验证所需的身份验证。 有关详细信息，请参阅[ **HS\_插件\_启动\_POST\_CONNECT\_身份验证**](hs-plugin-start-post-connect-auth.md)。

**HSPluginStopPostConnectAuth**  
连接过程的 API。

由热点主机以通知插件以停止身份验证过程调用。 有关详细信息，请参阅[ **HS\_插件\_停止\_POST\_CONNECT\_身份验证**](hs-plugin-stop-post-connect-auth.md)。

**HSPluginDisconnectFromNetwork**  
连接过程的 API。

调用由热点宿主以通知从网络断开连接的插件。 有关详细信息，请参阅[ **HS\_插件\_断开连接\_FROM\_网络**](hs-plugin-disconnect-from-network.md)。

**HSPluginReset**  
若要重置该插件的 API。 如果该插件不会从此调用返回前释放任何挂起的调用，该插件将被卸载。

由要重置该插件的热点主机调用。 有关详细信息，请参阅[ **HS\_插件\_重置**](hs-plugin-reset.md)。

**HSPluginSendKeepAlive**  
执行定期更新插件的 API。

调用由热点主机将保持活动状态的消息发送到该插件。 有关详细信息，请参阅[ **HS\_插件\_发送\_保留\_ALIVE**](hs-plugin-send-keep-alive.md)。

**HSPluginCheckForUpdates**  
执行定期更新插件的 API。

要检查有更新的热点主机由调用。 有关详细信息，请参阅[ **HS\_插件\_检查\_有关\_更新**](hs-plugin-check-for-updates.md)。

**HSPluginDeinit**  
API 调用以取消初始化和清理在卸载之前该插件。

调用由热点宿主以通知它是即将卸载该插件。 有关详细信息，请参阅[ **HS\_插件\_DEINIT**](hs-plugin-deinit.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Hotspotoffloadplugin.h （包括 Hotspotoffloadplugin.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**HSPluginInitPlugin**](hsplugininitplugin.md)

[**HS\_插件\_查询\_支持\_SIMS**](hs-plugin-query-supported-sims.md)

[**HS\_插件\_配置文件**](hs-plugin-profile.md)

[**HS\_插件\_查询\_HIDDEN\_网络**](hs-plugin-query-hidden-network.md)

[**HS\_插件\_IS\_热点\_网络**](hs-plugin-is-hotspot-network.md)

[**HS\_插件\_PRE\_CONNECT\_INIT**](hs-plugin-pre-connect-init.md)

[**HS\_PLUGIN\_START\_POST\_CONNECT\_AUTH**](hs-plugin-start-post-connect-auth.md)

[**HS\_插件\_停止\_POST\_CONNECT\_身份验证**](hs-plugin-stop-post-connect-auth.md)

[**HS\_PLUGIN\_DISCONNECT\_FROM\_NETWORK**](hs-plugin-disconnect-from-network.md)

[**HS\_插件\_重置**](hs-plugin-reset.md)

[**HS\_PLUGIN\_SEND\_KEEP\_ALIVE**](hs-plugin-send-keep-alive.md)

[**HS\_插件\_检查\_为\_更新**](hs-plugin-check-for-updates.md)

[**HS\_PLUGIN\_DEINIT**](hs-plugin-deinit.md)

 

 




