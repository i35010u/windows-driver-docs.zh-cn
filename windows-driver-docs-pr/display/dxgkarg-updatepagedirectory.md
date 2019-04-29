---
title: '\_DXGKARG\_UPDATEPAGEDIRECTORY 结构'
description: DXGKARG\_UPDATEPAGEDIRECTORY 结构保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: ac16c040-50d8-4716-8275-682092a2be77
keywords:
- _DXGKARG_UPDATEPAGEDIRECTORY 结构显示设备
- DXGKARG_UPDATEPAGEDIRECTORY 结构显示设备
topic_type:
- apiref
api_name:
- DXGKARG_UPDATEPAGEDIRECTORY
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: a34da191de818a172c14f5cd99e5544ec8dcd225
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384491"
---
# <a name="dxgkargupdatepagedirectory-structure"></a>\_DXGKARG\_UPDATEPAGEDIRECTORY 结构


DXGKARG\_UPDATEPAGEDIRECTORY 结构保留供系统使用。 不要使用它在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGKARG_UPDATEPAGEDIRECTORY {
  PVOID          pPageDirectory;
  UINT           StartIndex;
  UINT           PageTableCount;
  const DXGK_PDE *PDEArray;
} DXGKARG_UPDATEPAGEDIRECTORY;
```

<a name="members"></a>成员
-------

**pPageDirectory**保留供系统使用。

**StartIndex**保留供系统使用。

**PageTableCount**保留供系统使用。

**PDEArray**保留供系统使用。

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

 

 





