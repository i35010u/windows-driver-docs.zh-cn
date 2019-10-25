---
title: AVStream 中的电源和状态更改
description: AVStream 中的电源和状态更改
ms.assetid: f62f4306-97c0-40fe-89ec-d08eb18988c9
keywords:
- AVStream WDK，电源和状态更改
- 电源更改 WDK，AVStream
- 状态更改 WDK，AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18dcf6a7fdc63dd4bf308137c8da7bd17f77ebb8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842625"
---
# <a name="power-and-state-changes-in-avstream"></a>AVStream 中的电源和状态更改


当 AVStream 收到[**IRP\_MN\_设置\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power) request 时，如果微型驱动程序提供了一个微型驱动程序的[*AVStrMiniDeviceSetPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksdevicesetpower)回调例程，则会调用该例程。

当 AVStream 收到[**KSPROPERTY\_连接\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-state)属性的 set 请求时，如果微型驱动程序提供了一个微型驱动程序的[*AVStrMiniPinSetDeviceState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdevicestate)回调例程。

当系统从睡眠状态中唤醒时，AVStream 可能会按预期顺序反向调用微型驱动程序的*AVStrMiniPinSetDeviceState*和*AVStrMiniDeviceSetPower*回调例程。 例如，可以将*AVStrMiniPinSetDeviceState*称为*beforeAVStrMiniDeviceSetPower*。

因此，驱动程序*必须准备好处理此类预期回拨顺序的反转*。

当系统断电进入睡眠状态时，不会进行此冲销。 关闭电源后，这两个回调例程始终按预期顺序发生。 例如，在*AVStrMiniDeviceSetPower*之前始终调用*AVStrMiniPinSetDeviceState* 。

如果此冲销发生，则整个序列如下所示：

首先，出现断电序列：

1.  使用从**KSSTATE\_运行**到 KSSTATE\_暂停的请求来调用*AVStrMiniPinSetDeviceState* 。

2.  通过将电源状态从 D0 更改为 D2/D3 来调用*AVStrMiniDeviceSetPower* 。

3.  此时，系统处于睡眠状态。

4.  接下来，将出现开机序列：

5.  通过将电源状态从 D2/D3 更改为 D0 来调用*AVStrMiniDeviceSetPower* 。

6.  调用*AVStrMiniPinSetDeviceState*时，请求将设备状态从**KSSTATE\_PAUSE**更改为 KSSTATE\_运行。

在此方案中，步骤5和步骤6是按预期顺序反转的步骤。

此外，当应用程序进行流式处理并且系统启动关机序列时，正在运行的捕获关系图始终处于暂停状态。 如果图形已停止，则它将保持停止状态。

 

 




