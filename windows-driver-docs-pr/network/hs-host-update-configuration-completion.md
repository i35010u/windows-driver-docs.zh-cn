---
title: HS_HOST_UPDATE_CONFIGURATION_COMPLETION 函数
description: HS_HOST_UPDATE_CONFIGURATION_COMPLETION 函数指示检查更新的请求是成功还是失败。
ms.assetid: 7e9eda04-db8e-4181-90e3-8716a99429a8
keywords:
- typedef DWORD (WINAPI HS_HOST_UPDATE_CONFIGURATION_COMPLETION 从 Windows Vista 开始) 函数网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0a69af43a6428e15a7a73aa3b18e2b41f5b408c
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403076"
---
# <a name="hs_host_update_configuration_completion-function"></a>HS \_ 主机 \_ 更新 \_ 配置 \_ 完成功能

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 主机 \_ 更新 \_ 配置 \_ 完成**功能指示检查更新的请求是成功还是失败。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_HOST_UPDATE_CONFIGURATION_COMPLETION)(
  _In_ HANDLE            hPluginContext,
  _In_ eHS_UPDATE_RESULT UpdateResult
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

插件必须调用此函数以通知主机对 HS 插件的先前调用的结果 [** \_ \_ 检查 \_ 是否有 \_ 更新**](hs-plugin-check-for-updates.md)。

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


[**eHS \_ 更新 \_ 结果**](ehs-update-result.md)

[**HS \_ 插件 \_ 检查 \_ \_ 更新**](hs-plugin-check-for-updates.md)

 

 




