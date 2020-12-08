---
title: DXGKDDI \_ CREATEALLOCATION2 回调函数
description: DxgkDdiCreateAllocation2 函数保留供系统使用。 不要在您的驱动程序中实现它。
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
ms.openlocfilehash: 52024d9243f6b93323156e76c0f0de2667762d84
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808939"
---
# <a name="dxgkddi_createallocation2-callback-function"></a>DXGKDDI \_ CREATEALLOCATION2 回调函数


\[预留给系统使用。\]

*DxgkDdiCreateAllocation2* 函数保留供系统使用。 不要在您的驱动程序中实现它。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
DXGKDDI_CREATEALLOCATION2 DxgkDdiCreateAllocation2;

NTSTATUS DxgkDdiCreateAllocation2(
   IN_CONST_HANDLE                  hAdapter,
   INOUT_PDXGKARG_CREATEALLOCATION2 pCreateAllocation
)
{ ... }
```

<a name="parameters"></a>参数
----------

*hAdapter* 此参数保留供系统使用。

*pCreateAllocation* 此参数保留供系统使用。

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
<td align="left">台式机</td>
</tr>
<tr class="even">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 windows 7 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Dispmprt (包含 D3dkmddi) </td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

 

 





