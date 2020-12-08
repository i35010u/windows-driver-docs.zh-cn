---
title: DXGK \_ SEGMENTFLAGS2 结构
description: DXGK \_ SEGMENTFLAGS2 结构保留供系统使用。 不要在您的驱动程序中使用它。
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
ms.openlocfilehash: c97a0d35df3ae4eb179b6f778b604fd66f515c3e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808995"
---
# <a name="dxgk_segmentflags2-structure"></a>DXGK \_ SEGMENTFLAGS2 结构


DXGK \_ SEGMENTFLAGS2 结构保留供系统使用。 不要在您的驱动程序中使用它。

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

**口径** 保留供系统使用。

**PopulatedFromSystemMemory** 保留供系统使用。

**SystemMemoryReservedByBios** 保留供系统使用。

**CpuVisible** 保留供系统使用。

**保留** 保留供系统使用。

**值** 保留供系统使用。

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

 

 





