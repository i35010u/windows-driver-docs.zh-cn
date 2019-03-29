---
title: DXGKDDI\_DESCRIBEPAGETABLE 回调函数
description: DxgkDdiDescribePageTable 函数保留供系统使用。 不会实现其在您的驱动程序中。
ms.assetid: af9c9515-0225-4a97-bb8e-8ff9b57ac1a9
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
ms.openlocfilehash: 525b353f1b57e0fe06c6c388d6b22d23e20a61ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569214"
---
# <a name="dxgkddidescribepagetable-callback-function"></a>DXGKDDI\_DESCRIBEPAGETABLE 回调函数


\[保留供系统使用。\]

*DxgkDdiDescribePageTable*函数保留供系统使用。 不会实现其在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
DXGKDDI_DESCRIBEPAGETABLE DxgkDdiDescribePageTable;

NTSTATUS DxgkDdiDescribePageTable(
   IN_CONST_HANDLE                  hDevice,
   INOUT_PDXGKARG_DESCRIBEPAGETABLE pDescribePageTable
)
{ ... }
```

<a name="parameters"></a>Parameters
----------

*hDevice*此参数保留供系统使用。

*pDescribePageTable*此参数保留供系统使用。

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
<td align="left">Dispmprt.h （包括 Dispmprt.h）</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

 

 





