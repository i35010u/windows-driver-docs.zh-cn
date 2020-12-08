---
title: DxgkDdiUpdatePageDirectory 函数
description: DxgkDdiUpdatePageDirectory 函数保留供系统使用。 不要在您的驱动程序中实现它。
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
ms.openlocfilehash: c459dca806453dd8f559a92387254061df3f3297
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808923"
---
# <a name="dxgkddiupdatepagedirectory-function"></a>DxgkDdiUpdatePageDirectory 函数


\[预留给系统使用。\]

*DxgkDdiUpdatePageDirectory* 函数保留供系统使用。 不要在您的驱动程序中实现它。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
NTSTATUS APIENTRY DxgkDdiUpdatePageDirectory(
   IN_CONST_HANDLE                    hDevice,
   INOUT_PDXGKARG_UPDATEPAGEDIRECTORY pUpdatePageDirectory
);
```

<a name="parameters"></a>参数
----------

*hDevice* 此参数保留供系统使用。

*pUpdatePageDirectory* 此参数保留供系统使用。

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

 

 





