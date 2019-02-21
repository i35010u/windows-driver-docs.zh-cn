---
title: HS_PLUGIN_PRE_CONNECT_INIT 函数
description: HS_PLUGIN_PRE_CONNECT_INIT 函数调用以通知其状态与热点网络的连接时初始化该插件。
ms.assetid: 799242a0-144f-4d3f-b48c-9e96a851d8c4
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 typedef DWORD (WINAPI HS_PLUGIN_PRE_CONNECT_INIT) 函数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: a949921041a364e0f7f95f1f9558038d49c79816
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523915"
---
# <a name="hspluginpreconnectinit-function"></a>HS\_插件\_PRE\_CONNECT\_INIT 函数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_插件\_PRE\_CONNECT\_INIT**函数调用以通知其状态与热点网络的连接时初始化该插件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_PRE_CONNECT_INIT)(
  _In_ HS_NETWORK_IDENTITY *pNetworkIdentity
);
```

<a name="parameters"></a>参数
----------

*\*pNetworkIdentity* \[in\]  
指向[ **HS\_网络\_标识**](hs-network-identity.md)结构为目标网络。

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
<td><p>标头</p></td>
<td>Hotspotoffloadplugin.h （包括 Hotspotoffloadplugin.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**HS\_NETWORK\_IDENTITY**](hs-network-identity.md)

 

 




