---
title: '\_DXGK \_ TRANSFERFLAGS2 结构'
description: DXGK \_ TRANSFERFLAGS2 结构保留供系统使用。 不要在您的驱动程序中使用它。
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
ms.openlocfilehash: c201fb1933aab4cd6fc2118d9d54cf05e490b1d8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808993"
---
# <a name="_dxgk_transferflags2-structure"></a>\_DXGK \_ TRANSFERFLAGS2 结构


DXGK \_ TRANSFERFLAGS2 结构保留供系统使用。 不要在您的驱动程序中使用它。

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

**Swizzle** 保留供系统使用。

**Unswizzle** 保留供系统使用。

**AllocationIsIdle** 保留供系统使用。

**SwizzlingRange** 保留供系统使用。

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

 

 





