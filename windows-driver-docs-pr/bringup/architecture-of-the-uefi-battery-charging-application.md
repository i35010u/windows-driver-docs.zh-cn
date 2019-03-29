---
title: UEFI 电池充电应用程序的体系结构
description: Microsoft 提供的 UEFI 电池充电应用程序的体系结构
ms.assetid: eabac2ec-6e2f-448f-9793-117e12c288d9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e69976ba90a8fd4d87c0d2a29a2e223a05669aa8
ms.sourcegitcommit: 3cdabbe0af52459e484e093a9e11da8f5312daf6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/26/2019
ms.locfileid: "58441937"
---
# <a name="architecture-of-the-uefi-battery-charging-application-provided-by-microsoft"></a>Microsoft 提供的 UEFI 电池充电应用程序的体系结构

本主题提供有关设计的 UEFI 电池充电由 Microsoft 提供适用于运行 Windows 10 移动版设备的应用程序的信息。 Oem 可以使用电池充电来自 Microsoft，应用程序或它们可以实现自己的收费应用程序。 实现其自己 UEFI 电池充电应用程序的 Oem 可能会使用中的信息本主题指导原则是其设计。

UEFI 电池充电应用程序是一个第一的 Microsoft 自有应用程序在启动过程中运行。 UEFI 电池充电应用程序有以下主要职责：

- 请确保该设备具有足够的电源来启动。

- 提供*关机充电*如果由 OEM 启用支持。 关闭电源收费的详细信息，请参阅[启动环境中的电池充电](battery-charging-in-the-boot-environment.md)。

UEFI 电池充电应用程序使用密钥 UEFI 协议，并对返回的相关驱动程序的各种状态做出反应。

> [!NOTE]
> 术语*UEFI 电池充电应用程序*本主题中引用 UEFI 电池充电 mobilestartup.efi 所加载的库。 有关 mobilestartup.efi 详细信息，请参阅[启动和 UEFI](boot-and-uefi.md)。

## <a name="uefi-protocols-used-by-the-uefi-battery-charging-application"></a>使用 UEFI 电池充电应用程序的 UEFI 协议

UEFI 电池充电应用程序 （由 Microsoft 拥有） 使用以下各节所述的协议 （由 Oem 实现）。

### <a name="uefi-battery-charging-protocol-efibatterychargingprotocol"></a>UEFI 电池充电协议 (EFI\_电池\_正在充电\_协议)

以下步骤介绍如何 UEFI 电池充电应用程序使用 UEFI 电池充电协议的关键方面：

1. UEFI 电池充电应用程序使用轮询电池硬件的实时状态[EFI\_电池\_正在充电\_协议。GetBatteryInformation](efi-battery-charging-protocolgetbatteryinformation.md) (在设备的支持的版本 0x00010002 [EFI\_电池\_正在充电\_协议](efi-battery-charging-protocol.md)) 或[EFI\_电池\_正在充电\_协议。GetBatteryStatus](efi-battery-charging-protocolgetbatterystatus.md) (在设备的支持的 EFI 版本 0x00010001\_电池\_正在充电\_协议)。 这些函数返回的费用 (SOC) 值，只要有可能正确的状态至关重要。 SOC 是基于其状态 （包括容量、 电压和温度） 的值从 0 到 100 电量量从 OEM 定义的映射。

2. Oem 定义*启动到 Main OS 阈值*（从 0 到 100 的值）。 此值可以是不同的设备模型的不同。 有关详细信息*启动到 Main OS 阈值*和其他阈值的值，请参阅[启动环境中的电池充电](battery-charging-in-the-boot-environment.md)。

3. 电池充电应用程序使用该驱动程序从 SOC，并将对其进行比较*启动到 Main OS 阈值*值以确定它是否需要阻止引导过程，以便在 UEFI 中进行收费或继续启动。 它接收有关状态的费用的任何其他信息。

4. UEFI 电池充电的应用程序调用[EFI\_电池\_正在充电\_协议。ChargeBattery](efi-battery-charging-protocolchargebattery.md)收费设备，且该等待**CompletionEvent**对应[EFI\_电池\_正在充电\_状态](efi-battery-charging-status.md)返回。

有关此协议的详细信息，请参阅[UEFI 电池充电协议](uefi-battery-charging-protocol.md)。

### <a name="uefi-display-power-state-protocol-efidisplaypowerprotocol"></a>UEFI 显示电源状态协议 (EFI\_显示\_电源\_协议)

在 UEFI 电池充电过程中，UEFI 电池充电应用程序显示交替的低能耗 UI。 在 10 秒，而无需按下，应用程序调用的电源按钮后[EFI\_显示\_POWER\_协议。SetDisplayPowerState](efi-display-power-protocolsetdisplaypowerstate.md)若要关闭显示器和背景光。 这有助于 UEFI 电池充电时，过程中占用较少的电量的设备，可帮助设备费用，并且更快地进入主操作系统。 如果用户按下电源按钮时显示处于关闭状态，应用程序调用 EFI\_显示\_电源\_协议。SetDisplayPowerState 再次以启用显示。 有关更多详细信息，请参阅[的用户体验](#user-experience)本主题中更高版本。

有关此协议的详细信息，请参阅[UEFI 显示电源状态协议](uefi-display-power-state-protocol.md)。

### <a name="uefi-usb-function-protocol-efiusbfnioprotocol"></a>UEFI USB 函数协议 (EFI\_USBFN\_IO\_协议)

UEFI 电池充电应用程序以独占方式在依赖[EFI\_USBFN\_IO\_协议。DetectPort](efi-usbfn-io-protocoldetectport.md)来确定已连接的端口类型。 根据端口类型，应用程序调用[EFI\_电池\_正在充电\_协议。ChargeBattery](efi-battery-charging-protocolchargebattery.md) 1500 mA 或 500 mA。

有关此协议的详细信息，请参阅[UEFI USB 函数协议](uefi-usb-function-protocol.md)。

## <a name="application-logic"></a>应用程序逻辑

下图描述了 UEFI 电池充电应用程序的逻辑步骤。

![uefi 电池充电逻辑](images/oem-battery-charge-logic.png)

以下说明展开上的逻辑的重要部分：

- 然后再调用[EFI\_电池\_正在充电\_协议。ChargeBattery](efi-battery-charging-protocolchargebattery.md)，应用程序调用[EFI\_USBFN\_IO\_协议。DetectPort](efi-usbfn-io-protocoldetectport.md)来确定最大当前 USB 充电可提供：

  - 如果存在一个端口，应用程序使用 1500 mA 专用的墙充电器或 500 mA 的其他端口。

  - 如果存在任何端口，应用程序使用 500 mA。 无线充电器被应忽略此值。

  - 如果不存在的充电器，应用程序使用 500 mA。 但是，应用程序需要[EFI\_电池\_正在充电\_协议。ChargeBattery](efi-battery-charging-protocolchargebattery.md)以返回[EFI\_电池\_正在充电\_完成\_令牌](efi-battery-charging-completion-token.md)状态为**EfiBatteryChargingSourceNotDetected**。

- 在所有情况下，OEM 必须确保设备与充电器保持安全的操作区域中。

- 如果设备中没有的电池，但没有已连接的电源，当应用程序调用[EFI\_电池\_正在充电\_协议。ChargeBattery](efi-battery-charging-protocolchargebattery.md)给电池充电，UEFI 电池充电驱动程序应返回**EfiBatteryChargingStatusBatteryNotDetected**。 应用程序通过显示一条错误 UI 并关闭该设备来处理此错误。

- [EFI\_电池\_正在充电\_状态](efi-battery-charging-status.md)在这种相同的方式解释值*阈值充电*和*关闭电源收费*模式下除外**EfiBatteryChargingStatusSuccess**。 有关这些计费模式的详细信息，请参阅[启动环境中的电池充电](battery-charging-in-the-boot-environment.md)。

- 计费模式设备时，断开电源应导致信号与应用程序的固件**EfiBatteryChargingSourceNotDetected**，这将导致关闭该应用程序设备。

- 如果固件发出信号状态为应用程序**EfiBatteryChargingStatusOverheat**或**EfiBatteryChargingStatusTimeout**，设备暂停收取 5 分钟 （但应用程序仍然会调用[EFI\_电池\_正在充电\_协议。GetBatteryInformation](efi-battery-charging-protocolgetbatteryinformation.md)或[EFI\_电池\_正在充电\_协议。GetBatteryStatus](efi-battery-charging-protocolgetbatterystatus.md)每隔大约 1 秒)。 设备 5 分钟之后，恢复通过调用充电[EFI\_电池\_正在充电\_协议。ChargeBattery](efi-battery-charging-protocolchargebattery.md)。 在这 5 分钟内，固件仍应发出具有相应应用程序提供的事件信号[EFI\_电池\_正在充电\_状态](efi-battery-charging-status.md)值 （例如，源断开的连接应发出信号**EfiBatteryChargingSourceNotDetected**)。

- 将两种计费模式期间标有的框中显示相关动画的 UI**应用程序中保持**上图中。

- 在中*关机充电*模式下，如果固件已发送信号的事件，并且提供的状态**EfiBatteryChargingStatusSuccess**、 UEFI 电池充电应用程序无法启动到之前将主操作系统用户持有的 3 秒的电源按钮。 但是，如果应用程序检测到已断开 USB 电缆连接这一次，它将关闭电源的设备。 UEFI 电池充电应用程序需要驱动程序保持在完全在电池*充电模式关机*。

- 在*充电模式关机*，只要错误或成功事件，固件具有未收到信号，UEFI 电池充电应用程序不关闭电源的设备。

### <a name="error-handling"></a>错误处理

每次[EFI\_电池\_正在充电\_协议。ChargeBattery](efi-battery-charging-protocolchargebattery.md)调用时， [EFI\_电池\_正在充电\_完成\_令牌](efi-battery-charging-completion-token.md)指定。 在令牌中的事件驱动程序遇到错误，如果通过向发出信号[EFI\_电池\_正在充电\_状态](efi-battery-charging-status.md)。 下表说明了 UEFI 电池充电应用程序如何对不同的情况下的不同状态值做出响应。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>状态</th>
<th>阈值计费模式</th>
<th>打开 / 关闭 （之前和之后的费用状态达到的阈值） 计费模式</th>
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
<td><p><strong>之前的费用状态达到的阈值：</strong>在关闭电源计费模式下继续</p>
<p><strong>之后的费用状态达到的阈值：</strong>保持关闭电源计费模式，直到 USB 已断开连接</p></td>
</tr>
<tr class="odd">
<td><p>EfiBatteryChargingStatusOverheat</p></td>
<td><p>暂停时间为 5 分钟收费，然后在继续收费</p></td>
<td><p>暂停时间为 5 分钟收费，然后在继续收费</p></td>
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
<td><p>暂停时间为 5 分钟收费，然后在继续收费</p></td>
<td><p>暂停时间为 5 分钟收费，然后在继续收费</p></td>
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

下表说明了 UEFI 电池充电应用程序如何应对从收到的状态值[EFI\_电池\_正在充电\_协议。GetBatteryInformation](efi-battery-charging-protocolgetbatteryinformation.md)或[EFI\_电池\_正在充电\_协议。GetBatteryStatus](efi-battery-charging-protocolgetbatterystatus.md)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>状态</th>
<th>阈值计费模式</th>
<th>打开 / 关闭 （之前和之后的费用状态达到的阈值） 计费模式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EFI_SUCCESS</p>
<p>检测不到任何错误时返回此值。</p></td>
<td><p>不适用</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="even">
<td><p>EFI_INVALID_PARAMETER</p>
<p>输入的参数不正确时返回此值。 这应从理论上讲不是可以在生产环境中。</p></td>
<td><p>显示错误 UI 10 秒，然后关闭</p></td>
<td><p>显示错误 UI 10 秒，然后关闭</p></td>
</tr>
<tr class="odd">
<td><p>EFI_DEVICE_ERROR 或 EFI_NOT_READY</p>
<p>采用相同的方式处理这些错误情况。 这些值应由返回<a href="efi-battery-charging-protocolgetbatteryinformation.md" data-raw-source="[EFI_BATTERY_CHARGING_PROTOCOL.GetBatteryInformation](efi-battery-charging-protocolgetbatteryinformation.md)">EFI_BATTERY_CHARGING_PROTOCOL。GetBatteryInformation</a>或<a href="efi-battery-charging-protocolgetbatterystatus.md" data-raw-source="[EFI_BATTERY_CHARGING_PROTOCOL.GetBatteryStatus](efi-battery-charging-protocolgetbatterystatus.md)">EFI_BATTERY_CHARGING_PROTOCOL。GetBatteryStatus</a>情况下，设备可能无法启动到由于某些设备错误将主操作系统中。 具体而言：</p>
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
<p>引发 EFI_DEVICE_ERROR 或 EFI_NOT_READY 跟完成令牌之一的上面列出的错误将导致设备最终关闭。</p></td>
<td><p>恢复并调用<a href="efi-battery-charging-protocolchargebattery.md" data-raw-source="[EFI_BATTERY_CHARGING_PROTOCOL.ChargeBattery](efi-battery-charging-protocolchargebattery.md)">EFI_BATTERY_CHARGING_PROTOCOL。ChargeBattery</a></p></td>
<td><p>恢复并调用<a href="efi-battery-charging-protocolchargebattery.md" data-raw-source="[EFI_BATTERY_CHARGING_PROTOCOL.ChargeBattery](efi-battery-charging-protocolchargebattery.md)">EFI_BATTERY_CHARGING_PROTOCOL。ChargeBattery</a></p></td>
</tr>
</tbody>
</table>

## <a name="user-experience"></a>用户体验

下图显示了如何 UEFI 电池充电应用程序用户界面屏幕绘制如果电池不足够费用或设备是否在*充电模式关机*。

![电池充电的用户体验](images/oem-battery-charge-user-experience.png)

以下步骤介绍如何在应用程序绘制到屏幕用户界面：

- 应用程序通过写入到框架中的每个像素的背景填充颜色清除屏幕。

- 应用程序通过直接到显示位图缓冲区中复制像素绘制交替低水平电量电池 UI 位图。 如果没有被按下电源按钮，应用程序调用的情况下通过 10 秒[EFI\_显示\_POWER\_协议。SetDisplayPowerState](efi-display-power-protocolsetdisplaypowerstate.md)若要关闭显示器和背景光。 如果用户按下电源按钮，EFI\_DISPLAY\_电源\_协议。SetDisplayPowerState 调用以启用显示。

- 当应用程序从驱动程序收到错误时，应用程序通过写入帧缓冲区中的每个像素的背景填充颜色清除屏幕并应用程序然后通过复制相应的位图像素来绘制电池错误屏幕直接到显示的缓冲区。
