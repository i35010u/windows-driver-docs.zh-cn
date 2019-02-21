---
title: HS_PLUGIN_CHECK_FOR_UPDATES 函数
description: HS_PLUGIN_CHECK_FOR_UPDATES 函数会检查配置更新插件的 HS_PLUGIN_PROFILE 结构 dwProfileUpdateTimeDays 成员中指定的频率。
ms.assetid: 8db3c237-d61b-4dca-b3a5-2fdaeb683b15
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 typedef DWORD (WINAPI HS_PLUGIN_CHECK_FOR_UPDATES) 函数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: dde9ec25b30f0b28c742229a2714d9b98733022c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522207"
---
# <a name="hsplugincheckforupdates-function"></a>HS\_插件\_检查\_为\_更新函数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_插件\_检查\_有关\_更新**函数中指定的频率配置更新检查**dwProfileUpdateTimeDays**插件的成员[ **HS\_插件\_配置文件**](hs-plugin-profile.md)结构。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_CHECK_FOR_UPDATES)(
    
);
```

<a name="parameters"></a>参数
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
<td><p>标头</p></td>
<td>Hotspotoffloadplugin.h （包括 Hotspotoffloadplugin.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**HS\_插件\_配置文件**](hs-plugin-profile.md)

 

 




