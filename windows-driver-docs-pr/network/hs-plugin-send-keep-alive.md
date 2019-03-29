---
title: HS_PLUGIN_SEND_KEEP_ALIVE 函数
description: 由主机发送一个网络连接保持活动状态的消息调用 HS_PLUGIN_SEND_KEEP_ALIVE 函数。 它将调用插件的 HS_PLUGIN_PROFILE 结构 dwKeepAliveTimeMins 成员中指定的频率。
ms.assetid: 1db91146-03bb-4513-9c1b-f0dbd5c941f5
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 typedef DWORD (WINAPI HS_PLUGIN_SEND_KEEP_ALIVE) 函数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bda0334afb1974b183400a7694c5b5bd21246e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565380"
---
# <a name="hspluginsendkeepalive-function"></a>HS\_插件\_发送\_保持\_ALIVE 函数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_插件\_发送\_保留\_ALIVE**函数调用由主机发送一个网络连接保持活动状态消息。 它将调用中指定的频率**dwKeepAliveTimeMins**的插件的成员[ **HS\_插件\_配置文件**](hs-plugin-profile.md)结构.

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_SEND_KEEP_ALIVE)(
    
);
```

<a name="parameters"></a>Parameters
----------

此函数没有任何参数。

**   

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


[**HS\_插件\_配置文件**](hs-plugin-profile.md)

 

 




