---
title: HS_PLUGIN_PRE_CONNECT_INIT 函数
description: 调用 HS_PLUGIN_PRE_CONNECT_INIT 函数以通知插件在连接到热点网络时初始化其状态。
ms.assetid: 799242a0-144f-4d3f-b48c-9e96a851d8c4
keywords:
- typedef DWORD (WINAPI HS_PLUGIN_PRE_CONNECT_INIT 从 Windows Vista 开始) 函数网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7eb6c551ec078bdb033e9a8e5fdab8a627ba36f
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403028"
---
# <a name="hs_plugin_pre_connect_init-function"></a>HS \_ 插件 \_ \_ CONNECT \_ INIT 函数

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


在连接到热点网络时，将调用 **HS \_ 插件 \_ \_ CONNECT \_ INIT** 函数来通知插件初始化其状态。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_PRE_CONNECT_INIT)(
  _In_ HS_NETWORK_IDENTITY *pNetworkIdentity
);
```

<a name="parameters"></a>参数
----------

* \* pNetworkIdentity* \[\]  
指向目标网络的 [**HS \_ 网络 \_ 标识**](hs-network-identity.md) 结构的指针。

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

 

 




