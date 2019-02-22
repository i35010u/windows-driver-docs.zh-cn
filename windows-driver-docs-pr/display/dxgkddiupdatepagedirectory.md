---
title: DxgkDdiUpdatePageDirectory 函数
description: DxgkDdiUpdatePageDirectory 函数保留供系统使用。 不会实现其在您的驱动程序中。
ms.assetid: 91f81165-a63c-44bb-8898-9cc85c2a6e45
keywords:
- DxgkDdiUpdatePageDirectory 函数显示设备
topic_type:
- apiref
api_name:
- DxgkDdiUpdatePageDirectory
api_location:
- Dispmprt.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 138ae874d0a1935c65c7d80462537615a0c36244
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544824"
---
# <a name="dxgkddiupdatepagedirectory-function"></a>DxgkDdiUpdatePageDirectory 函数


\[保留供系统使用。\]

*DxgkDdiUpdatePageDirectory*函数保留供系统使用。 不会实现其在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
NTSTATUS APIENTRY DxgkDdiUpdatePageDirectory(
   IN_CONST_HANDLE                    hDevice,
   INOUT_PDXGKARG_UPDATEPAGEDIRECTORY pUpdatePageDirectory
);
```

<a name="parameters"></a>参数
----------

*hDevice*此参数保留供系统使用。

*pUpdatePageDirectory*此参数保留供系统使用。

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
<td align="left"><p>标头</p></td>
<td align="left">Dispmprt.h （包括 Dispmprt.h）</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

 

 





