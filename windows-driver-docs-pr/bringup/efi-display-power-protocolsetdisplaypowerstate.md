---
title: EFI_DISPLAY_POWER_PROTOCOL.SetDisplayPowerState
description: EFI_DISPLAY_POWER_PROTOCOL.SetDisplayPowerState
ms.assetid: ee638d05-4d0e-45b0-a733-73923a7c045a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7504bbe3f16cdd33fdd9f33803be203be0c0c5c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328011"
---
# <a name="efidisplaypowerprotocolsetdisplaypowerstate"></a>EFI\_DISPLAY\_POWER\_PROTOCOL.SetDisplayPowerState


修改显示和背景光电源的状态。

## <a name="syntax"></a>语法


```cpp
typedef EFI_STATUS (EFIAPI * EFI_DISPLAY_POWER_SETDISPLAYPOWERSTATE) (
    IN EFI_DISPLAY_POWER_PROTOCOL *This,
    IN EFI_DISPLAY_POWER_STATE PowerState 
    );
```

## <a name="parameters"></a>Parameters


<a href="" id="this"></a>*此*  
\[在中\]指向的指针[EFI\_显示\_POWER\_协议](efi-display-power-protocol.md)实例。

<a href="" id="powerstate"></a>*PowerState*  
\[在中\] [EFI\_显示\_POWER\_状态](efi-display-power-state.md)值，该值指定要设置的新电源状态。

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
<td><p>成功返回后更改的显示和背景光的电源状态的函数。</p></td>
</tr>
<tr class="even">
<td><p>EFI_INVALID_PARAMETER</p></td>
<td><p>参数不正确。</p></td>
</tr>
<tr class="odd">
<td><p>EFI_DEVICE_ERROR</p></td>
<td><p>物理设备报告了错误。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


此函数应显示或背景光以外的任何硬件组件上没有任何影响。

此函数必须允许的冗余调用，而不返回错误代码。 多个调用此函数具有相同*PowerState*参数必须返回成功。 处理的冗余调用时，此函数的实现应避免不必要的工作。

## <a name="requirements"></a>要求


**标头：** 用户生成

## <a name="related-topics"></a>相关主题
[EFI\_DISPLAY\_电源\_协议](efi-display-power-protocol.md)  



