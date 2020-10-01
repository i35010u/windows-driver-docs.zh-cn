---
title: DXGKCB \_ COMPLETEPSTATETRANSITION 回调函数
description: 了解 DXGKCB \_ COMPLETEPSTATETRANSITION 回调函数，该函数保留供系统使用。 不要在您的驱动程序中使用它。
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
ms.openlocfilehash: 926b0f1b6eaaa6fa4372f2bb43a8cd67db50681a
ms.sourcegitcommit: fc94eb0d5a41ef81c1b3ab91ad725386db0be0c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91603690"
---
# <a name="dxgkcb_completepstatetransition-callback-function"></a>DXGKCB \_ COMPLETEPSTATETRANSITION 回调函数


预留给系统使用。 不要在您的驱动程序中使用它。

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

<a name="parameters"></a>parameters
----------

*hAdapter* \[中\]

*ComponentIndex* \[中\]

*CompletedPState* \[中\]

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
<td align="left">D3dkmddi (包含 D3dkmddi) </td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= DISPATCH_LEVEL</p></td>
</tr>
</tbody>
</table>

 

 





