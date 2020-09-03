---
title: HS_PLUGIN_RESET 函数
description: 主机调用 HS_PLUGIN_RESET 函数，通知插件必须重置其状态。
ms.assetid: 9f5683c9-b426-4802-85bd-c1ce770b9e46
keywords:
- typedef DWORD (WINAPI HS_PLUGIN_RESET 从 Windows Vista 开始) 函数网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: eaf92ee04458e3f446fcfbea476190100e250d66
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403008"
---
# <a name="hs_plugin_reset-function"></a>HS \_ 插件 \_ RESET 函数

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


主机调用的 **HS \_ 插件 \_ RESET** 函数通知插件必须重置其状态。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_RESET)(
    
);
```

<a name="parameters"></a>参数
----------

此函数没有参数。

**   

<a name="return-value"></a>返回值
------------

宿主调用此函数以与插件通信，而不返回值。

<a name="remarks"></a>备注
-------

插件应终止所有线程，并停止正在进行的任何活动。

如果插件未能重置，则将其卸载。

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

 

 




