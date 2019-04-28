---
title: HS_HOST_SEND_KEEP_ALIVE_COMPLETION 函数
description: HS_HOST_SEND_KEEP_ALIVE_COMPLETION 函数指示成功或失败的网络发送保持活动状态消息的请求。
ms.assetid: 19fc1210-2c3a-46ca-96fb-dccafa9e9eef
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 typedef DWORD (WINAPI HS_HOST_SEND_KEEP_ALIVE_COMPLETION) 函数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1d73877e83584b147e1159ef5b025a5dc1ed623
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349654"
---
# <a name="hshostsendkeepalivecompletion-function"></a>HS\_主机\_发送\_保持\_ALIVE\_完成函数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_主机\_发送\_保留\_ALIVE\_完成**函数指示成功或失败的网络发送保持活动状态消息的请求。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_HOST_SEND_KEEP_ALIVE_COMPLETION)(
  _In_ HANDLE hPluginContext,
  _In_ DWORD  dwResult
);
```

<a name="parameters"></a>Parameters
----------

*hPluginContext* \[in\]  
此函数在调用插件的上下文句柄。

*dwResult* \[中\]  
结果代码。

<a name="return-value"></a>返回值
------------

此函数调用由插件与主机通信，并不会返回一个值。

<a name="remarks"></a>备注
-------

该插件必须调用此函数来通知以前调用的结果的宿主[ **HS\_插件\_发送\_保留\_ALIVE**](hs-plugin-send-keep-alive.md)。

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

## <a name="see-also"></a>请参阅


[**HS\_PLUGIN\_SEND\_KEEP\_ALIVE**](hs-plugin-send-keep-alive.md)

 

 




