---
title: AVStream 中的电源和状态更改
description: AVStream 中的电源和状态更改
keywords:
- AVStream WDK，电源和状态更改
- 电源更改 WDK，AVStream
- 状态更改 WDK，AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae07b0ca61f714973b851609406bc4f9bc435c8f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822691"
---
# <a name="power-and-state-changes-in-avstream"></a>AVStream 中的电源和状态更改


当 AVStream 收到 [**IRP \_ MN 设置 \_ 的 \_ POWER**](../kernel/irp-mn-set-power.md) 请求时，它会调用微型驱动程序的 [*AVStrMiniDeviceSetPower*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnksdevicesetpower) 回调例程（如果微型驱动程序提供一个）。

当 AVStream 收到 [**KSPROPERTY \_ 连接 \_ 状态**](./ksproperty-connection-state.md) 属性的 set 请求时，如果微型驱动程序提供了一个微型驱动程序的 [*AVStrMiniPinSetDeviceState*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdevicestate) 回调例程，则会调用该例程。

当系统从睡眠状态中唤醒时，AVStream 可能会按预期顺序反向调用微型驱动程序的 *AVStrMiniPinSetDeviceState* 和 *AVStrMiniDeviceSetPower* 回调例程。 例如，可以将 *AVStrMiniPinSetDeviceState* 称为 *beforeAVStrMiniDeviceSetPower*。

因此，驱动程序 *必须准备好处理此类预期回拨顺序的反转*。

当系统断电进入睡眠状态时，不会进行此冲销。 关闭电源后，这两个回调例程始终按预期顺序发生。 例如，在 *AVStrMiniDeviceSetPower* 之前始终调用 *AVStrMiniPinSetDeviceState* 。

如果此冲销发生，则整个序列如下所示：

首先，出现断电序列：

1.  调用 *AVStrMiniPinSetDeviceState* 时，请求将设备状态从 **KSSTATE \_ 运行** 更改为 KSSTATE \_ PAUSE。

2.  通过将电源状态从 D0 更改为 D2/D3 来调用 *AVStrMiniDeviceSetPower* 。

3.  此时，系统处于睡眠状态。

4.  接下来，将出现开机序列：

5.  通过将电源状态从 D2/D3 更改为 D0 来调用 *AVStrMiniDeviceSetPower* 。

6.  调用 *AVStrMiniPinSetDeviceState* 时，请求将设备状态从 **KSSTATE \_ 暂停** 更改为 KSSTATE \_ 运行。

在此方案中，步骤5和步骤6是按预期顺序反转的步骤。

此外，当应用程序进行流式处理并且系统启动关机序列时，正在运行的捕获关系图始终处于暂停状态。 如果图形已停止，则它将保持停止状态。

 

