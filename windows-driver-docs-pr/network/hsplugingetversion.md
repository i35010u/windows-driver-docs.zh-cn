---
title: HSPluginGetVersion 函数
description: HSPluginGetVersion 函数导出由插件 DLL，并调用以验证插件版本与主机版本相匹配。
ms.assetid: dfdd534c-43c0-4d96-b85b-de9c2830322d
keywords:
- 与 Windows Vista 一起启动的网络驱动程序的 HSPluginGetVersion 函数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b1a3709b96a2584e44942be540949fad8a09b3f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541271"
---
# <a name="hsplugingetversion-function"></a>HSPluginGetVersion 函数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HSPluginGetVersion**函数由插件 DLL 导出函数，调用以验证插件版本符合主机版本。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
DWORD HSPluginGetVersion(
  _Out_ HS_PLUGIN_VERSION *pHotspotPluginVersion
);
```

<a name="parameters"></a>参数
----------

*\*pHotspotPluginVersion* \[out\]  
一个指向[ **HS\_插件\_版本**](hs-plugin-version.md)结构，其中包含有关该插件的版本信息。

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


[**HS\_插件\_版本**](hs-plugin-version.md)

 

 




