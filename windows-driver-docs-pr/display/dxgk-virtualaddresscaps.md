---
title: '\_DXGK\_VIRTUALADDRESSCAPS 结构'
description: DXGK\_VIRTUALADDRESSCAPS 结构保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: 45a33031-26ca-4477-9be0-2066927506cf
keywords:
- _DXGK_VIRTUALADDRESSCAPS 结构显示设备
- DXGK_VIRTUALADDRESSCAPS 结构显示设备
topic_type:
- apiref
api_name:
- DXGK_VIRTUALADDRESSCAPS
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: fcba07e6797789f5251077f8f1023ef3ab909b6b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392024"
---
# <a name="dxgkvirtualaddresscaps-structure"></a>\_DXGK\_VIRTUALADDRESSCAPS 结构


DXGK\_VIRTUALADDRESSCAPS 结构保留供系统使用。 不要使用它在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGK_VIRTUALADDRESSCAPS {
  union {
    struct {
      UINT PrivilegedMemorySupported  :1;
      UINT ReadOnlyMemorySupported  :1;
      UINT Reserved  :30;
    };
    UINT Value;
  };
  UINT VirtualAddressBitCount;
  UINT PageTableCoverageBitCount;
  UINT PageDirectoryEntrySize;
  UINT PageDirectorySegment;
  UINT PageTableSegment;
  UINT IdealGPUPageSize;
} DXGK_VIRTUALADDRESSCAPS;
```

<a name="members"></a>成员
-------

**PrivilegedMemorySupported**保留供系统使用。

**ReadOnlyMemorySupported**保留供系统使用。

**保留**保留供系统使用。

**值**保留供系统使用。

**VirtualAddressBitCount**保留供系统使用。

**PageTableCoverageBitCount**保留供系统使用。

**PageDirectoryEntrySize**保留供系统使用。

**PageDirectorySegment**保留供系统使用。

**PageTableSegment**保留供系统使用。

**IdealGPUPageSize**保留供系统使用。

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

 

 





