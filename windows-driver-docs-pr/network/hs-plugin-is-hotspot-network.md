---
title: HS_PLUGIN_IS_HOTSPOT_NETWORK 函数
description: 主机调用 HS_PLUGIN_IS_HOTSPOT_NETWORK 函数来确定指定的网络是否是热点网络。
ms.assetid: 24a26ee0-9eb1-49fa-95da-40315a4aab3a
keywords:
- typedef DWORD (WINAPI HS_PLUGIN_IS_HOTSPOT_NETWORK 从 Windows Vista 开始) 函数网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9685f2f90aa08e519e09d31d6880771760b4e8c1
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403030"
---
# <a name="hs_plugin_is_hotspot_network-function"></a>HS \_ 插件 \_ 是 \_ 热点 \_ 网络功能

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 插件 \_ 为 \_ 热点 \_ 网络**函数由主机调用，用于确定指定的网络是否为热点网络。

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

* \* pNetworkIdentity* \[\]  
一个指针，指向要从中断开设备连接的网络的 [**HS \_ 网络 \_ 标识**](hs-network-identity.md) 结构。

* \* pNetworkState* \[\]  
指示网络类型的 [**eHS \_ 网络 \_ 状态**](ehs-network-state.md) 枚举值。

* \* pNetworkProfile* \[ out，可选\]  
指向网络的 [**HS \_ 网络 \_ 配置文件**](hs-network-profile.md) 结构的指针。

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

[**eHS \_ 网络 \_ 状态**](ehs-network-state.md)

[**HS \_ 网络 \_ 配置文件**](hs-network-profile.md)

 

 




