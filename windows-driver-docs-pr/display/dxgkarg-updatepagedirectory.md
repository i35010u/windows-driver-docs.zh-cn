---
title: '\_DXGKARG \_ UPDATEPAGEDIRECTORY 结构'
description: DXGKARG \_ UPDATEPAGEDIRECTORY 结构保留供系统使用。 不要在您的驱动程序中使用它。
keywords:
- _DXGKARG_UPDATEPAGEDIRECTORY 结构显示设备
- DXGKARG_UPDATEPAGEDIRECTORY 结构显示设备
topic_type:
- apiref
api_name:
- DXGKARG_UPDATEPAGEDIRECTORY
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 15840fea0c55446c1e192c38bac8a8f77b9758c1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808999"
---
# <a name="_dxgkarg_updatepagedirectory-structure"></a>\_DXGKARG \_ UPDATEPAGEDIRECTORY 结构


DXGKARG \_ UPDATEPAGEDIRECTORY 结构保留供系统使用。 不要在您的驱动程序中使用它。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGKARG_UPDATEPAGEDIRECTORY {
  PVOID          pPageDirectory;
  UINT           StartIndex;
  UINT           PageTableCount;
  const DXGK_PDE *PDEArray;
} DXGKARG_UPDATEPAGEDIRECTORY;
```

<a name="members"></a>成员
-------

**pPageDirectory** 保留供系统使用。

**StartIndex** 保留供系统使用。

**PageTableCount** 保留供系统使用。

**PDEArray** 保留供系统使用。

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

 

 





