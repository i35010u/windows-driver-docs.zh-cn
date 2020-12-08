---
title: '\_DXGK \_ DMABUFFERCAPS 结构'
description: DXGK \_ DMABUFFERCAPS 结构保留供系统使用。 不要在您的驱动程序中使用它。
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
ms.openlocfilehash: 5c78bc02f839c199fb290dc6dd245f6e6b5350e8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809039"
---
# <a name="_dxgk_dmabuffercaps-structure"></a>\_DXGK \_ DMABUFFERCAPS 结构


DXGK \_ DMABUFFERCAPS 结构保留供系统使用。 不要在您的驱动程序中使用它。

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
  } PresentDmaBuffer;
  struct {
    UINT Size;
    UINT PrivateDriverDataSize;
    UINT SegmentId;
    UINT AllocationGroup;
    UINT Reserved[16];
  } PagingDmaBuffer;
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
<td align="left"><p>版本</p></td>
<td align="left"><p>在 windows 7 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">D3dkmddi (包含 D3dkmddi) </td>
</tr>
</tbody>
</table>

 

 





