---
title: DXGKDDISETPOWERPSTATE 回调函数
description: 了解 DXGKDDISETPOWERPSTATE 回调函数，该函数保留供系统使用。 不要在您的驱动程序中使用它。
ms.assetid: 58DB4615-BD52-4003-8D60-0881E87C7BD3
keywords:
- DxgkDdiSetPowerPState 回调函数显示设备
- DXGKDDISETPOWERPSTATE
topic_type:
- apiref
api_name:
- DxgkDdiSetPowerPState
api_location:
- D3dkmddi.h
api_type:
- UserDefined
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3ad97add6b7a1b9170a36d7371d1bfdc2a63e582
ms.sourcegitcommit: fc94eb0d5a41ef81c1b3ab91ad725386db0be0c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91603643"
---
# <a name="dxgkddisetpowerpstate-callback-function"></a>DXGKDDISETPOWERPSTATE 回调函数


预留给系统使用。 不要在您的驱动程序中使用它。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
DXGKDDISETPOWERPSTATE DxgkDdiSetPowerPState;

NTSTATUS APIENTRY DxgkDdiSetPowerPState(
  _In_ const HANDLE DriverContext,
  _In_       UINT   ComponentIndex,
  _In_       UINT   RequestedComponentPState
)
{ ... }
```

<a name="parameters"></a>parameters
----------

*DriverContext* \[中\]

*ComponentIndex* \[中\]

*RequestedComponentPState* \[中\]

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>最低受支持的客户端</p></td>
<td align="left"><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">桌面型</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">D3dkmddi</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

 

 





