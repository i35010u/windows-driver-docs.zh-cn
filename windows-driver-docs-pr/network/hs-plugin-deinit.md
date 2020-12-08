---
title: HS_PLUGIN_DEINIT 函数
description: 宿主调用 HS_PLUGIN_DEINIT 函数以通知插件它将被卸载。
keywords:
- typedef DWORD (WINAPI HS_PLUGIN_DEINIT 从 Windows Vista 开始) 函数网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: e319687bd83a1c89d292017ae4f0c4c66a46673d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821365"
---
# <a name="hs_plugin_deinit-function"></a>HS \_ 插件 \_ DEINIT 函数

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


主机调用 **HS \_ 插件 \_ DEINIT** 函数，以通知插件它将被卸载。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_DEINIT)(
  _In_ eHS_UNLOAD_REASON UnloadReason
);
```

<a name="parameters"></a>参数
----------

*UnloadReason* \[中\]  
[**EHS \_ 卸载 \_ 原因**](ehs-unload-reason.md)枚举值，指示卸载的原因。

<a name="return-value"></a>返回值
------------

宿主调用此函数以与插件通信，而不返回值。

<a name="remarks"></a>备注
-------

收到通知后，如果需要，插件应该会完成任何当前活动并保存状态。

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


[**eHS \_ 卸载 \_ 原因**](ehs-unload-reason.md)

 

 




