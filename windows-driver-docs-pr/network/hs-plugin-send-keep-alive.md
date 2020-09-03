---
title: HS_PLUGIN_SEND_KEEP_ALIVE 函数
description: 主机调用 HS_PLUGIN_SEND_KEEP_ALIVE 函数发送网络连接 keep-alive 消息。 它将以插件的 HS_PLUGIN_PROFILE 结构的 dwKeepAliveTimeMins 成员中指定的频率进行调用。
ms.assetid: 1db91146-03bb-4513-9c1b-f0dbd5c941f5
keywords:
- typedef DWORD (WINAPI HS_PLUGIN_SEND_KEEP_ALIVE 从 Windows Vista 开始) 函数网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cd2e3bca7a7a3cad2b12abfb9592e5f84413d5b
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403006"
---
# <a name="hs_plugin_send_keep_alive-function"></a>HS \_ 插件 \_ 发送 \_ \_ keep-alive 函数

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 插件 \_ 发送 \_ \_ ** keep-alive 函数由主机调用，以发送网络连接 keep-alive 消息。 它将以插件的[**HS \_ 插件 \_ 配置文件**](hs-plugin-profile.md)结构的**dwKeepAliveTimeMins**成员中指定的频率进行调用。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_SEND_KEEP_ALIVE)(
    
);
```

<a name="parameters"></a>参数
----------

此函数没有参数。

**   

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


[**HS \_ 插件 \_ 配置文件**](hs-plugin-profile.md)

 

 




