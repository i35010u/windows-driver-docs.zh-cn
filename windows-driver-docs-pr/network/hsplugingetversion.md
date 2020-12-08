---
title: HSPluginGetVersion 函数
description: HSPluginGetVersion 函数由插件 DLL 导出，并调用来验证插件版本是否匹配主机版本。
keywords:
- 从 Windows Vista 开始的 HSPluginGetVersion 函数网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: cac1a737f04361f1095f518d6e40051baea9f51e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823885"
---
# <a name="hsplugingetversion-function"></a>HSPluginGetVersion 函数

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HSPluginGetVersion** 函数由插件 DLL 导出，并调用来验证插件版本是否匹配主机版本。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
DWORD HSPluginGetVersion(
  _Out_ HS_PLUGIN_VERSION *pHotspotPluginVersion
);
```

<a name="parameters"></a>参数
----------

*\* pHotspotPluginVersion* \[\]  
一个指针，指向包含插件的版本信息的 [**HS \_ 插件 \_ 版本**](hs-plugin-version.md) 结构。

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


[**HS \_ 插件 \_ 版本**](hs-plugin-version.md)

 

 




