---
title: '\_DXGKARG \_ CREATEALLOCATION2 结构'
description: DXGKARG \_ CREATEALLOCATION2 结构保留供系统使用。 不要在您的驱动程序中使用它。
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
ms.openlocfilehash: 10742610f093d6b5f701547b1ad409530bc72c7a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808981"
---
# <a name="_dxgkarg_createallocation2-structure"></a>\_DXGKARG \_ CREATEALLOCATION2 结构


DXGKARG \_ CREATEALLOCATION2 结构保留供系统使用。 不要在您的驱动程序中使用它。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGKARG_CREATEALLOCATION2 {
  const VOID                  *pPrivateDriverData;
  UINT                        PrivateDriverDataSize;
  UINT                        NumAllocations;
  DXGK_ALLOCATIONINFO2        *pAllocationInfo;
  HANDLE                      hResource;
  DXGK_CREATEALLOCATIONFLAGS2 Flags;
} DXGKARG_CREATEALLOCATION2;
```

<a name="members"></a>成员
-------

**pPrivateDriverData** 保留供系统使用。

**PrivateDriverDataSize** 保留供系统使用。

**NumAllocations** 保留供系统使用。

**pAllocationInfo** 保留供系统使用。

**hResource** 保留供系统使用。

**标志** 保留供系统使用。

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

 

 





