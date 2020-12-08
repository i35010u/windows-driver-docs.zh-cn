---
title: EFI_BATTERY_CHARGING_PROTOCOL.GetBatteryStatus
description: EFI_BATTERY_CHARGING_PROTOCOL.GetBatteryStatus
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c119ef8b1d00941a5528b00d8baa9c85b374b29
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789115"
---
# <a name="efi_battery_charging_protocolgetbatterystatus"></a>EFI \_ 电池 \_ 充电 \_ 协议。GetBatteryStatus


返回有关主电池的当前状态的信息。

## <a name="syntax"></a>语法


```cpp
typedef EFI_STATUS (EFIAPI * EFI_BATTERY_CHARGING_GET_BATTERY_STATUS) (
    IN EFI_BATTERY_CHARGING_PROTOCOL *This,
    OUT UINT32 *StateOfCharge,
    OUT UINT32 *RatedCapacity,
    OUT INT32 *ChargeCurrent );
```

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
\[位于 \] EFI \_ 电池 \_ 充电协议实例的指针中 \_ 。

<a href="" id="stateofcharge"></a>*StateOfCharge*  
\[out \] 返回主电池 (SOC) 的当前充电状态。 SOC 以百分比表示，100% 表示完全充电。

<a href="" id="ratedcapacity"></a>*RatedCapacity*  
\[out \] 返回 mAh 中的额定容量容量。

<a href="" id="chargecurrent"></a>*ChargeCurrent*  
\[\]如果电池正在充电，则返回一个正数，指示当前已发送到 mA 中的电池。 如果电池正在放电，将返回一个负数，指示当前正在使用 mA 中的电池进行绘制。 如果电池不会充电，也不会放电，则返回0。 如果硬件无法提供此信息，它将返回 \_ \_ \_ \_ (0x80000000) 不支持的 EFI 电池电量电流 \_ 。

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


此函数将返回额定容量和电量 (SOC) 用于主电池。 定期调用此函数，以帮助实现此协议的驱动程序进行额外处理。

## <a name="requirements"></a>要求


**标头：** 用户生成

## <a name="related-topics"></a>相关主题
[EFI \_ 电池 \_ 充电 \_ 协议](efi-battery-charging-protocol.md)  



