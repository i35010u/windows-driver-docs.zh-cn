---
title: '\_DXGKARG\_SUBMITRENDER 结构'
description: DXGKARG\_SUBMITRENDER 结构保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: eecc3c47-1387-4fca-9113-12dfedc58e80
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
ms.openlocfilehash: 15032e403895e5cf45a3e656f5caf15e000cfc89
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562665"
---
# <a name="dxgkargsubmitrender-structure"></a>\_DXGKARG\_SUBMITRENDER 结构


DXGKARG\_SUBMITRENDER 结构保留供系统使用。 不要使用它在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DXGKARG_SUBMITRENDER {
  VOID                   *pContextSaveArea;
  D3DGPU_VIRTUAL_ADDRESS DmaBuffer;
  UINT                   DmaSize;
  VOID                   *pPrivateDriverData;
  UINT                   PrivateDriverDataSize;
  VOID                   *pDmaBufferPrivateData;
  UINT                   DmaBufferPrivateDataSize;
  VOID                   *pDmaBuffer;
} DXGKARG_SUBMITRENDER;
```

<a name="members"></a>成员
-------

**pContextSaveArea**保留供系统使用。

**Dma 缓冲区**保留供系统使用。

**DmaSize**保留供系统使用。

**pPrivateDriverData**保留供系统使用。

**PrivateDriverDataSize**保留供系统使用。

**pDmaBufferPrivateData**保留供系统使用。

**DmaBufferPrivateDataSize**保留供系统使用。

**pDmaBuffer**保留供系统使用。

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

 

 





