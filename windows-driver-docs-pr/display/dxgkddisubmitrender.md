---
title: DXGKDDI\_SUBMITRENDER 回调函数
description: DxgkDdiSubmitRender 函数保留供系统使用。 不会实现其在您的驱动程序中。
ms.assetid: a409f737-72e9-43b0-be81-c373b151f5d9
keywords:
- DxgkDdiSubmitRender 回调函数显示设备
- DXGKDDI_SUBMITRENDER
topic_type:
- apiref
api_name:
- DxgkDdiSubmitRender
api_location:
- Dispmprt.h
api_type:
- UserDefined
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 494a0289335c5484008a94ec88884fcf9dcbddfa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569213"
---
# <a name="dxgkddisubmitrender-callback-function"></a>DXGKDDI\_SUBMITRENDER 回调函数


\[保留供系统使用。\]

*DxgkDdiSubmitRender*函数保留供系统使用。 不会实现其在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
DXGKDDI_SUBMITRENDER DxgkDdiSubmitRender;

NTSTATUS DxgkDdiSubmitRender(
   IN_CONST_HANDLE             hContext,
   INOUT_PDXGKARG_SUBMITRENDER pSubmitRender
)
{ ... }
```

<a name="parameters"></a>Parameters
----------

*hContext*此参数保留供系统使用。

*pSubmitRender*此参数保留供系统使用。

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
<td align="left">Dispmprt.h</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

 

 





