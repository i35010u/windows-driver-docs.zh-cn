---
title: '\_DXGKARG\_CREATEALLOCATION2 结构'
description: DXGKARG\_CREATEALLOCATION2 结构保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: 4796f378-78e0-4119-9ab4-d25d61fca7de
keywords:
- _DXGKARG_CREATEALLOCATION2 结构显示设备
- DXGKARG_CREATEALLOCATION2 结构显示设备
topic_type:
- apiref
api_name:
- DXGKARG_CREATEALLOCATION2
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0a3ce3bafca4808e0df527a8e4359ebfee8314ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522674"
---
# <a name="dxgkargcreateallocation2-structure"></a>\_DXGKARG\_CREATEALLOCATION2 结构


DXGKARG\_CREATEALLOCATION2 结构保留供系统使用。 不要使用它在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGKARG_CREATEALLOCATION2 {
  const VOID                  *pPrivateDriverData;
  UINT                        PrivateDriverDataSize;
  UINT                        NumAllocations;
  DXGK_ALLOCATIONINFO2        *pAllocationInfo;
  HANDLE                      hResource;
  DXGK_CREATEALLOCATIONFLAGS2 Flags;
} DXGKARG_CREATEALLOCATION2;
```

<a name="members"></a>成员
-------

**pPrivateDriverData**保留供系统使用。

**PrivateDriverDataSize**保留供系统使用。

**NumAllocations**保留供系统使用。

**pAllocationInfo**保留供系统使用。

**hResource**保留供系统使用。

**标志**保留供系统使用。

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
<td align="left"><p>标头</p></td>
<td align="left">D3dkmddi.h （包括 D3dkmddi.h）</td>
</tr>
</tbody>
</table>

 

 





