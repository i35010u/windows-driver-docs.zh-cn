---
title: HS_PLUGIN_VERSION 结构
description: HS_PLUGIN_VERSION 结构包含插件支持的最小和最大热点主机版本。
ms.assetid: ced24606-0379-4b13-831c-11de3ed6cd2b
keywords:
- 从 Windows Vista 开始 HS_PLUGIN_VERSION 结构网络驱动程序
- 从 Windows Vista 开始 PHS_PLUGIN_VERSION 结构指针网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40408006fe857c8c14a81f9ce1e6241deca24e07
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89402980"
---
# <a name="hs_plugin_version-structure"></a>HS \_ 插件 \_ 版本结构

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 插件 \_ 版本**结构包含插件支持的最小和最大热点主机版本。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _HS_PLUGIN_VERSION {
  DWORD dwVerMin;
  DWORD dwVerMax;
} HS_PLUGIN_VERSION, *PHS_PLUGIN_VERSION;
```

<a name="members"></a>成员
-------

**dwVerMin**  
插件支持的最小热点主机版本。

**dwVerMax**  
插件支持的最高热点主机版本。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Hotspotoffloadplugin (包含 Hotspotoffloadplugin) </td>
</tr>
</tbody>
</table>

 

 




