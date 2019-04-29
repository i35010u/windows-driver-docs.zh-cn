---
title: '\_DXGKARG\_MOVEPAGEDIRECTORY 结构'
description: DXGKARG\_MOVEPAGEDIRECTORY 结构保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: 81db1be9-4673-4353-b85f-8c6b87da1fc2
keywords:
- _DXGKARG_MOVEPAGEDIRECTORY 结构显示设备
- DXGKARG_MOVEPAGEDIRECTORY 结构显示设备
topic_type:
- apiref
api_name:
- DXGKARG_MOVEPAGEDIRECTORY
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: e74f8a20fe41acee0fa28176ca88d334d3e180af
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384496"
---
# <a name="dxgkargmovepagedirectory-structure"></a>\_DXGKARG\_MOVEPAGEDIRECTORY 结构


DXGKARG\_MOVEPAGEDIRECTORY 结构保留供系统使用。 不要使用它在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGKARG_MOVEPAGEDIRECTORY {
  PVOID            pPageDirectory;
  PHYSICAL_ADDRESS PhysicalAddress;
  UINT             Segment;
  UINT             SizeInPages;
} DXGKARG_MOVEPAGEDIRECTORY;
```

<a name="members"></a>成员
-------

**pPageDirectory**保留供系统使用。

**PhysicalAddress**保留供系统使用。

**段**保留供系统使用。

**SizeInPages**保留供系统使用。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows 7 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">D3dkmddi.h （包括 D3dkmddi.h）</td>
</tr>
</tbody>
</table>

 

 





