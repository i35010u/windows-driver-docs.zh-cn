---
title: '\_DXGKARG \_ SUBMITRENDER 结构'
description: DXGKARG \_ SUBMITRENDER 结构保留供系统使用。 不要在您的驱动程序中使用它。
keywords:
- _DXGKARG_SUBMITRENDER 结构显示设备
- DXGKARG_SUBMITRENDER 结构显示设备
topic_type:
- apiref
api_name:
- DXGKARG_SUBMITRENDER
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: e4d9ff9d1adf14ebca76de43b845968d41d9ab55
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808969"
---
# <a name="_dxgkarg_submitrender-structure"></a>\_DXGKARG \_ SUBMITRENDER 结构


DXGKARG \_ SUBMITRENDER 结构保留供系统使用。 不要在您的驱动程序中使用它。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGKARG_SUBMITRENDER {
  VOID                   *pContextSaveArea;
  D3DGPU_VIRTUAL_ADDRESS DmaBuffer;
  UINT                   DmaSize;
  VOID                   *pPrivateDriverData;
  UINT                   PrivateDriverDataSize;
  VOID                   *pDmaBufferPrivateData;
  UINT                   DmaBufferPrivateDataSize;
  VOID                   *pDmaBuffer;
} DXGKARG_SUBMITRENDER;
```

<a name="members"></a>成员
-------

**pContextSaveArea** 保留供系统使用。

**DmaBuffer** 保留供系统使用。

**DmaSize** 保留供系统使用。

**pPrivateDriverData** 保留供系统使用。

**PrivateDriverDataSize** 保留供系统使用。

**pDmaBufferPrivateData** 保留供系统使用。

**DmaBufferPrivateDataSize** 保留供系统使用。

**pDmaBuffer** 保留供系统使用。

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

 

 





