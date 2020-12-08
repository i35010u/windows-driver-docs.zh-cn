---
title: UEFI 电池充电应用程序的体系结构
description: Microsoft 提供的 UEFI 电池充电应用程序的体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a8e2f59100eb7d3eafbf80bebf68285423973c9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798479"
---
# <a name="architecture-of-the-uefi-battery-charging-application-provided-by-microsoft"></a>Microsoft 提供的 UEFI 电池充电应用程序的体系结构

本主题提供有关 Microsoft 为运行 Windows 10 移动版的设备提供的 UEFI 电池充电应用程序设计的信息。 Oem 可以使用 Microsoft 的电池充电应用程序，也可以实现其自己的收费应用程序。 如果 Oem 实现自己的 UEFI 电池充电应用程序，则可以使用本主题中的信息作为其设计的指导原则。

UEFI 电池充电应用程序是在启动过程中最先运行的 Microsoft 拥有的应用程序之一。 UEFI 电池充电应用程序具有以下主要职责：

- 请确保设备有足够的电量启动。

- 如果 OEM 启用，请提供 *断电* 支持。 有关断电的详细信息，请参阅 [在启动环境中进行电池充电](battery-charging-in-the-boot-environment.md)。

UEFI 电池充电应用程序使用密钥 UEFI 协议，并响应相关驱动程序返回的各种状态。

> [!NOTE]
> 本主题中的 " *uefi 电池充电应用程序* " 一词是指由 mobilestartup 加载的 uefi 电池充电库。 有关 mobilestartup 的详细信息，请参阅 [Boot AND UEFI](boot-and-uefi.md)。

## <a name="uefi-protocols-used-by-the-uefi-battery-charging-application"></a>UEFI 电池充电应用程序使用的 UEFI 协议

Microsoft) 拥有的 UEFI 电池充电应用程序 (使用由 Oem 实现的协议 () 以下部分中所述。

### <a name="uefi-battery-charging-protocol-efi_battery_charging_protocol"></a> (EFI 电池充电协议的 UEFI 充电协议 \_ \_ \_) 

以下步骤介绍了 UEFI 电池充电应用程序如何使用 UEFI 电池充电协议的主要方面：

1. 通过使用 [EFI \_ 电池 \_ 充电协议，UEFI 电池充电应用程序会轮询电池硬件的实时状态 \_ 。GetBatteryInformation](efi-battery-charging-protocolgetbatteryinformation.md) (在支持) [efi \_ 电池 \_ 充电 \_ 协议](efi-battery-charging-protocol.md) 的版本0x00010002 或 [efi \_ 电池 \_ 充电协议的设备中 \_ 。GetBatteryStatus](efi-battery-charging-protocolgetbatterystatus.md) (在支持 \_) EFI 电池 \_ 充电协议版本0x00010001 的设备中 \_ 。 如果可能，这些函数应尽可能 (SOC) 值返回准确的状态。 SOC 是从电池中的电量量开始的 OEM 定义的映射，其状态为从0到100的值 (包括容量、电压和温度) 。

2. Oem 定义从0到 100) 中的 " *启动到主操作系统" 阈值* (值。 对于不同的设备型号，此值可能会不同。 有关 *启动到主操作系统阈值* 和其他阈值的详细信息，请参阅 [启动环境中的电池充电](battery-charging-in-the-boot-environment.md)。

3. 电池充电应用程序使用驱动程序中的 SOC，并将其与 " *启动到主操作系统阈值* " 的值进行比较，以确定是否需要阻止启动过程以在 UEFI 中计费或继续启动。 它不会收到有关费用状态的任何其他信息。

4. UEFI 电池充电应用程序调用 [EFI \_ 电池 \_ 充电 \_ 协议。ChargeBattery](efi-battery-charging-protocolchargebattery.md)对设备计费，并等待返回具有相应 [EFI \_ 电池 \_ 充电 \_ 状态](efi-battery-charging-status.md)的 **CompletionEvent** 。

有关此协议的详细信息，请参阅 [UEFI 电池充电协议](uefi-battery-charging-protocol.md)。

### <a name="uefi-display-power-state-protocol-efi_display_power_protocol"></a>UEFI 显示电源状态协议 (EFI \_ 显示 \_ 电源 \_ 协议) 

在 UEFI 电池充电过程中，UEFI 电池充电应用程序将显示一个备用的低功耗 UI。 10秒后，如果未按下电源按钮，应用程序将调用 [EFI \_ 显示 \_ 电源 \_ 协议。SetDisplayPowerState](efi-display-power-protocolsetdisplaypowerstate.md) 关闭显示屏和背景光。 这可以帮助设备在 UEFI 电池充电期间消耗更少的电量，这有助于设备充电并更快地进入主操作系统。 如果用户在显示处于关闭状态的情况下按下 "电源" 按钮，应用程序将调用 EFI \_ 显示 \_ 电源 \_ 协议。SetDisplayPowerState 再次打开显示。 有关更多详细信息，请参阅本主题后面的 [用户体验](#user-experience) 。

有关此协议的详细信息，请参阅 [UEFI 显示电源状态协议](uefi-display-power-state-protocol.md)。

### <a name="uefi-usb-function-protocol-efi_usbfn_io_protocol"></a>UEFI USB function 协议 (EFI \_ USBFN \_ IO \_ 协议) 

UEFI 电池充电应用程序仅依赖于 [EFI \_ USBFN \_ IO \_ 协议。DetectPort](efi-usbfn-io-protocoldetectport.md) 确定连接的端口类型。 根据端口类型，应用程序将调用 [EFI \_ 电池 \_ 充电 \_ 协议。ChargeBattery](efi-battery-charging-protocolchargebattery.md) 为 1500 ma 或 500 ma。

有关此协议的详细信息，请参阅 [UEFI USB 函数协议](uefi-usb-function-protocol.md)。

## <a name="application-logic"></a>应用程序逻辑

下图描述了 UEFI 电池充电应用程序的逻辑过程。

![uefi 电池充电逻辑](images/oem-battery-charge-logic.png)

以下内容概述了逻辑的一些关键部分：

- 在调用 [EFI \_ 电池 \_ 充电 \_ 协议之前。ChargeBattery](efi-battery-charging-protocolchargebattery.md)，应用程序调用 [EFI \_ USBFN \_ IO \_ 协议。DetectPort](efi-usbfn-io-protocoldetectport.md) 确定 USB 充电器可提供的最大电流：

  - 如果存在端口，则该应用程序将为其他端口使用 1500 mA 作为专用壁式充电器或 500 mA。

  - 如果没有端口，应用程序将使用 500 mA。 无线充电器应忽略此值。

  - 如果没有任何充电器，应用程序将使用 500 mA。 但是，应用程序需要 [EFI \_ 电池 \_ 充电 \_ 协议。ChargeBattery](efi-battery-charging-protocolchargebattery.md)返回状态为 **EfiBatteryChargingSourceNotDetected** 的 [EFI \_ 电池 \_ 充电 \_ 完成 \_ 令牌](efi-battery-charging-completion-token.md)。

- 在所有情况下，OEM 必须确保设备和充电器处于安全的操作区域内。

- 如果设备中没有电池，但在应用程序调用 [EFI \_ 电池 \_ 充电协议时有连接的电源 \_ 。ChargeBattery](efi-battery-charging-protocolchargebattery.md) 为电池充电，UEFI 电池充电驱动程序应返回 **EfiBatteryChargingStatusBatteryNotDetected**。 应用程序通过显示错误 UI 并关闭设备来处理此错误。

- [EFI \_ 电池 \_ 充电 \_ 状态](efi-battery-charging-status.md)值的解释方式与 *阈值充电* 和 *电源切断充电* 模式相同，但 **EfiBatteryChargingStatusSuccess** 除外。 有关这些收费模式的详细信息，请参阅 [启动环境中的电池充电](battery-charging-in-the-boot-environment.md)。

- 当设备处于充电模式时，断开电源将导致固件使用 **EfiBatteryChargingSourceNotDetected** 向应用程序发出信号，这将导致应用程序关闭设备。

- 如果固件用 **EfiBatteryChargingStatusOverheat** 或 **EfiBatteryChargingStatusTimeout** 的状态对应用程序发出信号，则设备将在5分钟内暂停充电 (但应用程序仍调用 [EFI \_ 电池 \_ 充电 \_ 协议。GetBatteryInformation](efi-battery-charging-protocolgetbatteryinformation.md) 或 [EFI \_ 电池 \_ 充电 \_ 协议。GetBatteryStatus](efi-battery-charging-protocolgetbatterystatus.md) 大约为1秒的间隔) 。 5分钟后，设备会通过调用 [EFI \_ 电池 \_ 充电协议恢复充电 \_ 。ChargeBattery](efi-battery-charging-protocolchargebattery.md)。 在5分钟内，固件仍应使用适当的 [EFI \_ 电池 \_ 充电 \_ 状态](efi-battery-charging-status.md) 值向应用程序提供的事件发出信号 (例如，源断开连接应发出 **EfiBatteryChargingSourceNotDetected**) 信号。

- 在这两种充电模式下，在上图中标记为 " **应用** " 的框中，将显示相关的动画 UI。

- 在 *关闭充电* 模式下，如果固件发出了一个事件，并提供了 **EfiBatteryChargingStatusSuccess** 状态，则在用户按住电源按钮3秒钟之前，UEFI 电池充电应用程序不会启动到主操作系统。 但是，如果应用程序检测到 USB 电缆此时已断开连接，则它会关闭设备电源。 UEFI 电池充电应用程序期望驱动程序在 *电源关闭充电模式下* 维持电池电量完全相同。

- 在关闭 *充电模式下*，只要固件未发出错误或成功事件，UEFI 电池充电应用程序就不会关闭设备电源。

### <a name="error-handling"></a>错误处理

每次进行 [EFI \_ 电池 \_ 充电 \_ 协议。调用 ChargeBattery](efi-battery-charging-protocolchargebattery.md) 时，指定了 [EFI \_ 电池 \_ 充电 \_ 完成 \_ 令牌](efi-battery-charging-completion-token.md) 。 如果驱动程序遇到错误，则令牌中的事件以 [EFI \_ 电池 \_ 充电 \_ 状态](efi-battery-charging-status.md)进行信号。 下表说明了在不同情况下，UEFI 电池充电应用程序如何对不同状态值做出反应。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>状态</th>
<th>阈值充电模式</th>
<th>在收费状态达到阈值之前和之后 (的电充电模式) </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EfiBatteryChargingStatusNoneNone</p></td>
<td><p>不应/无效</p></td>
<td><p>不应/无效</p></td>
</tr>
<tr class="even">
<td><p>EfiBatteryChargingStatusSuccess</p></td>
<td><p>启动到 OS</p></td>
<td><p><strong>在收费状态达到阈值之前：</strong> 在电源关闭充电模式下继续</p>
<p><strong>当收费状态达到阈值后：</strong> 在 USB 断开连接之前，请保持断电充电模式</p></td>
</tr>
<tr class="odd">
<td><p>EfiBatteryChargingStatusOverheat</p></td>
<td><p>在5分钟内暂停充电，然后恢复充电</p></td>
<td><p>在5分钟内暂停充电，然后恢复充电</p></td>
</tr>
<tr class="even">
<td><p>EfiBatteryChargingStatusVoltageOutOfRange</p></td>
<td><p>启动到 OS</p></td>
<td><p>启动到 OS</p></td>
</tr>
<tr class="odd">
<td><p>EfiBatteryChargingStatusCurrentOutOfRange</p></td>
<td><p>启动到 OS</p></td>
<td><p>启动到 OS</p></td>
</tr>
<tr class="even">
<td><p>EfiBatteryChargingStatusTimeout</p></td>
<td><p>在5分钟内暂停充电，然后恢复充电</p></td>
<td><p>在5分钟内暂停充电，然后恢复充电</p></td>
</tr>
<tr class="odd">
<td><p>EfiBatteryChargingStatusAborted</p></td>
<td><p>显示错误 UI 10 秒，然后关闭</p></td>
<td><p>显示错误 UI 10 秒，然后关闭</p></td>
</tr>
<tr class="even">
<td><p>EfiBatteryChargingStatusDeviceError</p></td>
<td><p>显示错误 UI 10 秒，然后关闭</p></td>
<td><p>显示错误 UI 10 秒，然后关闭</p></td>
</tr>
<tr class="odd">
<td><p>EfiBatteryChargingStatusExtremeCold</p></td>
<td><p>显示错误 UI 10 秒，然后关闭</p></td>
<td><p>显示错误 UI 10 秒，然后关闭</p></td>
</tr>
<tr class="even">
<td><p>EfiBatteryChargingStatusBatteryChargingNotSupported</p></td>
<td><p>显示错误 UI 10 秒，然后关闭</p></td>
<td><p>显示错误 UI 10 秒，然后关闭</p></td>
</tr>
<tr class="odd">
<td><p>EfiBatteryChargingStatusBatteryNotDetected</p></td>
<td><p>显示错误 UI 10 秒，然后关闭</p></td>
<td><p>显示错误 UI 10 秒，然后关闭</p></td>
</tr>
<tr class="even">
<td><p>EfiBatteryChargingSourceNotDetected</p></td>
<td><p>关机</p></td>
<td><p>关机</p></td>
</tr>
<tr class="odd">
<td><p>EfiBatteryChargingSourceVoltageInvalid</p></td>
<td><p>显示错误 UI 10 秒，然后关闭</p></td>
<td><p>显示错误 UI 10 秒，然后关闭</p></td>
</tr>
<tr class="even">
<td><p>EfiBatteryChargingSourceCurrentInvalid</p></td>
<td><p>显示错误 UI 10 秒，然后关闭</p></td>
<td><p>显示错误 UI 10 秒，然后关闭</p></td>
</tr>
<tr class="odd">
<td><p>EfiBatteryChargingErrorRequestShutdown</p></td>
<td><p>关机</p></td>
<td><p>关机</p></td>
</tr>
<tr class="even">
<td><p>EfiBatteryChargingErrorRequestReboot</p></td>
<td><p>重新启动</p></td>
<td><p>重新启动</p></td>
</tr>
</tbody>
</table>

下表说明了 UEFI 电池充电应用程序如何响应从 [EFI \_ 电池 \_ 充电协议接收到的状态值 \_ 。GetBatteryInformation](efi-battery-charging-protocolgetbatteryinformation.md) 或 [EFI \_ 电池 \_ 充电 \_ 协议。GetBatteryStatus](efi-battery-charging-protocolgetbatterystatus.md)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>状态</th>
<th>阈值充电模式</th>
<th>在收费状态达到阈值之前和之后 (的电充电模式) </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EFI_SUCCESS</p>
<p>如果未检测到错误，则返回该值。</p></td>
<td><p>不适用</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="even">
<td><p>EFI_INVALID_PARAMETER</p>
<p>当输入参数不正确时，将返回此值。 理论上，这在生产环境中不可能出现。</p></td>
<td><p>显示错误 UI 10 秒，然后关闭</p></td>
<td><p>显示错误 UI 10 秒，然后关闭</p></td>
</tr>
<tr class="odd">
<td><p>EFI_DEVICE_ERROR 或 EFI_NOT_READY</p>
<p>这些错误条件的处理方式相同。 应 EFI_BATTERY_CHARGING_PROTOCOL 返回这些值 <a href="efi-battery-charging-protocolgetbatteryinformation.md" data-raw-source="[EFI_BATTERY_CHARGING_PROTOCOL.GetBatteryInformation](efi-battery-charging-protocolgetbatteryinformation.md)">。GetBatteryInformation</a> 或 <a href="efi-battery-charging-protocolgetbatterystatus.md" data-raw-source="[EFI_BATTERY_CHARGING_PROTOCOL.GetBatteryStatus](efi-battery-charging-protocolgetbatterystatus.md)">EFI_BATTERY_CHARGING_PROTOCOL。GetBatteryStatus</a> ，因为某些设备出错，设备可能无法启动到主操作系统。 具体而言：</p>
<ul>
<li><p>EfiBatteryChargingStatusAborted</p></li>
<li><p>EfiBatteryChargingStatusDeviceError</p></li>
<li><p>EfiBatteryChargingStatusExtremeCold</p></li>
<li><p>EfiBatteryChargingStatusBatteryChargingNotSupported</p></li>
<li><p>EfiBatteryChargingStatusBatteryNotDetected</p></li>
<li><p>EfiBatteryChargingSourceVoltageInvalid</p></li>
<li><p>EfiBatteryChargingSourceCurrentInvalid</p></li>
<li><p>EfiBatteryChargingErrorRequestShutdown</p></li>
<li><p>EfiBatteryChargingErrorRequestReboot</p></li>
</ul>
<p>引发上述错误之一的 EFI_DEVICE_ERROR 或 EFI_NOT_READY 后，将导致设备最终关闭。</p></td>
<td><p>恢复并调用 <a href="efi-battery-charging-protocolchargebattery.md" data-raw-source="[EFI_BATTERY_CHARGING_PROTOCOL.ChargeBattery](efi-battery-charging-protocolchargebattery.md)">EFI_BATTERY_CHARGING_PROTOCOL。ChargeBattery</a></p></td>
<td><p>恢复并调用 <a href="efi-battery-charging-protocolchargebattery.md" data-raw-source="[EFI_BATTERY_CHARGING_PROTOCOL.ChargeBattery](efi-battery-charging-protocolchargebattery.md)">EFI_BATTERY_CHARGING_PROTOCOL。ChargeBattery</a></p></td>
</tr>
</tbody>
</table>

## <a name="user-experience"></a>用户体验

下图显示了在电池电量不足的情况下，以及设备是否处于 *关机模式* 时，UEFI 电池充电应用程序如何将 UI 绘制到屏幕。

![电池充电用户体验](images/oem-battery-charge-user-experience.png)

以下步骤说明了应用程序如何将 UI 绘制到屏幕：

- 应用程序通过将背景填充颜色写入帧中的每个像素来清除屏幕。

- 应用程序通过将位图缓冲区中的像素直接复制到显示器，来绘制备用电池电量小用户位图。 如果10秒通过，但没有按下电源按钮，应用程序将调用 [EFI \_ 显示 \_ 电源 \_ 协议。SetDisplayPowerState](efi-display-power-protocolsetdisplaypowerstate.md) 关闭显示屏和背景光。 如果用户按下 "电源" 按钮，则 EFI \_ 显示 \_ 电源 \_ 协议。调用 SetDisplayPowerState 以重新打开显示。

- 当应用程序收到来自驱动程序的错误时，应用程序会通过将背景填充颜色写入帧缓冲区中的每个像素来清除屏幕，然后应用程序通过将像素从适当的位图缓冲区直接复制到显示器来绘制电池错误屏幕。
