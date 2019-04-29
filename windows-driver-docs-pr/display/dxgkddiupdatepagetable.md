---
title: DXGKDDI\_UPDATEPAGETABLE 回调函数
description: DxgkDdiUpdatePageTable 函数保留供系统使用。 不会实现其在您的驱动程序中。
ms.assetid: 08328e82-d1cc-4c50-bc96-7382232676ab
keywords:
- DxgkDdiUpdatePageTable 回调函数显示设备
- DXGKDDI_UPDATEPAGETABLE
topic_type:
- apiref
api_name:
- DxgkDdiUpdatePageTable
api_location:
- Dispmprt.h
api_type:
- UserDefined
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 332293a5255408a07f1895ec68b316451733652e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323271"
---
# <a name="dxgkddiupdatepagetable-callback-function"></a>DXGKDDI\_UPDATEPAGETABLE 回调函数


\[保留供系统使用。\]

*DxgkDdiUpdatePageTable*函数保留供系统使用。 不会实现其在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
DXGKDDI_UPDATEPAGETABLE DxgkDdiUpdatePageTable;

NTSTATUS DxgkDdiUpdatePageTable(
   IN_CONST_HANDLE                hDevice,
   INOUT_PDXGKARG_UPDATEPAGETABLE pUpdatePageTable
)
{ ... }
```

<a name="parameters"></a>Parameters
----------

*hDevice*此参数保留供系统使用。

*pUpdatePageTable*此参数保留供系统使用。

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
<td align="left"><p>Version</p></td>
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

 

 





