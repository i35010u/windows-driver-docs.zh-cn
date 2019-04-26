---
title: EFI_BATTERY_CHARGING_PROTOCOL.GetBatteryInformation
description: EFI_BATTERY_CHARGING_PROTOCOL.GetBatteryInformation
ms.assetid: 497cd001-5180-4dee-a070-ccf8c987bd71
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de0470ff8a3f6dc41c366d6a4d04f30102edb0e9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328045"
---
# <a name="efibatterychargingprotocolgetbatteryinformation"></a>EFI\_BATTERY\_CHARGING\_PROTOCOL.GetBatteryInformation


返回有关主电池包括充电，耗电量被传递到或从电池，电池的终端、 电池温度、 通过 USB 电缆电压电压绘制的当前状态的当前状态的信息并通过 USB 电缆当前。

## <a name="syntax"></a>语法


```cpp
typedef EFI_STATUS (EFIAPI * EFI_BATTERY_CHARGING_GET_BATTERY_INFORMATION) (
    IN EFI_BATTERY_CHARGING_PROTOCOL *This,
    OUT UINT32 *StateOfCharge,
    OUT INT32 *CurrentIntoBattery,
    OUT UINT32 *BatteryTerminalVoltage, 
    OUT INT32 *BatteryTemperature,
    OUT UINT32 *USBCableVoltage,
    OUT UINT32 *USBCableCurrent );
```

## <a name="parameters"></a>Parameters


<a href="" id="this"></a>*此*  
\[在中\]指向 EFI\_电池\_正在充电\_协议实例。

<a href="" id="stateofcharge"></a>*StateOfCharge*  
\[out\]返回主电池的电量 (SOC) 的当前状态。 SOC 以百分比表示，其中 100%表示完全充电表示。

<a href="" id="currentintobattery"></a>*CurrentIntoBattery*  
\[out\]返回下表中所列出的值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>正数</p></td>
<td><p>电池是收费的过程中。 值表示当前传递到 mA 上的电池。</p></td>
</tr>
<tr class="even">
<td><p>负数</p></td>
<td><p>电池正在放电的过程中为。 值指示当前所绘制从 mA 上的电池。</p></td>
</tr>
<tr class="odd">
<td><p>0</p></td>
<td><p>未被电池放电或收费。</p></td>
</tr>
<tr class="even">
<td><p>EFI_BATTERY_CHARGE_CURRENT_NOT_SUPPORTED (0X80000000)</p></td>
<td><p>硬件不能提供此信息。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="batteryterminalvoltage"></a>*BatteryTerminalVoltage*  
\[out\] mV 中的电池终端使跨电压。

<a href="" id="batterytemperature"></a>*BatteryTemperature*  
\[out\] 10ths Kelvin 在某种程度上的电池温度。

<a href="" id="usbcablevoltage"></a>*USBCableVoltage*  
\[out\] mV 中的 USB 电缆通过电压。

<a href="" id="usbcablecurrent"></a>*USBCableCurrent*  
\[out\]在 mA 的 USB 电缆通过当前。

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


UEFI 电池充电应用程序可以检索有关电池的信息定期调用此函数。 应用程序使用此信息来帮助监视电池的状态和诊断错误。

**请注意**  此函数是可以开始于 EFI 的修订 0x00010002\_电池\_正在充电\_协议。 如果 UEFI 电池充电应用程序检测到，只有修订 0x00010001 的协议，则它将调用[EFI\_电池\_正在充电\_协议。GetBatteryStatus](efi-battery-charging-protocolgetbatterystatus.md)相反。

 

## <a name="requirements"></a>要求


**标头：** 用户生成

## <a name="related-topics"></a>相关主题
[EFI\_电池\_正在充电\_协议](efi-battery-charging-protocol.md)  



