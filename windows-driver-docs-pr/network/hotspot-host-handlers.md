---
title: HOTSPOT_HOST_HANDLERS 结构
description: HOTSPOT_HOST_HANDLERS 结构包含热点主机处理程序函数表。
ms.assetid: b381e471-7713-401a-b3fa-eae1801b0e81
keywords:
- 从 Windows Vista 开始 HOTSPOT_HOST_HANDLERS 结构网络驱动程序
- 从 Windows Vista 开始 PHOTSPOT_HOST_HANDLERS 结构指针网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 189e9a8b51fb3cc6a14547019be8f8a62f63e1b3
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403126"
---
# <a name="hotspot_host_handlers-structure"></a>热点 \_ 主机 \_ 处理程序结构

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**热点 \_ 主机 \_ 处理程序**结构包含热点主机处理程序函数表。 调用 [**HSPluginInitPlugin**](hsplugininitplugin.md) 时，会将此函数表传递给插件。 该表包含插件调用的、用于与热点主机通信的函数。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _HOTSPOT_HOST_HANDLERS {
  HS_HOST_ALLOCATE_MEMORY                          HSHostAllocateMemory;
  HS_HOST_FREE_MEMORY                              HSHostFreeMemory;
  HS_HOST_POST_CONNECT_AUTH_COMPLETION             HSHostPostConnectAuthCompletion;
  HS_HOST_SEND_KEEP_ALIVE_COMPLETION               HSHostSendKeepAliveCompletion;
  HS_HOST_UPDATE_CONFIGURATION_COMPLETION          HSHostUpdateConfigurationCompletion;
  HS_HOST_SEND_USER_MESSAGE                        HSHostSendUserMessage;
} HOTSPOT_HOST_HANDLERS, *PHOTSPOT_HOST_HANDLERS;
```

<a name="members"></a>成员
-------

**HSHostAllocateMemory**  
可选内存管理处理程序。

由插件调用的函数的句柄，用于分配插件所需的任何内存。 有关详细信息，请参阅 [**HS \_ 主机 \_ 分配 \_ 内存**](hs-host-allocate-memory.md)。

**HSHostFreeMemory**  
可选内存管理处理程序。

由插件调用的函数的句柄，用于释放以前通过调用 [**HS \_ 主机 \_ 分配 \_ 内存**](hs-host-allocate-memory.md)分配的任何内存。 有关详细信息，请参阅 [**HS \_ 主机 \_ 可用 \_ 内存**](hs-host-free-memory.md)。

**HSHostPostConnectAuthCompletion**  
必需的连接-进程处理程序。

由插件调用的函数的句柄，用于指示在第2层 Wi-fi 连接设置后的身份验证尝试所导致的成功或失败状态。 有关详细信息，请 [**参阅 \_ HS \_ 插件 \_ 启动 \_ 连接 \_ 身份验证**](hs-plugin-start-post-connect-auth.md)。

**HSHostSendKeepAliveCompletion**  
可选的定期请求。

由插件调用的函数的句柄，用于指示 Send Keep-alive 请求导致的成功或失败状态。 有关详细信息，请参阅 [**HS \_ 插件 \_ 发送 \_ 保持 \_ 活动状态**](hs-plugin-send-keep-alive.md)。

**HSHostUpdateConfigurationCompletion**  
可选的定期请求。

由插件调用的函数的句柄，用于指示对检查更新的调用是成功还是失败。 有关详细信息，请 [**参阅 \_ HS \_ 插件 \_ 检查 \_ 更新**](hs-plugin-check-for-updates.md)。

**HSHostSendUserMessage**  
可选的定期请求。

用于与用户进行通信的调用函数的句柄。 有关详细信息，请参阅 [**HS \_ 主机 \_ 发送 \_ 用户 \_ 消息**](hs-host-send-user-message.md)。

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
<td>Hotspotoffloadplugin (包含 Hotspotoffloadplugin) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**HSPluginInitPlugin**](hsplugininitplugin.md)

[**HS \_ 主机 \_ 分配 \_ 内存**](hs-host-allocate-memory.md)

[**HS \_ 主机 \_ 可用 \_ 内存**](hs-host-free-memory.md)

[**HS \_ 插件 \_ 启动 \_ 后 \_ 连接 \_ 身份验证**](hs-plugin-start-post-connect-auth.md)

[**HS \_ 插件 \_ 发送 \_ 保持 \_ 活动状态**](hs-plugin-send-keep-alive.md)

[**HS \_ 插件 \_ 检查 \_ \_ 更新**](hs-plugin-check-for-updates.md)

[**HS \_ 主机 \_ 发送 \_ 用户 \_ 消息**](hs-host-send-user-message.md)

 

 




