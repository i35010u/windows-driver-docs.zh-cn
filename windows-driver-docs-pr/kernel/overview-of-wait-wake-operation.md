---
title: 等待/唤醒操作概述
description: 等待/唤醒操作概述
ms.assetid: 63453f7e-f656-4efc-bb44-9e2cb0232270
keywords:
- 电源管理 WDK 内核，唤醒功能
- 外部唤醒信号 WDK
- 唤醒设备
- 唤醒功能 WDK 电源管理
- 设备唤醒 ups WDK 电源管理
- IRP_MN_WAIT_WAKE
- 等待/唤醒 Irp WDK 电源管理，有关等待/唤醒 Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4c57b4c8047d9747a476e0fd8d34bdfb2757b42
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360217"
---
# <a name="overview-of-waitwake-operation"></a>等待/唤醒操作概述





操作系统的唤醒机制的工作原理，如下图中所示。

![说明的 irp 概述关系图\-mn\-等待\-唤醒处理](images/send-waitwake.png)

1.  虽然系统和设备是处于工作状态，设备的电源策略所有者确定，其设备，应启用 （"有"） 用于唤醒。 电源策略所有者请求 power IRP ([**PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734)细微的代码与[ **IRP\_MN\_等待\_唤醒**](https://msdn.microsoft.com/library/windows/hardware/ff551766)) 发送到其 PDO 以通知其设备堆栈中的所有驱动程序。 在请求中，策略所有者指定的回调例程 (不完全相同[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程)。

2.  电源管理器，通过 I/O 管理器中，将 IRP 发送到设备堆栈的顶部。

3.  驱动程序集*IoCompletion*例程，并传递 IRP 向下的直到它到达总线驱动程序。

4.  总线驱动程序启用唤醒在物理设备上，如果可以和将挂起的 IRP 标记。 如有必要，它还为其父请求等待/唤醒 IRP。

5.  一段时间后，外部的唤醒信号到达。

6.  总线驱动程序完成**IRP\_MN\_等待\_唤醒**。

7.  I/O 管理器调用*IoCompletion*例程作为驱动程序传入 IRP 设置向下堆栈。

8.  I/O 管理器调用所有者设置的策略请求 IRP 的回调例程。

**IRP\_MN\_等待\_唤醒**请求不会更改的设备或系统电源状态。 它只是使唤醒设备上，从而使更高版本，则设备将进入相应的睡眠状态，如果外部信号将导致设备 （和可能是系统） 被唤醒。

当唤醒信号到达时，驱动程序的行为是相同的是否由系统还是仅将自身中唤醒设备。 如果设备启用了唤醒系统处于休眠状态从该设备可以唤醒它，则设备将被唤醒系统。 如果设备启用了唤醒系统处于工作状态，仅在设备将被唤醒。

因为在不同的计算机和设备设计，特别是涉及 power 平面支持的系统和设备电源状态-，因此可以支持等待/唤醒-的状态都是不在所有硬件配置上相同。 因此，任何拥有其设备的电源策略的驱动程序和每个总线驱动程序必须特别注意正在其运行的各个配置的功能。 有关详细信息，请参阅[确定设备是否可以将系统唤醒](determining-whether-a-device-can-wake-the-system.md)。

等待/唤醒操作的更多详细信息，请参阅[了解路径的等待/唤醒 Irp 通过设备树](understanding-the-path-of-wait-wake-irps-through-a-device-tree.md)并[等待/唤醒 IRP 完成的概述](overview-of-wait-wake-irp-completion.md)。

 

 




