---
title: DXGKDDI\_CREATEALLOCATION2 回调函数
description: DxgkDdiCreateAllocation2 函数保留供系统使用。 不会实现其在您的驱动程序中。
ms.assetid: c22e176e-cde5-4edf-8f53-1d7874c7d5da
keywords:
- DxgkDdiCreateAllocation2 回调函数显示设备
- DXGKDDI_CREATEALLOCATION2
topic_type:
- apiref
api_name:
- DxgkDdiCreateAllocation2
api_location:
- Dispmprt.h
api_type:
- UserDefined
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: dfcd61d26e5d7bd0730acc3fc717120a833c83e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569218"
---
# <a name="dxgkddicreateallocation2-callback-function"></a>DXGKDDI\_CREATEALLOCATION2 回调函数


\[保留供系统使用。\]

*DxgkDdiCreateAllocation2*函数保留供系统使用。 不会实现其在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
DXGKDDI_CREATEALLOCATION2 DxgkDdiCreateAllocation2;

NTSTATUS DxgkDdiCreateAllocation2(
   IN_CONST_HANDLE                  hAdapter,
   INOUT_PDXGKARG_CREATEALLOCATION2 pCreateAllocation
)
{ ... }
```

<a name="parameters"></a>Parameters
----------

*hAdapter*此参数保留供系统使用。

*pCreateAllocation*此参数保留供系统使用。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows 7 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Dispmprt.h （包括 D3dkmddi.h）</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

 

 





