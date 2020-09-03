---
title: HS_PLUGIN_DISCONNECT_FROM_NETWORK 函数
description: HS_PLUGIN_DISCONNECT_FROM_NETWORK 函数通知插件设备将从网络断开连接。
ms.assetid: 8a53c824-18f7-4000-b264-fe852595a9e3
keywords:
- typedef DWORD (WINAPI HS_PLUGIN_DISCONNECT_FROM_NETWORK 从 Windows Vista 开始) 函数网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94199962b45d416a500e13ec334d1f96ba6e0d85
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403044"
---
# <a name="hs_plugin_disconnect_from_network-function"></a>HS \_ 插件 \_ \_ 从 \_ 网络功能断开连接

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 插件 \_ \_ 从 \_ 网络功能断开连接**将通知插件设备将从网络断开连接。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_DISCONNECT_FROM_NETWORK)(
  _In_ HS_NETWORK_IDENTITY *pNetworkIdentity
);
```

<a name="parameters"></a>参数
----------

* \* pNetworkIdentity* \[\]  
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
<td><p>Header</p></td>
<td>Hotspotoffloadplugin (包含 Hotspotoffloadplugin) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**HS \_ 网络 \_ 标识**](hs-network-identity.md)

 

 




