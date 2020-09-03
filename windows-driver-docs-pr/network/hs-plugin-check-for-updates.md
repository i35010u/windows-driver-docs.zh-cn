---
title: HS_PLUGIN_CHECK_FOR_UPDATES 函数
description: HS_PLUGIN_CHECK_FOR_UPDATES 函数按在插件 HS_PLUGIN_PROFILE 结构的 dwProfileUpdateTimeDays 成员中指定的频率检查配置更新。
ms.assetid: 8db3c237-d61b-4dca-b3a5-2fdaeb683b15
keywords:
- typedef DWORD (WINAPI HS_PLUGIN_CHECK_FOR_UPDATES 从 Windows Vista 开始) 函数网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6122d1315f1ff213476adef6a0a4713c4dd98c47
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403058"
---
# <a name="hs_plugin_check_for_updates-function"></a>HS \_ 插件 \_ 检查 \_ \_ 更新功能

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**Hs \_ 插件 \_ 检查 \_ \_ 更新**功能按在插件的[**HS \_ 插件 \_ 配置文件**](hs-plugin-profile.md)结构的**dwProfileUpdateTimeDays**成员中指定的频率检查配置更新。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_CHECK_FOR_UPDATES)(
    
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

 

 




