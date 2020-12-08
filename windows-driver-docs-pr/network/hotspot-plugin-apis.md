---
title: HOTSPOT_PLUGIN_APIS 结构
description: HOTSPOT_PLUGIN_APIS 结构包含热点插件 Api 函数表。
keywords:
- 从 Windows Vista 开始 HOTSPOT_PLUGIN_APIS 结构网络驱动程序
- 从 Windows Vista 开始 PHOTSPOT_PLUGIN_APIS 结构指针网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa38ed5c5f4ae954a1ec710f47238f5eefc61cb5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836349"
---
# <a name="hotspot_plugin_apis-structure"></a>热点 \_ 插件 \_ api 结构

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**作用点 \_ 插件 \_ Api** 结构包含热点插件 api 函数表。 调用 [**HSPluginInitPlugin**](hsplugininitplugin.md) 来初始化插件时，插件会返回此函数表。 该表包含热点主机调用以与插件通信的函数。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _HOTSPOT_PLUGIN_APIS {
  HS_PLUGIN_QUERY_SUPPORTED_SIMS     HSPluginQuerySupportedSIMs;
  HS_PLUGIN_QUERY_HIDDEN_NETWORK     HSPluginQueryCellularExceptionHosts;
  HS_PLUGIN_IS_HOTSPOT_NETWORK       HSPluginIsHotspotNetwork;
  HS_PLUGIN_PRE_CONNECT_INIT         HSPluginPreConnectInit;
  HS_PLUGIN_START_POST_CONNECT_AUTH  HSPluginStartPostConnectAuth;
  HS_PLUGIN_STOP_POST_CONNECT_AUTH   HSPluginStopPostConnectAuth;
  HS_PLUGIN_DISCONNECT_FROM_NETWORK  HSPluginDisconnectFromNetwork;
  HS_PLUGIN_RESET                    HSPluginReset;
  HS_PLUGIN_SEND_KEEP_ALIVE          HSPluginSendKeepAlive;
  HS_PLUGIN_CHECK_FOR_UPDATES        HSPluginCheckForUpdates;
  HS_PLUGIN_DEINIT                   HSPluginDeinit;
} HOTSPOT_PLUGIN_APIS, *PHOTSPOT_PLUGIN_APIS;
```

<a name="members"></a>成员
-------

**HSPluginQuerySupportedSIMs**  
在插件初始化过程中调用 API。

由热点主机调用以检索插件支持的 Sim 列表。 可调用此方法来检索受支持的 Sim 的完整列表，或仅检索特定网络的 Sim。 有关详细信息，请参阅 [**HS \_ 插件 \_ 查询支持的 \_ \_ sim**](hs-plugin-query-supported-sims.md)。

**HSPluginQueryCellularExceptionHosts**  
在插件初始化过程中调用 API。

如果插件已通过 [**hs \_ 插件 \_ 配置文件**](hs-plugin-profile.md)结构指定了 **hs \_ 标志 \_ 功能 \_ 网络 \_ 类型 \_ 隐藏** 功能，则由该热点主机调用。 有关详细信息，请参阅 [**HS \_ 插件 \_ 查询 \_ 隐藏 \_ 网络**](hs-plugin-query-hidden-network.md)。

**HSPluginIsHotspotNetwork**  
处理扫描结果时调用了 API。

由热点主机调用，以请求该插件识别传入 *pHiddenNetworkIdentity* 参数的网络是否是热点网络。 有关详细信息，请参阅 [**HS \_ 插件 \_ 是 \_ 热点 \_ 网络**](hs-plugin-is-hotspot-network.md)。

**HSPluginPreConnectInit**  
连接-进程 API。

由热点主机调用，用于通知插件在连接正在进行时初始化其状态。 有关详细信息，请 [**参阅 \_ HS \_ 插件 \_ CONNECT \_ INIT**](hs-plugin-pre-connect-init.md)。

**HSPluginStartPostConnectAuth**  
连接-进程 API。

由热点主机调用，请求该插件执行任何要求的连接后身份验证，以通过网络对设备进行身份验证。 有关详细信息，请 [**参阅 \_ HS \_ 插件 \_ 启动 \_ 连接 \_ 身份验证**](hs-plugin-start-post-connect-auth.md)。

**HSPluginStopPostConnectAuth**  
连接-进程 API。

由热点主机调用以通知插件停止身份验证过程。 有关详细信息，请参阅 [**HS \_ 插件 \_ 停止 \_ 后 \_ 连接 \_ 身份验证**](hs-plugin-stop-post-connect-auth.md)。

**HSPluginDisconnectFromNetwork**  
连接-进程 API。

由热点主机调用以通知插件与网络断开连接。 有关详细信息，请 [**参阅 \_ HS \_ 插件 \_ 从 \_ 网络断开连接**](hs-plugin-disconnect-from-network.md)。

**HSPluginReset**  
用于重置插件的 API。 如果在从此调用返回之前，该插件不会释放任何挂起的调用，则将卸载该插件。

由热点主机调用以重置插件。 有关详细信息，请参阅 [**HS \_ 插件 \_ RESET**](hs-plugin-reset.md)。

**HSPluginSendKeepAlive**  
用于进行定期更新的插件 API。

由热点主机调用，以将 keep-alive 消息发送到插件。 有关详细信息，请参阅 [**HS \_ 插件 \_ 发送 \_ 保持 \_ 活动状态**](hs-plugin-send-keep-alive.md)。

**HSPluginCheckForUpdates**  
用于进行定期更新的插件 API。

由热点主机调用以检查更新。 有关详细信息，请 [**参阅 \_ HS \_ 插件 \_ 检查 \_ 更新**](hs-plugin-check-for-updates.md)。

**HSPluginDeinit**  
在卸载之前调用 API 来取消初始化和清理插件。

由热点主机调用，通知插件即将卸载它。 有关详细信息，请参阅 [**HS \_ 插件 \_ DEINIT**](hs-plugin-deinit.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Hotspotoffloadplugin (包含 Hotspotoffloadplugin) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**HSPluginInitPlugin**](hsplugininitplugin.md)

[**HS \_ 插件 \_ 查询 \_ 支持的 \_ SIM**](hs-plugin-query-supported-sims.md)

[**HS \_ 插件 \_ 配置文件**](hs-plugin-profile.md)

[**HS \_ 插件 \_ 查询 \_ 隐藏 \_ 网络**](hs-plugin-query-hidden-network.md)

[**HS \_ 插件 \_ 是 \_ 热点 \_ 网络**](hs-plugin-is-hotspot-network.md)

[**HS \_ 插件 \_ 预先 \_ 连接 \_ 初始化**](hs-plugin-pre-connect-init.md)

[**HS \_ 插件 \_ 启动 \_ 后 \_ 连接 \_ 身份验证**](hs-plugin-start-post-connect-auth.md)

[**HS \_ 插件 \_ 停止 \_ 后 \_ 连接 \_ 身份验证**](hs-plugin-stop-post-connect-auth.md)

[**HS \_ 插件 \_ \_ 从 \_ 网络断开连接**](hs-plugin-disconnect-from-network.md)

[**HS \_ 插件 \_ 重置**](hs-plugin-reset.md)

[**HS \_ 插件 \_ 发送 \_ 保持 \_ 活动状态**](hs-plugin-send-keep-alive.md)

[**HS \_ 插件 \_ 检查 \_ \_ 更新**](hs-plugin-check-for-updates.md)

[**HS \_ 插件 \_ DEINIT**](hs-plugin-deinit.md)

 

 




