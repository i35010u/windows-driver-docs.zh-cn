---
title: HS_PLUGIN_DEINIT 函数
description: HS_PLUGIN_DEINIT 函数称为主机来通知该插件将被卸载。
ms.assetid: 3bb0ad85-91db-476e-b347-0fa8ed4ae24e
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 typedef DWORD (WINAPI HS_PLUGIN_DEINIT) 函数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9fb4383d35237faeb57585798523f60983256e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526826"
---
# <a name="hsplugindeinit-function"></a>HS\_插件\_DEINIT 函数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_插件\_DEINIT**函数调用由主机来通知该插件将被卸载。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_DEINIT)(
  _In_ eHS_UNLOAD_REASON UnloadReason
);
```

<a name="parameters"></a>参数
----------

*UnloadReason* \[中\]  
[ **EHS\_卸载\_原因**](ehs-unload-reason.md)枚举值，该值指示为要卸载的原因。

<a name="return-value"></a>返回值
------------

此函数调用由宿主与插件进行通信，并不会返回一个值。

<a name="remarks"></a>备注
-------

收到通知，它将被卸载时，该插件应完成当前的所有活动，如果需要保存状态。

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
<td>Hotspotoffloadplugin.h （包括 Hotspotoffloadplugin.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**eHS\_UNLOAD\_REASON**](ehs-unload-reason.md)

 

 




