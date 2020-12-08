---
title: DxgkDdiMovePageDirectory 函数
description: DxgkDdiMovePageDirectory 函数保留供系统使用。 不要在您的驱动程序中实现它。
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
ms.openlocfilehash: 5ed20e1e12773215f949316c08970f5d9ccb9e64
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808933"
---
# <a name="dxgkddimovepagedirectory-function"></a>DxgkDdiMovePageDirectory 函数


\[预留给系统使用。\]

*DxgkDdiMovePageDirectory* 函数保留供系统使用。 不要在您的驱动程序中实现它。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
NTSTATUS APIENTRY DxgkDdiMovePageDirectory(
  _In_    CONST HANDLE              hContext,
  _Inout_ DXGKARG_MOVEPAGEDIRECTORY *pMovePageDirectory
);
```

<a name="parameters"></a>参数
----------

*hContext* \[在中， \] 此参数保留供系统使用。

*pMovePageDirectory* \[在中， \] 此参数保留供系统使用。

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

 

 





