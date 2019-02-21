---
title: '\_DXGK\_ALLOCATIONINFO2 结构'
description: DXGK\_ALLOCATIONINFO2 结构保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: af396dd1-6b47-4724-a481-c8f4646816e9
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
ms.openlocfilehash: 23c1e8d305312dfa6750d7b313a1626c038147c6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543164"
---
# <a name="dxgkallocationinfo2-structure"></a>\_DXGK\_ALLOCATIONINFO2 结构


DXGK\_ALLOCATIONINFO2 结构保留供系统使用。 不要使用它在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGK_ALLOCATIONINFO2 {
  VOID                      *pPrivateDriverData;
  UINT                      PrivateDriverDataSize;
  UINT                      Alignment;
  SIZE_T                    Size;
  DXGK_SEGMENTPREFERENCE    PreferredSegment;
  UINT                      SupportedSegmentSet;
  UINT                      MaximumRenamingListLength;
  HANDLE                    hAllocation;
  DXGK_ALLOCATIONINFOFLAGS2 Flags;
  DXGK_ALLOCATIONUSAGEHINT  *pAllocationUsageHint;
  UINT                      AllocationPriority;
  UINT                      AllocationGroup;
  UINT                      SwizzlingInvariantBlockSize;
  UINT                      Reserved[6];
} DXGK_ALLOCATIONINFO2;
```

<a name="members"></a>成员
-------

**pPrivateDriverData**保留供系统使用。

**PrivateDriverDataSize**保留供系统使用。

**对齐方式**保留供系统使用。

**大小**保留供系统使用。

**PreferredSegment**保留供系统使用。

**SupportedSegmentSet**保留供系统使用。

**MaximumRenamingListLength**保留供系统使用。

**hAllocation**保留供系统使用。

**标志**保留供系统使用。

**pAllocationUsageHint**保留供系统使用。

**AllocationPriority**保留供系统使用。

**AllocationGroup**保留供系统使用。

**SwizzlingInvariantBlockSize**保留供系统使用。

**保留**保留供系统使用。

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
<td align="left"><p>标头</p></td>
<td align="left">D3dkmddi.h （包括 D3dkmddi.h）</td>
</tr>
</tbody>
</table>

 

 





