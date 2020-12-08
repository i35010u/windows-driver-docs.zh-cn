---
title: DXGKDDI \_ DESCRIBEPAGETABLE 回调函数
description: DxgkDdiDescribePageTable 函数保留供系统使用。 不要在您的驱动程序中实现它。
keywords:
- DxgkDdiDescribePageTable 回调函数显示设备
- DXGKDDI_DESCRIBEPAGETABLE
topic_type:
- apiref
api_name:
- DxgkDdiDescribePageTable
api_location:
- Dispmprt.h
api_type:
- UserDefined
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 206365d706e4ecff782b607368bf23d34f18f070
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808935"
---
# <a name="dxgkddi_describepagetable-callback-function"></a>DXGKDDI \_ DESCRIBEPAGETABLE 回调函数


\[预留给系统使用。\]

*DxgkDdiDescribePageTable* 函数保留供系统使用。 不要在您的驱动程序中实现它。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
DXGKDDI_DESCRIBEPAGETABLE DxgkDdiDescribePageTable;

NTSTATUS DxgkDdiDescribePageTable(
   IN_CONST_HANDLE                  hDevice,
   INOUT_PDXGKARG_DESCRIBEPAGETABLE pDescribePageTable
)
{ ... }
```

<a name="parameters"></a>参数
----------

*hDevice* 此参数保留供系统使用。

*pDescribePageTable* 此参数保留供系统使用。

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
<td align="left">Dispmprt (包含 Dispmprt) </td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

 

 





