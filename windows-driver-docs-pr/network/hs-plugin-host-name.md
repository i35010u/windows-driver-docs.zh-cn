---
title: HS_PLUGIN_HOST_NAME 结构
description: HS_PLUGIN_HOST_NAME 结构包含主机名。
keywords:
- 从 Windows Vista 开始 HS_PLUGIN_HOST_NAME 结构网络驱动程序
- 从 Windows Vista 开始 PHS_PLUGIN_HOST_NAME 结构指针网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 244db0fd25e8e5996a18e01b70fd1a8fdcb4f114
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837691"
---
# <a name="hs_plugin_host_name-structure"></a>HS \_ 插件 \_ 主机 \_ 名称结构

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ 插件 \_ 主机 \_ 名称** 结构包含主机名。

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
<td><p>标头</p></td>
<td>Hotspotoffloadplugin (包含 Hotspotoffloadplugin) </td>
</tr>
</tbody>
</table>

 

 




