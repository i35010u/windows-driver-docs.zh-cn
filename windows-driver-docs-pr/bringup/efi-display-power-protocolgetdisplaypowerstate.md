---
title: EFI_DISPLAY_POWER_PROTOCOL.GetDisplayPowerState
description: EFI_DISPLAY_POWER_PROTOCOL.GetDisplayPowerState
ms.assetid: 8c5fe55f-903e-4ef0-b3cf-8b764af767cf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46d6f29f8c91834a95b7cdeb9a1aa1bf6c391e94
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328013"
---
# <a name="efidisplaypowerprotocolgetdisplaypowerstate"></a>EFI\_DISPLAY\_POWER\_PROTOCOL.GetDisplayPowerState


返回当前的显示和背景光电源状态。

## <a name="syntax"></a>语法


```cpp
typedef EFI_STATUS (EFIAPI * EFI_DISPLAY_POWER_GETDISPLAYPOWERSTATE) (
    IN EFI_DISPLAY_POWER_PROTOCOL *This,
    OUT EFI_DISPLAY_POWER_STATE *PowerState 
    );
```

## <a name="parameters"></a>Parameters


<a href="" id="this"></a>*此*  
\[在中\]指向的指针[EFI\_显示\_POWER\_协议](efi-display-power-protocol.md)实例。

<a href="" id="powerstate"></a>*PowerState*  
\[out\]指向的指针[EFI\_显示\_POWER\_状态](efi-display-power-state.md)接收的当前电源状态的值。

## <a name="return-value"></a>返回值


返回一个下面的状态代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EFI_SUCCESS</p></td>
<td><p>该函数返回成功。</p></td>
</tr>
<tr class="even">
<td><p>EFI_INVALID_PARAMETER</p></td>
<td><p>参数无效。</p></td>
</tr>
<tr class="odd">
<td><p>EFI_DEVICE_ERROR</p></td>
<td><p>物理设备报告了错误。</p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要求


**标头：** 用户生成

## <a name="related-topics"></a>相关主题
[EFI\_DISPLAY\_电源\_协议](efi-display-power-protocol.md)  



