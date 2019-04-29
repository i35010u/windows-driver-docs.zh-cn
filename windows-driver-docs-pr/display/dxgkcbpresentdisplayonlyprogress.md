---
title: DXGKCB\_存在\_DISPLAYONLY\_进度回调函数
description: 保留供系统使用。 不要使用它在您的驱动程序中。
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
ms.openlocfilehash: 67306955be711f55f169aa36727f6293e779e39d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323155"
---
# <a name="dxgkcbpresentdisplayonlyprogress-callback-function"></a>DXGKCB\_存在\_DISPLAYONLY\_进度回调函数


保留供系统使用。 不要使用它在您的驱动程序中。

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

<a name="parameters"></a>Parameters
----------

*hAdapter* \[in\]

*pProgress* \[in\]

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
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">D3dkmddi.h</td>
</tr>
</tbody>
</table>

 

 





