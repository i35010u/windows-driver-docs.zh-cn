---
title: DXGK \_ PRESENTALLOCATIONINFO 结构
description: DXGK \_ PRESENTALLOCATIONINFO 结构保留供系统使用。 不要在您的驱动程序中使用它。
keywords:
- DXGK_PRESENTALLOCATIONINFO 结构显示设备
topic_type:
- apiref
api_name:
- DXGK_PRESENTALLOCATIONINFO
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 38c2b7d474069b79f0d46e4ae5b49d1a5e84de33
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809015"
---
# <a name="dxgk_presentallocationinfo-structure"></a>DXGK \_ PRESENTALLOCATIONINFO 结构


DXGK \_ PRESENTALLOCATIONINFO 结构保留供系统使用。 不要在您的驱动程序中使用它。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGK_PRESENTALLOCATIONINFO {
  HANDLE                 hDeviceSpecificAllocation;
  D3DGPU_VIRTUAL_ADDRESS AllocationVirtualAddress;
  PHYSICAL_ADDRESS       PhysicalAddress;
  WORD                   SegmentId;
  WORD                   PhysicalAdapterIndex;
} DXGK_PRESENTALLOCATIONINFO;
```

<a name="members"></a>成员
-------

**hDeviceSpecificAllocation** 保留供系统使用。

**AllocationVirtualAddress** 保留供系统使用。

**PhysicalAddress** 保留供系统使用。

**SegmentId** 保留供系统使用。

**PhysicalAdapterIndex** 保留供系统使用。

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

 

 





