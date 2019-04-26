---
title: '\_DXGK\_DMABUFFERCAPS 结构'
description: DXGK\_DMABUFFERCAPS 结构保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: 57ccc0e6-eacf-48a2-a9a1-cb7e43850caa
keywords:
- _DXGK_DMABUFFERCAPS 结构显示设备
- DXGK_DMABUFFERCAPS 结构显示设备
topic_type:
- apiref
api_name:
- DXGK_DMABUFFERCAPS
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: d4caf3c18a133580b5479219b25897a09f374fdf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327110"
---
# <a name="dxgkdmabuffercaps-structure"></a>\_DXGK\_DMABUFFERCAPS 结构


DXGK\_DMABUFFERCAPS 结构保留供系统使用。 不要使用它在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGK_DMABUFFERCAPS {
  struct {
    UINT Size;
    UINT PrivateDriverDataSize;
    UINT SegmentId;
    UINT AllocationGroup;
    UINT Reserved[16];
  } PresentDmaBuffer;
  struct {
    UINT Size;
    UINT PrivateDriverDataSize;
    UINT SegmentId;
    UINT AllocationGroup;
    UINT Reserved[16];
  } PagingDmaBuffer;
} DXGK_DMABUFFERCAPS;
```

<a name="members"></a>成员
-------

**PresentDmaBuffer**

**PagingDmaBuffer**

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

 

 





