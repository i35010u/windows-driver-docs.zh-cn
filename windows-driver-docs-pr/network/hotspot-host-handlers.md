---
title: HOTSPOT_HOST_HANDLERS 结构
description: HOTSPOT_HOST_HANDLERS 结构包含热点主机处理程序函数表。
ms.assetid: b381e471-7713-401a-b3fa-eae1801b0e81
keywords:
- HOTSPOT_HOST_HANDLERS 结构与 Windows Vista 一起启动的网络驱动程序
- PHOTSPOT_HOST_HANDLERS 结构指针与 Windows Vista 一起启动的网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fceb6db6fb58d26326ffa84bdd5140fbe985901
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525120"
---
# <a name="hotspothosthandlers-structure"></a>热点\_主机\_处理程序结构

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**热点\_主机\_处理程序**结构包含热点主机处理程序函数表。 此函数表传递给插件时[ **HSPluginInitPlugin** ](hsplugininitplugin.md)调用以对其进行初始化。 该表包含函数调用的插件与热点主机进行通信。

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
可选的内存管理处理程序。

插件以分配所需插件的任何内存由调用的函数的句柄。 有关详细信息，请参阅[ **HS\_主机\_分配\_内存**](hs-host-allocate-memory.md)。

**HSHostFreeMemory**  
可选的内存管理处理程序。

句柄的插件来释放已分配任何内存由调用该函数通过调用早期[ **HS\_主机\_分配\_内存**](hs-host-allocate-memory.md)。 有关详细信息，请参阅[ **HS\_主机\_免费\_内存**](hs-host-free-memory.md)。

**HSHostPostConnectAuthCompletion**  
所需的连接过程处理程序。

函数调用的插件，以指示成功或失败状态导致的身份验证尝试遵循在第 2 层设置的 Wi-fi 连接的句柄。 有关详细信息，请参阅[ **HS\_插件\_启动\_POST\_CONNECT\_身份验证**](hs-plugin-start-post-connect-auth.md)。

**HSHostSendKeepAliveCompletion**  
可选的定期请求。

函数调用的插件，以指示由该发送保持活动状态的请求生成的成功或失败状态的句柄。 有关详细信息，请参阅[ **HS\_插件\_发送\_保留\_ALIVE**](hs-plugin-send-keep-alive.md)。

**HSHostUpdateConfigurationCompletion**  
可选的定期请求。

函数调用的插件，以指示成功或失败的调用以检查有更新的句柄。 有关详细信息，请参阅[ **HS\_插件\_检查\_有关\_更新**](hs-plugin-check-for-updates.md)。

**HSHostSendUserMessage**  
可选的定期请求。

调用与用户进行通信的函数的句柄。 有关详细信息请参阅[ **HS\_主机\_发送\_用户\_消息**](hs-host-send-user-message.md)。

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
<td>Hotspotoffloadplugin.h （包括 Hotspotoffloadplugin.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**HSPluginInitPlugin**](hsplugininitplugin.md)

[**HS\_主机\_分配\_内存**](hs-host-allocate-memory.md)

[**HS\_主机\_免费\_内存**](hs-host-free-memory.md)

[**HS\_PLUGIN\_START\_POST\_CONNECT\_AUTH**](hs-plugin-start-post-connect-auth.md)

[**HS\_PLUGIN\_SEND\_KEEP\_ALIVE**](hs-plugin-send-keep-alive.md)

[**HS\_插件\_检查\_为\_更新**](hs-plugin-check-for-updates.md)

[**HS\_主机\_发送\_用户\_消息**](hs-host-send-user-message.md)

 

 




