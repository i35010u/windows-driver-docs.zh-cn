---
title: DXGKCB \_ 存在 \_ DISPLAYONLY \_ 进度回调函数
description: 了解 DXGKCB 存在的 \_ \_ DISPLAYONLY \_ 进度回调函数，该函数保留供系统使用。 不要在您的驱动程序中使用它。
keywords:
- pfnPresentDisplayOnlyProgress 回调函数显示设备
- DXGKCB_PRESENT_DISPLAYONLY_PROGRESS
topic_type:
- apiref
api_name:
- pfnPresentDisplayOnlyProgress
api_location:
- D3dkmddi.h
api_type:
- UserDefined
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: d8e2abef230fbe411d3f44b167225055c249a7e5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808941"
---
# <a name="dxgkcb_present_displayonly_progress-callback-function"></a>DXGKCB \_ 存在 \_ DISPLAYONLY \_ 进度回调函数


预留给系统使用。 不要在您的驱动程序中使用它。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
DXGKCB_PRESENT_DISPLAYONLY_PROGRESS pfnPresentDisplayOnlyProgress;

void APIENTRY CALLBACK* pfnPresentDisplayOnlyProgress(
  _In_ const HANDLE                                 hAdapter,
  _In_ const DXGKARGCB_PRESENT_DISPLAYONLY_PROGRESS *pProgress
)
{ ... }
```

<a name="parameters"></a>参数
----------

*hAdapter* \[中\]

*pProgress* \[中\]

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
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">台式机</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">D3dkmddi</td>
</tr>
</tbody>
</table>

 

 





