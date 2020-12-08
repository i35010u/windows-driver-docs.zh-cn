---
title: HS_PLUGIN_DISCONNECT_FROM_NETWORK 函数
description: HS_PLUGIN_DISCONNECT_FROM_NETWORK 函数通知插件设备将从网络断开连接。
keywords:
- typedef DWORD (WINAPI HS_PLUGIN_DISCONNECT_FROM_NETWORK 从 Windows Vista 开始) 函数网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbad7bd0ac65d0a43199988e039f7b6d6abeab6f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825099"
---
# <a name="hs_plugin_disconnect_from_network-function"></a>HS \_ 插件 \_ \_ 从 \_ 网络功能断开连接

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 插件 \_ \_ 从 \_ 网络功能断开连接** 将通知插件设备将从网络断开连接。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_DISCONNECT_FROM_NETWORK)(
  _In_ HS_NETWORK_IDENTITY *pNetworkIdentity
);
```

<a name="parameters"></a>参数
----------

*\* pNetworkIdentity* \[\]  
一个指针，指向要从中断开设备连接的网络的 [**HS \_ 网络 \_ 标识**](hs-network-identity.md) 结构。

<a name="return-value"></a>返回值
------------

宿主调用此函数以与插件通信，而不返回值。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>Windows 10 移动版</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Hotspotoffloadplugin (包含 Hotspotoffloadplugin) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**HS \_ 网络 \_ 标识**](hs-network-identity.md)

 

 




