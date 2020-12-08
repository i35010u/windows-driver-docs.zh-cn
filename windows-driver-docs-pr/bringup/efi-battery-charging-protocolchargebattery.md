---
title: EFI_BATTERY_CHARGING_PROTOCOL.ChargeBattery
description: EFI_BATTERY_CHARGING_PROTOCOL.ChargeBattery
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e19655cdbe61be20a36f2a313ac0efb962a7d65
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789113"
---
# <a name="efi_battery_charging_protocolchargebattery"></a>EFI \_ 电池 \_ 充电 \_ 协议。ChargeBattery


使用最大收费为指定目标级别的主电池充电。

## <a name="syntax"></a>语法


```cpp
typedef EFI_STATUS (EFIAPI * EFI_BATTERY_CHARGING_CHARGE_BATTERY) (
    IN EFI_BATTERY_CHARGING_PROTOCOL *This,
    IN UINT32 MaximumCurrent, 
    IN UINT32 TargetStateOfCharge,
    IN EFI_BATTERY_CHARGING_COMPLETION_TOKEN *CompletionToken );
```

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
\[位于 \] EFI \_ 电池 \_ 充电协议实例的指针中 \_ 。

<a href="" id="maximumcurrent"></a>*MaximumCurrent*  
\[以 \] 可选。 可用于对主电池进行计费的最大电流。 如果为 NULL 值，则会提示实现此协议的驱动程序自行处理此类详细信息。

<a href="" id="targetstateofcharge"></a>*TargetStateOfCharge*  
\[在 " \] 目标状态" 中，在 *COMPLETIONTOKEN* 为 NULL 时，该函数将返回的主电池) 的 (SOC。 SOC 以百分比表示，100% 表示完全充电。

<a href="" id="completiontoken"></a>*CompletionToken*  
\[指向 \] 与请求的费用操作相关联的 [EFI \_ 电池 \_ 充电 \_ 完成 \_ 标记](efi-battery-charging-completion-token.md) 。

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
<td><p>参数不正确。</p></td>
</tr>
<tr class="odd">
<td><p>EFI_DEVICE_ERROR</p></td>
<td><p>物理设备报告了一个错误。</p></td>
</tr>
<tr class="even">
<td><p>EFI_NOT_READY</p></td>
<td><p>物理设备处于繁忙状态或尚未准备好处理此请求。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注


此非阻塞函数使用最大收费为指定目标级别的主电池充电。

若要检测错误， *CompletionToken* 中包含的事件类型必须是 \_ \_ 使用 **CreateEventEx** 创建的 .evt 通知信号，并且必须将 **NotifyFunction** 与 *CompletionToken* 关联为 **NotifyContext**。 状态错误代码将通过 *CompletionToken* 的 **status** 成员提供。

## <a name="requirements"></a>要求

**标头：** 用户生成

## <a name="related-topics"></a>相关主题

[EFI \_ 电池 \_ 充电 \_ 协议](efi-battery-charging-protocol.md)  

[EFI \_ 电池 \_ 充电 \_ 完成 \_ 令牌](efi-battery-charging-completion-token.md)  
