---
title: DXGK\_SEGMENTDESCRIPTOR2 结构
description: DXGK\_SEGMENTDESCRIPTOR2 结构保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: 94eb1c9a-919c-4819-848b-29106e216980
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
ms.openlocfilehash: 2c0ea78370d3b2975c3ee8e934067c79a27d8098
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576718"
---
# <a name="dxgksegmentdescriptor2-structure"></a>DXGK\_SEGMENTDESCRIPTOR2 结构


DXGK\_SEGMENTDESCRIPTOR2 结构保留供系统使用。 不要使用它在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGK_SEGMENTDESCRIPTOR2 {
  DXGK_SEGMENTFLAGS2 Flags;
  SIZE_T             Size;
  PMDL               pMdl;
  PHYSICAL_ADDRESS   BaseAddress;
  PHYSICAL_ADDRESS   CpuTranslatedAddress;
} DXGK_SEGMENTDESCRIPTOR2;
```

<a name="members"></a>成员
-------

**标志**保留供系统使用。

**大小**保留供系统使用。

**pMdl**保留供系统使用。

**BaseAddress**保留供系统使用。

**CpuTranslatedAddress**保留供系统使用。

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

 

 





