---
title: HS_PLUGIN_DISCONNECT_FROM_NETWORK 函数
description: HS_PLUGIN_DISCONNECT_FROM_NETWORK 函数会通知该插件的设备将从网络断开连接。
ms.assetid: 8a53c824-18f7-4000-b264-fe852595a9e3
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 typedef DWORD (WINAPI HS_PLUGIN_DISCONNECT_FROM_NETWORK) 函数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c1b260fb81ccb0fd5590aa5022988dbf32e38f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575236"
---
# <a name="hsplugindisconnectfromnetwork-function"></a>HS\_插件\_断开连接\_FROM\_网络函数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_插件\_断开连接\_FROM\_网络**函数会通知该插件的设备将从网络断开连接。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_DISCONNECT_FROM_NETWORK)(
  _In_ HS_NETWORK_IDENTITY *pNetworkIdentity
);
```

<a name="parameters"></a>Parameters
----------

*\*pNetworkIdentity* \[in\]  
指向[ **HS\_网络\_标识**](hs-network-identity.md)要断开连接设备的网络的结构。

<a name="return-value"></a>返回值
------------

此函数调用由宿主与插件进行通信，并不会返回一个值。

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
<td>Hotspotoffloadplugin.h （包括 Hotspotoffloadplugin.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**HS\_NETWORK\_IDENTITY**](hs-network-identity.md)

 

 




