---
title: DXGK \_ SEGMENTDESCRIPTOR2 结构
description: DXGK \_ SEGMENTDESCRIPTOR2 结构保留供系统使用。 不要在您的驱动程序中使用它。
keywords:
- DXGK_SEGMENTDESCRIPTOR2 结构显示设备
topic_type:
- apiref
api_name:
- DXGK_SEGMENTDESCRIPTOR2
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 18a1cd90442a6771b354d378b7a31ea56ca411ba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808997"
---
# <a name="dxgk_segmentdescriptor2-structure"></a>DXGK \_ SEGMENTDESCRIPTOR2 结构


DXGK \_ SEGMENTDESCRIPTOR2 结构保留供系统使用。 不要在您的驱动程序中使用它。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGK_SEGMENTDESCRIPTOR2 {
  DXGK_SEGMENTFLAGS2 Flags;
  SIZE_T             Size;
  PMDL               pMdl;
  PHYSICAL_ADDRESS   BaseAddress;
  PHYSICAL_ADDRESS   CpuTranslatedAddress;
} DXGK_SEGMENTDESCRIPTOR2;
```

<a name="members"></a>成员
-------

**标志** 保留供系统使用。

**大小** 保留供系统使用。

**pMdl** 保留供系统使用。

**BaseAddress** 保留供系统使用。

**CpuTranslatedAddress** 保留供系统使用。

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

 

 





