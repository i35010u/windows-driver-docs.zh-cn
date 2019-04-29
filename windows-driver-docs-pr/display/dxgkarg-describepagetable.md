---
title: '\_DXGKARG\_DESCRIBEPAGETABLE 结构'
description: DXGKARG\_DESCRIBEPAGETABLE 结构保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: f439ba7c-216e-4286-9a63-d8f596996ac2
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
ms.openlocfilehash: 21bdb72b5623c5cfbb4435983bb731a6ec7f5731
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379079"
---
# <a name="dxgkargdescribepagetable-structure"></a>\_DXGKARG\_DESCRIBEPAGETABLE 结构


DXGKARG\_DESCRIBEPAGETABLE 结构保留供系统使用。 不要使用它在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGKARG_DESCRIBEPAGETABLE {
  D3DGPU_VIRTUAL_ADDRESS CoverageStart;
  UINT                   CoverageSizeInBytes;
  UINT                   SizeInBytes;
  UINT                   SubtableOffset1;
  UINT                   SubtableOffset2;
} DXGKARG_DESCRIBEPAGETABLE;
```

<a name="members"></a>成员
-------

**CoverageStart**保留供系统使用。

**CoverageSizeInBytes**保留供系统使用。

**SizeInBytes**保留供系统使用。

**SubtableOffset1**保留供系统使用。

**SubtableOffset2**保留供系统使用。

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

 

 





