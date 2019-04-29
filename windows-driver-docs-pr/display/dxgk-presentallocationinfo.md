---
title: DXGK\_PRESENTALLOCATIONINFO 结构
description: DXGK\_PRESENTALLOCATIONINFO 结构保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: 8a7f25cf-c08c-4f65-bbf4-ba129d88ff6a
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
ms.openlocfilehash: 360e4c8978e9ddc4f98bfaeb4528fd59dbce3cee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392031"
---
# <a name="dxgkpresentallocationinfo-structure"></a>DXGK\_PRESENTALLOCATIONINFO 结构


DXGK\_PRESENTALLOCATIONINFO 结构保留供系统使用。 不要使用它在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGK_PRESENTALLOCATIONINFO {
  HANDLE                 hDeviceSpecificAllocation;
  D3DGPU_VIRTUAL_ADDRESS AllocationVirtualAddress;
  PHYSICAL_ADDRESS       PhysicalAddress;
  WORD                   SegmentId;
  WORD                   PhysicalAdapterIndex;
} DXGK_PRESENTALLOCATIONINFO;
```

<a name="members"></a>成员
-------

**hDeviceSpecificAllocation**保留供系统使用。

**AllocationVirtualAddress**保留供系统使用。

**PhysicalAddress**保留供系统使用。

**SegmentId**保留供系统使用。

**PhysicalAdapterIndex**保留供系统使用。

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

 

 





