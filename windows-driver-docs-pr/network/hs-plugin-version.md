---
title: HS_PLUGIN_VERSION 结构
description: HS_PLUGIN_VERSION 结构包含由插件所支持的最小值和最大热点主机版本。
ms.assetid: ced24606-0379-4b13-831c-11de3ed6cd2b
keywords:
- HS_PLUGIN_VERSION 结构与 Windows Vista 一起启动的网络驱动程序
- PHS_PLUGIN_VERSION 结构指针与 Windows Vista 一起启动的网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5db1c982afe60fbaa492b551fa452aede38370c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569373"
---
# <a name="hspluginversion-structure"></a>HS\_插件\_版本的结构

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_插件\_版本**结构包含由插件所支持的最小值和最大热点主机版本。

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
该插件支持的最小热点主机版本。

**dwVerMax**  
该插件支持的最大热点主机版本。

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
<td>Hotspotoffloadplugin.h （包括 Hotspotoffloadplugin.h）</td>
</tr>
</tbody>
</table>

 

 




