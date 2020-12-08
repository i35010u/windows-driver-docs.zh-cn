---
title: EFI_BATTERY_CHARGING_PROTOCOL.GetBatteryInformation
description: EFI_BATTERY_CHARGING_PROTOCOL.GetBatteryInformation
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cae893d791dbd6c3240bb2e792ab9358a7229531
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803411"
---
# <a name="efi_battery_charging_protocolgetbatteryinformation"></a>EFI \_ 电池 \_ 充电 \_ 协议。GetBatteryInformation


返回有关主电池的当前状态的信息，包括电量状态、当前正在传送到电池的电流量、电池的终端温度、电池温度、USB 电缆上的电压以及通过 USB 电缆的电流。

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

## <a name="parameters"></a>参数


<a href="" id="this"></a>*此*  
\[位于 \] EFI \_ 电池 \_ 充电协议实例的指针中 \_ 。

<a href="" id="stateofcharge"></a>*StateOfCharge*  
\[out \] 返回主电池 (SOC) 的当前充电状态。 SOC 以百分比表示，其中100% 表示完全充电。

<a href="" id="currentintobattery"></a>*CurrentIntoBattery*  
\[out \] 返回下表中列出的值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>“值”</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>正数</p></td>
<td><p>电池正在充电。 值指示当前通过 mA 传递到电池的电流。</p></td>
</tr>
<tr class="even">
<td><p>负数</p></td>
<td><p>电池正在放电。 值指示当前正在使用 mA 中的电池进行绘制。</p></td>
</tr>
<tr class="odd">
<td><p>0</p></td>
<td><p>电池未充电或电量不足。</p></td>
</tr>
<tr class="even">
<td><p>EFI_BATTERY_CHARGE_CURRENT_NOT_SUPPORTED (0x80000000) </p></td>
<td><p>硬件无法提供此信息。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="batteryterminalvoltage"></a>*BatteryTerminalVoltage*  
\[每 \] 个电池电量在 mV 中的电压。

<a href="" id="batterytemperature"></a>*BatteryTemperature*  
\[\]10ths 的电池电量不足。

<a href="" id="usbcablevoltage"></a>*USBCableVoltage*  
\[\]在 mV 中通过 USB 电缆的电压。

<a href="" id="usbcablecurrent"></a>*USBCableCurrent*  
\[\]通过 mA 中的 USB 电缆来确定当前的。

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


此函数由 UEFI 电池充电应用程序定期调用，以检索有关电池的信息。 应用程序使用此信息来帮助监视电池的状态，并诊断错误。

**注意**  
此函数可从 EFI \_ 电池充电协议的修订版0x00010002 开始 \_ \_ 。 如果 UEFI 电池充电应用程序检测到仅提供协议的修订版0x00010001，它将调用 [EFI \_ 电池 \_ 充电 \_ 协议。GetBatteryStatus](efi-battery-charging-protocolgetbatterystatus.md) 。

 

## <a name="requirements"></a>要求


**标头：** 用户生成

## <a name="related-topics"></a>相关主题
[EFI \_ 电池 \_ 充电 \_ 协议](efi-battery-charging-protocol.md)  



