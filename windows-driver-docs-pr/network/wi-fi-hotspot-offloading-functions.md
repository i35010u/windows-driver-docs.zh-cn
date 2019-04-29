---
title: Wi-Fi 热点卸载函数
description: Wi-Fi 热点卸载函数
ms.assetid: 114e1604-0d9a-418c-aee1-a9b615d13d21
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7aed1acdaae9c12ad6e7f7138df44f8b30dbcdf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385919"
---
# <a name="wi-fi-hotspot-offloading-functions"></a>Wi-Fi 热点卸载函数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


本部分介绍的 Wi-fi 热点卸载 framework 函数。 这些函数简化插件的热点和热点插件宿主之间的交互。

以下函数由插件 DLL 导出。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="hsplugingetversion.md" data-raw-source="[HSPluginGetVersion](hsplugingetversion.md)">HSPluginGetVersion</a></p></td>
<td><p>此函数验证插件和主机版本匹配。</p></td>
</tr>
<tr class="even">
<td><p><a href="hsplugininitplugin.md" data-raw-source="[HSPluginInitPlugin](hsplugininitplugin.md)">HSPluginInitPlugin</a></p></td>
<td><p>要初始化该插件的宿主通过调用此函数。</p></td>
</tr>
</tbody>
</table>

 

热点插件公开以下函数通过[热点\_插件\_API](hotspot-plugin-apis.md)结构。 在初始化期间，此结构被传递给热点插件宿主。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><a href="hs-plugin-check-for-updates.md" data-raw-source="[HS_PLUGIN_CHECK_FOR_UPDATES](hs-plugin-check-for-updates.md)">HS_PLUGIN_CHECK_FOR_UPDATES</a></p></td>
<td><p>此函数会检查配置更新。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-plugin-deinit.md" data-raw-source="[HS_PLUGIN_DEINIT](hs-plugin-deinit.md)">HS_PLUGIN_DEINIT</a></p></td>
<td><p>调用此函数来通知该插件将被卸载。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-plugin-disconnect-from-network.md" data-raw-source="[HS_PLUGIN_DISCONNECT_FROM_NETWORK](hs-plugin-disconnect-from-network.md)">HS_PLUGIN_DISCONNECT_FROM_NETWORK</a></p></td>
<td><p>调用此函数将从网络断开连接设备时通知该插件。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-plugin-is-hotspot-network.md" data-raw-source="[HS_PLUGIN_IS_HOTSPOT_NETWORK](hs-plugin-is-hotspot-network.md)">HS_PLUGIN_IS_HOTSPOT_NETWORK</a></p></td>
<td><p>若要确定指定的网络是否热点网络主机调用此函数。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-plugin-pre-connect-init.md" data-raw-source="[HS_PLUGIN_PRE_CONNECT_INIT](hs-plugin-pre-connect-init.md)">HS_PLUGIN_PRE_CONNECT_INIT</a></p></td>
<td><p>此函数调用以通知其状态与热点网络的连接时初始化该插件。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-plugin-query-cellular-exception-hosts.md" data-raw-source="[HS_PLUGIN_QUERY_CELLULAR_EXCEPTION_HOSTS](hs-plugin-query-cellular-exception-hosts.md)">HS_PLUGIN_QUERY_CELLULAR_EXCEPTION_HOSTS</a></p></td>
<td><p>调用此函数来检索该插件需要作为其身份验证过程的一部分通过移动电话网络连接到的主机的列表。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-plugin-query-hidden-network.md" data-raw-source="[HS_PLUGIN_QUERY_HIDDEN_NETWORK](hs-plugin-query-hidden-network.md)">HS_PLUGIN_QUERY_HIDDEN_NETWORK</a></p></td>
<td><p>此函数返回的网络标识和隐藏网络的网络配置文件</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-plugin-reset.md" data-raw-source="[HS_PLUGIN_RESET](hs-plugin-reset.md)">HS_PLUGIN_RESET</a></p></td>
<td><p>调用此函数以重置该插件。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-plugin-send-keep-alive.md" data-raw-source="[HS_PLUGIN_SEND_KEEP_ALIVE](hs-plugin-send-keep-alive.md)">HS_PLUGIN_SEND_KEEP_ALIVE</a></p></td>
<td><p>此函数发送的网络连接保持活动状态消息。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-plugin-start-post-connect-auth.md" data-raw-source="[HS_PLUGIN_START_POST_CONNECT_AUTH](hs-plugin-start-post-connect-auth.md)">HS_PLUGIN_START_POST_CONNECT_AUTH</a></p></td>
<td><p>调用此函数来执行任何后续连接设备通过网络进行身份验证所需的身份验证。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-plugin-stop-post-connect-auth.md" data-raw-source="[HS_PLUGIN_STOP_POST_CONNECT_AUTH](hs-plugin-stop-post-connect-auth.md)">HS_PLUGIN_STOP_POST_CONNECT_AUTH</a></p></td>
<td><p>若要停止身份验证过程，调用此函数。</p></td>
</tr>
</tbody>
</table>

 

热点插件宿主公开以下函数通过[热点\_主机\_处理程序](hotspot-host-handlers.md)结构。 此结构传递给热点插件初始化过程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="hs-host-allocate-memory.md" data-raw-source="[HS_HOST_ALLOCATE_MEMORY](hs-host-allocate-memory.md)">HS_HOST_ALLOCATE_MEMORY</a></p></td>
<td><p>此函数返回由调用方指定的内存量。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-host-free-memory.md" data-raw-source="[HS_HOST_FREE_MEMORY](hs-host-free-memory.md)">HS_HOST_FREE_MEMORY</a></p></td>
<td><p>此函数将释放由调用方分配任何内存。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-host-post-connect-auth-completion.md" data-raw-source="[HS_HOST_POST_CONNECT_AUTH_COMPLETION](hs-host-post-connect-auth-completion.md)">HS_HOST_POST_CONNECT_AUTH_COMPLETION</a></p></td>
<td><p>此函数指示成功或失败的身份验证尝试。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-host-send-keep-alive-completion.md" data-raw-source="[HS_HOST_SEND_KEEP_ALIVE_COMPLETION](hs-host-send-keep-alive-completion.md)">HS_HOST_SEND_KEEP_ALIVE_COMPLETION</a></p></td>
<td><p>此函数指示成功或失败的"发送保持活动状态"请求。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-host-update-configuration-completion.md" data-raw-source="[HS_HOST_UPDATE_CONFIGURATION_COMPLETION](hs-host-update-configuration-completion.md)">HS_HOST_UPDATE_CONFIGURATION_COMPLETION</a></p></td>
<td><p>此函数指示成功或失败的"检查更新"请求。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[卸载引用的 Wi-fi 热点](wi-fi-hotspot-offloading-reference.md)  



