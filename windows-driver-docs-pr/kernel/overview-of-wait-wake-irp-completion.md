---
title: 等待/唤醒 IRP 完成概述
description: 等待/唤醒 IRP 完成概述
ms.assetid: a5e09fda-f722-4335-8576-7b058b2f7a21
keywords:
- 电源管理 WDK 内核，唤醒功能
- 外部唤醒信号 WDK
- 唤醒设备
- 唤醒功能 WDK 电源管理
- 设备唤醒 ups WDK 电源管理
- IRP_MN_WAIT_WAKE
- 等待/唤醒 Irp WDK 电源管理完成
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 936b23454102a8fe20fffc79f4a0e279fe65cb50
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352002"
---
# <a name="overview-of-waitwake-irp-completion"></a>等待/唤醒 IRP 完成概述





等待/唤醒 IRP 完成唤醒信号到达时。 唤醒信号是特定于设备的但通常是设备的普通服务事件。 例如，传入通道可能会导致唤醒处于睡眠状态调制解调器。

下图显示在完成等待/唤醒 IRP 的步骤。

![用于完成等待/唤醒 irp 的步骤](images/comp-waitwake.png)

信号时，控制重新进入其中总线检测到该设备已唤醒的点处的总线驱动程序。 总线驱动程序服务所需的事件并调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)完成[ **IRP\_MN\_等待\_唤醒**](https://msdn.microsoft.com/library/windows/hardware/ff551766)其 PDO 的 IRP。

然后，I/O 管理器调用[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程由设备堆栈中的下一个更高版本驱动程序设置。 在中*IoCompletion*例程，该驱动程序服务，根据需要唤醒信号和调用**IoCompleteRequest**完成 IRP。 I/O 管理器将继续调用*IoCompletion*例程处理备份设备堆栈之前的所有驱动程序已完成 IRP。

在其*IoCompletion*例程，任何驱动程序的枚举 （创建多个 PDO） 的多个子设备和已收到等待/唤醒请求来自多个此类设备必须发送本身等待/唤醒 IRP，若要重新配置自身的等待/ 唤醒在另一个子活动。 有关详细信息，请参阅[了解路径的等待/唤醒 Irp 通过设备树](understanding-the-path-of-wait-wake-irps-through-a-device-tree.md)。

在调用*IoCompletion*例程由驱动程序设置，为他们通过在堆栈的下层 IRP，I/O 管理器调用所有者设置的电源策略请求等待/唤醒 IRP 的回调例程。 在回调例程中，策略所有者应将其设备恢复至工作状态，并对其子 PDO 完成挂起等待/唤醒 IRP，如果有。

完成孩子的 IRP 导致 I/O 管理器调用*IoCompletion*例程由子范围的设备堆栈中的驱动程序设置和其他操作。 最终，devnode 启动原始等待/唤醒 IRP 的策略所有者可以确定，其设备被唤醒信号，肯定，所有挂起等待/唤醒 Irp 将会完成。

 

 




