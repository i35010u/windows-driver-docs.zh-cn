---
title: EFI_BATTERY_CHARGING_PROTOCOL.GetBatteryStatus
description: EFI_BATTERY_CHARGING_PROTOCOL.GetBatteryStatus
ms.assetid: dc2b647b-b3b6-4d85-9faf-9e401fa67571
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6159f4fea5db4361067d0ec066a5574b9f393df8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541705"
---
# <a name="efibatterychargingprotocolgetbatterystatus"></a>EFI\_BATTERY\_CHARGING\_PROTOCOL.GetBatteryStatus


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
\[在中\]指向 EFI\_电池\_正在充电\_协议实例。

<a href="" id="stateofcharge"></a>*StateOfCharge*  
\[out\]返回主电池的电量 (SOC) 的当前状态。 SOC 表示为百分比，指示完全充电的 100%。

<a href="" id="ratedcapacity"></a>*RatedCapacity*  
\[out\] mAh 中返回的主电池的额定的功率。

<a href="" id="chargecurrent"></a>*ChargeCurrent*  
\[out\]如果电池正在充电的过程中，将返回正数，表示当前传递到 mA 上的电池。 如果电池正在放电的过程中，返回一个负的数字，指示当前所绘制从 mA 上的电池。 如果既不被收费的也不正在放电电池，它将返回 0。 如果硬件不能提供此信息，它将返回 EFI\_电池\_费用\_当前\_不\_支持 (0x80000000)。

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


此函数返回的额定的功率和费用 (SOC) 主电池的状态。 调用此函数是定期以帮助其他驱动程序实现此协议处理。

## <a name="requirements"></a>要求


**标头：** 用户生成

## <a name="related-topics"></a>相关主题
[EFI\_电池\_正在充电\_协议](efi-battery-charging-protocol.md)  



