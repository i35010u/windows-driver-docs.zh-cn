---
title: AVStream 中的电源和状态更改
description: AVStream 中的电源和状态更改
ms.assetid: f62f4306-97c0-40fe-89ec-d08eb18988c9
keywords:
- AVStream WDK、 power 和状态更改
- 电源更改 WDK AVStream
- 状态更改 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e253c29111f582a92db828895e048c881b6dfbd7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369555"
---
# <a name="power-and-state-changes-in-avstream"></a>AVStream 中的电源和状态更改


当收到 AVStream [ **IRP\_MN\_设置\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)请求，它将调用微型驱动程序的[ *AVStrMiniDeviceSetPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksdevicesetpower)回调例程，如果微型驱动程序提供了一个。

当 AVStream 收到的集请求[ **KSPROPERTY\_连接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-state)属性，它会调用微型驱动程序的[ *AVStrMiniPinSetDeviceState* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspinsetdevicestate)回调例程，如果微型驱动程序提供了一个。

当系统从睡眠状态中唤醒时，AVStream 可能调用微型驱动程序的*AVStrMiniPinSetDeviceState*并*AVStrMiniDeviceSetPower*中预期的顺序相反的回调例程。 例如， *AVStrMiniPinSetDeviceState*不能调用*beforeAVStrMiniDeviceSetPower*。

因此，该驱动程序*必须准备好处理此类正好相反的预期的回调顺序*。

当系统关闭电源进入睡眠状态时不会发生此正好相反。 关闭电源，两个回调例程始终按预期顺序发生。 例如， *AVStrMiniPinSetDeviceState*之前，始终调用*AVStrMiniDeviceSetPower*。

如果此反转的发生，整个序列如下所示：

首先，会发生关机序列：

1.  *AVStrMiniPinSetDeviceState*请求以更改设备状态从使用调用**KSSTATE\_运行**到 KSSTATE\_暂停。

2.  *AVStrMiniDeviceSetPower*调用包含从 D0 的电源状态更改为 D2/D3 的请求。

3.  此时，系统处于休眠状态。

4.  接下来，在开机发生：

5.  *AVStrMiniDeviceSetPower*调用包含从 D2/D3 的电源状态更改为 D0 的请求。

6.  *AVStrMiniPinSetDeviceState*请求以更改设备状态从使用调用**KSSTATE\_暂停**到 KSSTATE\_运行。

在此方案中，步骤 5 和 6 是从预期的顺序反转的步骤。

此外，当流式处理应用程序并在系统启动序列关机时，正在运行的捕获关系图始终放在暂停状态。 如果已停止在关系图，它将保持已停止。

 

 




