---
title: HS_PLUGIN_RESET 函数
description: HS_PLUGIN_RESET 函数称为主机来通知该插件，它必须重置其状态。
ms.assetid: 9f5683c9-b426-4802-85bd-c1ce770b9e46
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 typedef DWORD (WINAPI HS_PLUGIN_RESET) 函数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27795a01e46b0ee81ef0ef6554c14beec4080acc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322170"
---
# <a name="hspluginreset-function"></a>HS\_插件\_RESET 函数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_插件\_重置**宿主通知该插件，它必须重置其状态调用函数。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_RESET)(
    
);
```

<a name="parameters"></a>Parameters
----------

此函数没有任何参数。

**   

<a name="return-value"></a>返回值
------------

此函数调用由宿主与插件进行通信，并不会返回一个值。

<a name="remarks"></a>备注
-------

该插件应终止所有线程，停止正在进行中的任何活动。

它将无法重置时，可以卸载该插件。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>Windows 10 移动版</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Hotspotoffloadplugin.h （包括 Hotspotoffloadplugin.h）</td>
</tr>
</tbody>
</table>

 

 




