---
title: HS_HOST_UPDATE_CONFIGURATION_COMPLETION 函数
description: HS_HOST_UPDATE_CONFIGURATION_COMPLETION 函数指示成功或失败的请求以检查更新。
ms.assetid: 7e9eda04-db8e-4181-90e3-8716a99429a8
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 typedef DWORD (WINAPI HS_HOST_UPDATE_CONFIGURATION_COMPLETION) 函数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67135e7348bfe8a3ee2c58b932c98c54f5fad319
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349651"
---
# <a name="hshostupdateconfigurationcompletion-function"></a>HS\_主机\_更新\_配置\_完成函数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_主机\_更新\_配置\_完成**函数指示成功或失败的请求以检查更新。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_HOST_UPDATE_CONFIGURATION_COMPLETION)(
  _In_ HANDLE            hPluginContext,
  _In_ eHS_UPDATE_RESULT UpdateResult
);
```

<a name="parameters"></a>Parameters
----------

*hPluginContext* \[in\]  
此函数在调用插件的上下文句柄。

*UpdateResult* \[中\]  
[ **EHS\_更新\_结果**](ehs-update-result.md)枚举值，该值指示要检查是否有更新的请求的结果。

<a name="return-value"></a>返回值
------------

此函数调用由插件与主机通信，并不会返回一个值。

<a name="remarks"></a>备注
-------

该插件必须调用此函数来通知以前调用的结果的宿主[ **HS\_插件\_检查\_有关\_更新**](hs-plugin-check-for-updates.md)。

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


[**eHS\_UPDATE\_RESULT**](ehs-update-result.md)

[**HS\_插件\_检查\_为\_更新**](hs-plugin-check-for-updates.md)

 

 




