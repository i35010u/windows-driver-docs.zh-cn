---
title: '\_DXGKARG \_ DESCRIBEPAGETABLE 结构'
description: DXGKARG \_ DESCRIBEPAGETABLE 结构保留供系统使用。 不要在您的驱动程序中使用它。
keywords:
- _DXGKARG_DESCRIBEPAGETABLE 结构显示设备
- DXGKARG_DESCRIBEPAGETABLE 结构显示设备
topic_type:
- apiref
api_name:
- DXGKARG_DESCRIBEPAGETABLE
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: fda1abaea9a4d79b40f71b9f5a7dfc9a908fda29
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808973"
---
# <a name="_dxgkarg_describepagetable-structure"></a>\_DXGKARG \_ DESCRIBEPAGETABLE 结构


DXGKARG \_ DESCRIBEPAGETABLE 结构保留供系统使用。 不要在您的驱动程序中使用它。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGKARG_DESCRIBEPAGETABLE {
  D3DGPU_VIRTUAL_ADDRESS CoverageStart;
  UINT                   CoverageSizeInBytes;
  UINT                   SizeInBytes;
  UINT                   SubtableOffset1;
  UINT                   SubtableOffset2;
} DXGKARG_DESCRIBEPAGETABLE;
```

<a name="members"></a>成员
-------

**CoverageStart** 保留供系统使用。

**CoverageSizeInBytes** 保留供系统使用。

**SizeInBytes** 保留供系统使用。

**SubtableOffset1** 保留供系统使用。

**SubtableOffset2** 保留供系统使用。

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

 

 





