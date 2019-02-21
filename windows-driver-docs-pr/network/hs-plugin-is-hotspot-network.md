---
title: HS_PLUGIN_IS_HOTSPOT_NETWORK 函数
description: 由主机以确定指定的网络是否热点网络调用 HS_PLUGIN_IS_HOTSPOT_NETWORK 函数。
ms.assetid: 24a26ee0-9eb1-49fa-95da-40315a4aab3a
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 typedef DWORD (WINAPI HS_PLUGIN_IS_HOTSPOT_NETWORK) 函数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52bd0fefd29dc2aafeba7c3484f7fab6237da18b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540440"
---
# <a name="hspluginishotspotnetwork-function"></a>HS\_插件\_IS\_热点\_网络函数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_插件\_IS\_热点\_网络**主机以确定指定的网络是否热点网络调用函数。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_IS_HOTSPOT_NETWORK)(
  _In_      HS_NETWORK_IDENTITY *pNetworkIdentity,
  _Out_     eHS_NETWORK_STATE   *pNetworkState,
  _Out_opt_ HS_NETWORK_PROFILE  *pNetworkProfile
);
```

<a name="parameters"></a>参数
----------

*\*pNetworkIdentity* \[in\]  
指向[ **HS\_网络\_标识**](hs-network-identity.md)要断开连接设备的网络的结构。

*\*pNetworkState* \[out\]  
[ **EHS\_网络\_状态**](ehs-network-state.md)枚举值，该值指示网络的类型。

*\*pNetworkProfile* \[out, optional\]  
指向[ **HS\_网络\_配置文件**](hs-network-profile.md)网络的结构。

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

[**eHS\_NETWORK\_STATE**](ehs-network-state.md)

[**HS\_NETWORK\_PROFILE**](hs-network-profile.md)

 

 




