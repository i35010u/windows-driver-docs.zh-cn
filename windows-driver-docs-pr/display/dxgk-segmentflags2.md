---
title: DXGK\_SEGMENTFLAGS2 结构
description: DXGK\_SEGMENTFLAGS2 结构保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: 9e6f96a2-d32f-4ef8-aaad-dc0cbd053222
keywords:
- DXGK_SEGMENTFLAGS2 结构显示设备
topic_type:
- apiref
api_name:
- DXGK_SEGMENTFLAGS2
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: a403faf9a775b7b40a142fe973dd3e96bdc2adbf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567034"
---
# <a name="dxgksegmentflags2-structure"></a>DXGK\_SEGMENTFLAGS2 结构


DXGK\_SEGMENTFLAGS2 结构保留供系统使用。 不要使用它在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGK_SEGMENTFLAGS2 {
  union {
    struct {
      UINT Aperture  :1;
      UINT PopulatedFromSystemMemory  :1;
      UINT SystemMemoryReservedByBios  :1;
      UINT CpuVisible  :1;
      UINT Reserved  :28;
    };
    UINT Value;
  };
} DXGK_SEGMENTFLAGS2;
```

<a name="members"></a>成员
-------

**Aperture**保留供系统使用。

**PopulatedFromSystemMemory**保留供系统使用。

**SystemMemoryReservedByBios**保留供系统使用。

**CpuVisible**保留供系统使用。

**保留**保留供系统使用。

**值**保留供系统使用。

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

 

 





