---
title: DxgkDdiMovePageDirectory 函数
description: DxgkDdiMovePageDirectory 函数保留供系统使用。 不会实现其在您的驱动程序中。
ms.assetid: 25972570-174d-40dc-bfbc-e9eb395dcb0e
keywords:
- DxgkDdiMovePageDirectory 函数显示设备
topic_type:
- apiref
api_name:
- DxgkDdiMovePageDirectory
api_location:
- Dispmprt.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: f326ad39f877af4d363f92373a38fdcbaacc5a0a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341111"
---
# <a name="dxgkddimovepagedirectory-function"></a>DxgkDdiMovePageDirectory 函数


\[保留供系统使用。\]

*DxgkDdiMovePageDirectory*函数保留供系统使用。 不会实现其在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
NTSTATUS APIENTRY DxgkDdiMovePageDirectory(
  _In_    CONST HANDLE              hContext,
  _Inout_ DXGKARG_MOVEPAGEDIRECTORY *pMovePageDirectory
);
```

<a name="parameters"></a>Parameters
----------

*hContext* \[中\]此参数保留供系统使用。

*pMovePageDirectory* \[in、 out\]此参数保留供系统使用。

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
<td align="left">Dispmprt.h （包括 Dispmprt.h）</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

 

 





