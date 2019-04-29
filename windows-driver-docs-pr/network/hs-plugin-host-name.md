---
title: HS_PLUGIN_HOST_NAME 结构
description: HS_PLUGIN_HOST_NAME 结构包含的主机名。
ms.assetid: 3995fff6-6992-4dd6-a94c-a27b2ee44436
keywords:
- HS_PLUGIN_HOST_NAME 结构与 Windows Vista 一起启动的网络驱动程序
- PHS_PLUGIN_HOST_NAME 结构指针与 Windows Vista 一起启动的网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4457f8f594fe1a2663c23929e045865ba92ed18
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322191"
---
# <a name="hspluginhostname-structure"></a>HS\_插件\_主机\_结构

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_插件\_主机\_名称**结构包含的主机名。

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
<td>Hotspotoffloadplugin.h （包括 Hotspotoffloadplugin.h）</td>
</tr>
</tbody>
</table>

 

 




