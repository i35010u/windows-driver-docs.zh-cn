---
title: EFI_DISPLAY_POWER_PROTOCOL.SetDisplayPowerState
description: EFI_DISPLAY_POWER_PROTOCOL.SetDisplayPowerState
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 954a11e6c0ed0997ee0c09f60af6da26e1bd8c2e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803407"
---
# <a name="efi_display_power_protocolsetdisplaypowerstate"></a>EFI \_ 显示 \_ 电源 \_ 协议。SetDisplayPowerState


修改显示器和背光的电源状态。

## <a name="syntax"></a>语法


```cpp
typedef EFI_STATUS (EFIAPI * EFI_DISPLAY_POWER_SETDISPLAYPOWERSTATE) (
    IN EFI_DISPLAY_POWER_PROTOCOL *This,
    IN EFI_DISPLAY_POWER_STATE PowerState 
    );
```

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
\[位于 \] [EFI \_ 显示 \_ 电源 \_ 协议](efi-display-power-protocol.md) 实例的指针中。

<a href="" id="powerstate"></a>*PowerState*  
\[在 \] [EFI \_ 显示 \_ 电源 \_ 状态](efi-display-power-state.md) 值中，指定要设置的新电源状态。

## <a name="return-value"></a>返回值


返回以下状态代码之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EFI_SUCCESS</p></td>
<td><p>此函数在更改显示和背光的电源状态后成功返回。</p></td>
</tr>
<tr class="even">
<td><p>EFI_INVALID_PARAMETER</p></td>
<td><p>参数不正确。</p></td>
</tr>
<tr class="odd">
<td><p>EFI_DEVICE_ERROR</p></td>
<td><p>物理设备报告了一个错误。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


此函数不会对显示或背景光以外的任何硬件组件产生任何影响。

此函数必须允许冗余调用，而不会返回错误代码。 对于具有相同 *PowerState* 参数的此函数的多个调用，必须返回 success。 在处理冗余调用时，此函数的实现应避免不必要的工作。

## <a name="requirements"></a>要求


**标头：** 用户生成

## <a name="related-topics"></a>相关主题
[EFI \_ 显示 \_ 电源 \_ 协议](efi-display-power-protocol.md)  



