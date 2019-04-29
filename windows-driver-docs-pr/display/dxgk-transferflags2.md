---
title: '\_DXGK\_TRANSFERFLAGS2 结构'
description: DXGK\_TRANSFERFLAGS2 结构保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: 5bc690c4-d95a-4048-b716-fb2b12a22a86
keywords:
- _DXGK_TRANSFERFLAGS2 结构显示设备
- DXGK_TRANSFERFLAGS2 结构显示设备
topic_type:
- apiref
api_name:
- DXGK_TRANSFERFLAGS2
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: f017aaafc25f3e5acad42d84bb0a12ac42f1da75
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350283"
---
# <a name="dxgktransferflags2-structure"></a>\_DXGK\_TRANSFERFLAGS2 结构


DXGK\_TRANSFERFLAGS2 结构保留供系统使用。 不要使用它在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGK_TRANSFERFLAGS2 {
  union {
    struct {
      UINT Swizzle  :1;
      UINT Unswizzle  :1;
      UINT AllocationIsIdle  :1;
      UINT SwizzlingRange  :1;
      UINT Reserved  :28;
    };
    UINT Value;
  };
} DXGK_TRANSFERFLAGS2;
```

<a name="members"></a>成员
-------

**Swizzle**保留供系统使用。

**Unswizzle**保留供系统使用。

**AllocationIsIdle**保留供系统使用。

**SwizzlingRange**保留供系统使用。

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
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows 7 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">D3dkmddi.h （包括 D3dkmddi.h）</td>
</tr>
</tbody>
</table>

 

 





