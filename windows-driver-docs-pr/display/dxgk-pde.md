---
title: '\_DXGK \_ PDE 结构'
description: DXGK \_ PDE 结构保留供系统使用。 不要在您的驱动程序中使用它。
keywords:
- _DXGK_PDE 结构显示设备
- DXGK_PDE 结构显示设备
topic_type:
- apiref
api_name:
- DXGK_PDE
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: ecb3ea3ac16def8e9c8abb534c152303fb4c71f0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809029"
---
# <a name="_dxgk_pde-structure"></a>\_DXGK \_ PDE 结构


DXGK \_ PDE 结构保留供系统使用。 不要在您的驱动程序中使用它。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGK_PDE {
  union {
    struct {
      ULONGLONG Valid  :1;
      ULONGLONG Segment  :5;
      ULONGLONG Reserved  :6;
      ULONGLONG PageTableAddress  :52;
    };
    ULONGLONG Value;
  };
  UINT PageTableSizeInPages;
} DXGK_PDE;
```

<a name="members"></a>成员
-------

**有效** 保留供系统使用。

**段** 保留供系统使用。

**保留** 保留供系统使用。

**PageTableAddress** 保留供系统使用。

**值** 保留供系统使用。

**PageTableSizeInPages** 保留供系统使用。

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

 

 





