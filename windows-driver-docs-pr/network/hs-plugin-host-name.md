---
title: HS_PLUGIN_HOST_NAME 结构
description: HS_PLUGIN_HOST_NAME 结构包含主机名。
ms.assetid: 3995fff6-6992-4dd6-a94c-a27b2ee44436
keywords:
- 从 Windows Vista 开始 HS_PLUGIN_HOST_NAME 结构网络驱动程序
- 从 Windows Vista 开始 PHS_PLUGIN_HOST_NAME 结构指针网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73a84e19c647049b5a77762f5cb643aa3e24196d
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403042"
---
# <a name="hs_plugin_host_name-structure"></a>HS \_ 插件 \_ 主机 \_ 名称结构

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 插件 \_ 主机 \_ 名称**结构包含主机名。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _HS_PLUGIN_HOST_NAME {
  WHCAR pszHostName[HS_CONST_MAX_HOST_NAME_LENGTH+1];
} HS_PLUGIN_HOST_NAME, *PHS_PLUGIN_HOST_NAME;
```

<a name="members"></a>成员
-------

**pszHostName**  
指向主机名的指针。

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

 

 




