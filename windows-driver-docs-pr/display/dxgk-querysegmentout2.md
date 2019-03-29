---
title: DXGK\_QUERYSEGMENTOUT2 结构
description: DXGK\_QUERYSEGMENTOUT2 结构保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: 7193c763-fd76-4d7a-81ac-dfcc2b7bf881
keywords:
- DXGK_QUERYSEGMENTOUT2 结构显示设备
topic_type:
- apiref
api_name:
- DXGK_QUERYSEGMENTOUT2
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: c24a6c657c25b27518888ac53d6114bf663707a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568529"
---
# <a name="dxgkquerysegmentout2-structure"></a>DXGK\_QUERYSEGMENTOUT2 结构


DXGK\_QUERYSEGMENTOUT2 结构保留供系统使用。 不要使用它在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGK_QUERYSEGMENTOUT2 {
  UINT                    SegmentCount;
  DXGK_SEGMENTDESCRIPTOR2 *pSegmentDescriptor;
} DXGK_QUERYSEGMENTOUT2;
```

<a name="members"></a>成员
-------

**SegmentCount**保留供系统使用。

**pSegmentDescriptor**保留供系统使用。

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

 

 





