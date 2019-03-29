---
title: '\_DXGKARG\_UPDATEPAGETABLE 结构'
description: DXGKARG\_UPDATEPAGETABLE 结构保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: abd5a200-5f10-4b5d-98e5-f75bc045aff8
keywords:
- _DXGKARG_UPDATEPAGETABLE 结构显示设备
- DXGKARG_UPDATEPAGETABLE 结构显示设备
topic_type:
- apiref
api_name:
- DXGKARG_UPDATEPAGETABLE
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 33e65321bae2be7635717182a87874c9135eee8b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567460"
---
# <a name="dxgkargupdatepagetable-structure"></a>\_DXGKARG\_UPDATEPAGETABLE 结构


DXGKARG\_UPDATEPAGETABLE 结构保留供系统使用。 不要使用它在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGKARG_UPDATEPAGETABLE {
  PVOID                        pPageTable;
  UINT                         SizeOfPageTableInPages;
  UINT                         StartIndex;
  UINT                         PageCount;
  const DXGK_PTE               *PTEArray;
  HANDLE                       hAllocation;
  UINT                         PageOffset;
  DXGKARG_UPDATEPAGETABLEFLAGS Flags;
} DXGKARG_UPDATEPAGETABLE;
```

<a name="members"></a>成员
-------

**pPageTable**保留供系统使用。

**SizeOfPageTableInPages**保留供系统使用。

**StartIndex**保留供系统使用。

**PageCount**保留供系统使用。

**PTEArray**保留供系统使用。

**hAllocation**保留供系统使用。

**PageOffset**保留供系统使用。

**标志**保留供系统使用。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows 7 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">D3dkmddi.h （包括 D3dkmddi.h）</td>
</tr>
</tbody>
</table>

 

 





