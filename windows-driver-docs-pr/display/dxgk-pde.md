---
title: '\_DXGK\_PDE 结构'
description: DXGK\_PDE 结构保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: e2cd4541-beda-4c61-bdba-a86ae3888501
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
ms.openlocfilehash: 5b78cf2ade71e885665748cedbf9cd69e6ad8101
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566470"
---
# <a name="dxgkpde-structure"></a>\_DXGK\_PDE 结构


DXGK\_PDE 结构保留供系统使用。 不要使用它在您的驱动程序中。

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

**有效**保留供系统使用。

**段**保留供系统使用。

**保留**保留供系统使用。

**PageTableAddress**保留供系统使用。

**值**保留供系统使用。

**PageTableSizeInPages**保留供系统使用。

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

 

 





