---
title: HS_PLUGIN_VERSION 结构
description: HS_PLUGIN_VERSION 结构包含插件支持的最小和最大热点主机版本。
keywords:
- 从 Windows Vista 开始 HS_PLUGIN_VERSION 结构网络驱动程序
- 从 Windows Vista 开始 PHS_PLUGIN_VERSION 结构指针网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: f01767c7d1c03e6f388d194e60875582a5d3f81c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823907"
---
# <a name="hs_plugin_version-structure"></a>HS \_ 插件 \_ 版本结构

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 插件 \_ 版本** 结构包含插件支持的最小和最大热点主机版本。

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
<td><p>标头</p></td>
<td>Hotspotoffloadplugin (包含 Hotspotoffloadplugin) </td>
</tr>
</tbody>
</table>

 

 




