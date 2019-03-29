---
title: '\_DXGK\_ALLOCATIONGROUPOUT 结构'
description: DXGK\_ALLOCATIONGROUPOUT 结构保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: 4aafe036-09a5-4e2d-a2ea-b81d0ba05ec1
keywords:
- _DXGK_ALLOCATIONGROUPOUT 结构显示设备
- DXGK_ALLOCATIONGROUPOUT 结构显示设备
topic_type:
- apiref
api_name:
- DXGK_ALLOCATIONGROUPOUT
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: fcad8a968f450ff2ee47812606936f15529e7db5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563794"
---
# <a name="dxgkallocationgroupout-structure"></a>\_DXGK\_ALLOCATIONGROUPOUT 结构


DXGK\_ALLOCATIONGROUPOUT 结构保留供系统使用。 不要使用它在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGK_ALLOCATIONGROUPOUT {
  UINT                           NbAllocationGroup;
  DXGK_ALLOCATIONGROUPDESCRIPTOR *pAllocationGroupDescriptor;
} DXGK_ALLOCATIONGROUPOUT;
```

<a name="members"></a>成员
-------

**NbAllocationGroup**保留供系统使用。

**pAllocationGroupDescriptor**保留供系统使用。

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

 

 





