---
title: DXGKCB\_COMPLETEPSTATETRANSITION 回调函数
description: 保留供系统使用。 不要使用它在您的驱动程序中。
ms.assetid: F0EF1B1F-58C3-4D6D-BF9A-0621CC82ED6B
keywords:
- DxgkCbCompletePStateTransition 回调函数显示设备
- DXGKCB_COMPLETEPSTATETRANSITION
topic_type:
- apiref
api_name:
- DxgkCbCompletePStateTransition
api_location:
- D3dkmddi.h
api_type:
- UserDefined
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 58b1f3961f8ca78a1fb625b079315dfc23b69b96
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569217"
---
# <a name="dxgkcbcompletepstatetransition-callback-function"></a>DXGKCB\_COMPLETEPSTATETRANSITION 回调函数


保留供系统使用。 不要使用它在您的驱动程序中。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
DXGKCB_COMPLETEPSTATETRANSITION DxgkCbCompletePStateTransition;

VOID APIENTRY CALLBACK* DxgkCbCompletePStateTransition(
  _In_ const HANDLE hAdapter,
  _In_       UINT   ComponentIndex,
  _In_       UINT   CompletedPState
)
{ ... }
```

<a name="parameters"></a>Parameters
----------

*hAdapter* \[in\]

*ComponentIndex* \[in\]

*CompletedPState* \[in\]

<a name="return-value"></a>返回值
------------

此回调函数不返回值。

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
<td align="left"><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">D3dkmddi.h （包括 D3dkmddi.h）</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;=DISPATCH_LEVEL</p></td>
</tr>
</tbody>
</table>

 

 





