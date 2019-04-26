---
title: EFI_BATTERY_CHARGING_PROTOCOL.ChargeBattery
description: EFI_BATTERY_CHARGING_PROTOCOL.ChargeBattery
ms.assetid: 362b812f-b64b-4b6c-84a6-61c09a60f8a3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a21f3ab95d77e144a3b4d5808e70f4e9185f7d34
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328046"
---
# <a name="efibatterychargingprotocolchargebattery"></a>EFI\_BATTERY\_CHARGING\_PROTOCOL.ChargeBattery


与最大费用当前可为指定的目标级别为主电池充电。

## <a name="syntax"></a>语法


```cpp
typedef EFI_STATUS (EFIAPI * EFI_BATTERY_CHARGING_CHARGE_BATTERY) (
    IN EFI_BATTERY_CHARGING_PROTOCOL *This,
    IN UINT32 MaximumCurrent, 
    IN UINT32 TargetStateOfCharge,
    IN EFI_BATTERY_CHARGING_COMPLETION_TOKEN *CompletionToken );
```

## <a name="parameters"></a>Parameters


<a href="" id="this"></a>*此*  
\[在中\]指向 EFI\_电池\_正在充电\_协议实例。

<a href="" id="maximumcurrent"></a>*MaximumCurrent*  
\[在\]可选。 可用于主电池充电的 mA 中的最大当前。 NULL 值会提示驱动程序实现此协议来处理此类本身的详细信息。

<a href="" id="targetstateofcharge"></a>*TargetStateOfCharge*  
\[在中\]之后，如果该函数将返回主电池的目标的费用 (SOC) 的状态*CompletionToken*为 NULL。 SOC 表示为百分比，指示完全充电的 100%。

<a href="" id="completiontoken"></a>*CompletionToken*  
\[在中\]指针，指向[EFI\_电池\_正在充电\_完成\_令牌](efi-battery-charging-completion-token.md)请求的费用操作与该键相关联。

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
<td><p>参数不正确。</p></td>
</tr>
<tr class="odd">
<td><p>EFI_DEVICE_ERROR</p></td>
<td><p>物理设备报告了错误。</p></td>
</tr>
<tr class="even">
<td><p>EFI_NOT_READY</p></td>
<td><p>物理设备是正忙还是未准备好处理此请求。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


此非阻止函数为指定的目标级别为主电池充电与最大费用当前。

若要检测错误，事件中包含的类型*CompletionToken*必须为 EVT\_通知\_信号，使用创建**CreateEventEx** ，并必须将关联**NotifyFunction**与*CompletionToken*作为**NotifyContext**。 状态错误代码将是可通过**状态**的成员*CompletionToken*。

## <a name="requirements"></a>要求

**标头：** 用户生成

## <a name="related-topics"></a>相关主题

[EFI\_电池\_正在充电\_协议](efi-battery-charging-protocol.md)  

[EFI\_电池\_正在充电\_完成\_令牌](efi-battery-charging-completion-token.md)  
