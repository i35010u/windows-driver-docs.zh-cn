---
title: EFI_DISPLAY_POWER_PROTOCOL.GetDisplayPowerState
description: EFI_DISPLAY_POWER_PROTOCOL.GetDisplayPowerState
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24125342c99e122d490297a6b4552c2fc9bbc496
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789109"
---
# <a name="efi_display_power_protocolgetdisplaypowerstate"></a>EFI \_ 显示 \_ 电源 \_ 协议。GetDisplayPowerState


返回显示器和背景光的当前电源状态。

## <a name="syntax"></a>语法


```cpp
typedef EFI_STATUS (EFIAPI * EFI_DISPLAY_POWER_GETDISPLAYPOWERSTATE) (
    IN EFI_DISPLAY_POWER_PROTOCOL *This,
    OUT EFI_DISPLAY_POWER_STATE *PowerState 
    );
```

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
\[位于 \] [EFI \_ 显示 \_ 电源 \_ 协议](efi-display-power-protocol.md) 实例的指针中。

<a href="" id="powerstate"></a>*PowerState*  
\[out \] 一个指针，指向用于接收当前电源状态的 [EFI \_ 显示 \_ 电源 \_ 状态](efi-display-power-state.md) 值。

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
<td><p>函数已成功返回。</p></td>
</tr>
<tr class="even">
<td><p>EFI_INVALID_PARAMETER</p></td>
<td><p>参数无效。</p></td>
</tr>
<tr class="odd">
<td><p>EFI_DEVICE_ERROR</p></td>
<td><p>物理设备报告了一个错误。</p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要求


**标头：** 用户生成

## <a name="related-topics"></a>相关主题
[EFI \_ 显示 \_ 电源 \_ 协议](efi-display-power-protocol.md)  



