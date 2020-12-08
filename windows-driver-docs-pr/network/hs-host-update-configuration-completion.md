---
title: HS_HOST_UPDATE_CONFIGURATION_COMPLETION 函数
description: HS_HOST_UPDATE_CONFIGURATION_COMPLETION 函数指示检查更新的请求是成功还是失败。
keywords:
- typedef DWORD (WINAPI HS_HOST_UPDATE_CONFIGURATION_COMPLETION 从 Windows Vista 开始) 函数网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d1cb79e21f3260568a51ee223a3b3219b095ed9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814169"
---
# <a name="hs_host_update_configuration_completion-function"></a>HS \_ 主机 \_ 更新 \_ 配置 \_ 完成功能

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 主机 \_ 更新 \_ 配置 \_ 完成** 功能指示检查更新的请求是成功还是失败。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_HOST_UPDATE_CONFIGURATION_COMPLETION)(
  _In_ HANDLE            hPluginContext,
  _In_ eHS_UPDATE_RESULT UpdateResult
);
```

<a name="parameters"></a>参数
----------

*hPluginContext* \[中\]  
调用此函数的插件的上下文句柄。

*UpdateResult* \[中\]  
[**EHS \_ UPDATE \_ result**](ehs-update-result.md)枚举值，指示请求检查更新的结果。

<a name="return-value"></a>返回值
------------

此函数由插件调用，以与主机通信并且不返回值。

<a name="remarks"></a>备注
-------

插件必须调用此函数以通知主机对 HS 插件的先前调用的结果 [**\_ \_ 检查 \_ 是否有 \_ 更新**](hs-plugin-check-for-updates.md)。

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
<td>Hotspotoffloadplugin (包含 Hotspotoffloadplugin) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**eHS \_ 更新 \_ 结果**](ehs-update-result.md)

[**HS \_ 插件 \_ 检查 \_ \_ 更新**](hs-plugin-check-for-updates.md)

 

 




