---
title: DXGKCB \_ 存在 \_ DISPLAYONLY \_ 进度回调函数
description: 了解 DXGKCB 存在的 \_ \_ DISPLAYONLY \_ 进度回调函数，该函数保留供系统使用。 不要在您的驱动程序中使用它。
ms.assetid: 8970246b-b46f-464f-93b2-973cc351ed07
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
ms.openlocfilehash: 2bf3a3ad0e0acb51b36f74580b7c4b78a1d90537
ms.sourcegitcommit: fc94eb0d5a41ef81c1b3ab91ad725386db0be0c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91603565"
---
# <a name="dxgkcb_present_displayonly_progress-callback-function"></a>DXGKCB \_ 存在 \_ DISPLAYONLY \_ 进度回调函数


预留给系统使用。 不要在您的驱动程序中使用它。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
DXGKCB_PRESENT_DISPLAYONLY_PROGRESS pfnPresentDisplayOnlyProgress;

void APIENTRY CALLBACK* pfnPresentDisplayOnlyProgress(
  _In_ const HANDLE                                 hAdapter,
  _In_ const DXGKARGCB_PRESENT_DISPLAYONLY_PROGRESS *pProgress
)
{ ... }
```

<a name="parameters"></a>parameters
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
<td align="left">桌面型</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">D3dkmddi</td>
</tr>
</tbody>
</table>

 

 





