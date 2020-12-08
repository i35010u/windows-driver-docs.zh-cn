---
title: '\_DXGK \_ ALLOCATIONINFO2 结构'
description: DXGK \_ ALLOCATIONINFO2 结构保留供系统使用。 不要在您的驱动程序中使用它。
keywords:
- _DXGK_ALLOCATIONINFO2 结构显示设备
- DXGK_ALLOCATIONINFO2 结构显示设备
topic_type:
- apiref
api_name:
- DXGK_ALLOCATIONINFO2
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: ceddae7ca8d0c9fab39880910d47455a5620d61b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809061"
---
# <a name="_dxgk_allocationinfo2-structure"></a>\_DXGK \_ ALLOCATIONINFO2 结构


DXGK \_ ALLOCATIONINFO2 结构保留供系统使用。 不要在您的驱动程序中使用它。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGK_ALLOCATIONINFO2 {
  VOID                      *pPrivateDriverData;
  UINT                      PrivateDriverDataSize;
  UINT                      Alignment;
  SIZE_T                    Size;
  DXGK_SEGMENTPREFERENCE    PreferredSegment;
  UINT                      SupportedSegmentSet;
  UINT                      MaximumRenamingListLength;
  HANDLE                    hAllocation;
  DXGK_ALLOCATIONINFOFLAGS2 Flags;
  DXGK_ALLOCATIONUSAGEHINT  *pAllocationUsageHint;
  UINT                      AllocationPriority;
  UINT                      AllocationGroup;
  UINT                      SwizzlingInvariantBlockSize;
  UINT                      Reserved[6];
} DXGK_ALLOCATIONINFO2;
```

<a name="members"></a>成员
-------

**pPrivateDriverData** 保留供系统使用。

**PrivateDriverDataSize** 保留供系统使用。

**对齐** 保留供系统使用。

**大小** 保留供系统使用。

**PreferredSegment** 保留供系统使用。

**SupportedSegmentSet** 保留供系统使用。

**MaximumRenamingListLength** 保留供系统使用。

**hAllocation** 保留供系统使用。

**标志** 保留供系统使用。

**pAllocationUsageHint** 保留供系统使用。

**AllocationPriority** 保留供系统使用。

**AllocationGroup** 保留供系统使用。

**SwizzlingInvariantBlockSize** 保留供系统使用。

**保留** 保留供系统使用。

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
<td align="left"><p>在 windows 7 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">D3dkmddi (包含 D3dkmddi) </td>
</tr>
</tbody>
</table>

 

 





