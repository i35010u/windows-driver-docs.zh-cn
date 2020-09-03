---
title: HS_HOST_SEND_KEEP_ALIVE_COMPLETION 函数
description: HS_HOST_SEND_KEEP_ALIVE_COMPLETION 函数指示网络请求的成功或失败情况发送 keep-alive 消息。
ms.assetid: 19fc1210-2c3a-46ca-96fb-dccafa9e9eef
keywords:
- typedef DWORD (WINAPI HS_HOST_SEND_KEEP_ALIVE_COMPLETION 从 Windows Vista 开始) 函数网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 620d37d2556518131d87f887de1326e46a8a4b94
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403092"
---
# <a name="hs_host_send_keep_alive_completion-function"></a>HS \_ 主机 \_ 发送 \_ 保持 \_ 活动 \_ 完成功能

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 主机 send \_ keep-alive \_ \_ \_ 完成**功能指示网络请求的成功或失败情况发送 keep-alive 消息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_HOST_SEND_KEEP_ALIVE_COMPLETION)(
  _In_ HANDLE hPluginContext,
  _In_ DWORD  dwResult
);
```

<a name="parameters"></a>参数
----------

*hPluginContext* \[中\]  
调用此函数的插件的上下文句柄。

*dwResult* \[中\]  
结果代码。

<a name="return-value"></a>返回值
------------

此函数由插件调用，以与主机通信并且不返回值。

<a name="remarks"></a>备注
-------

插件必须调用此函数以通知主机对 HS 插件的先前调用的结果 [** \_ \_ 发送 \_ 保持 \_ 活动状态**](hs-plugin-send-keep-alive.md)。

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


[**HS \_ 插件 \_ 发送 \_ 保持 \_ 活动状态**](hs-plugin-send-keep-alive.md)

 

 




