---
title: 单个设备的电源 IRP
description: 单个设备的电源 IRP
ms.assetid: a8d5db12-8f6b-4c65-9814-0bc3e476dd1c
keywords:
- power Irp WDK 内核设备
- 设备电源 Irp WDK 内核
- power 序列值 WDK 内核
- 工作状态返回 WDK 电源管理
- 唤醒设备
- 唤醒功能 WDK 电源管理
- 设备唤醒 ups WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 745120e7270a05fca085e969fb0066770c806d9f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369184"
---
# <a name="power-irps-for-individual-devices"></a>单个设备的电源 IRP





一个*设备电源 IRP*指定主要 IRP 代码[ **IRP\_MJ\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff550784)、 一个下面列出，次要电源 IRP 代码和值**DevicePowerState**中**Power.Type**成员。

[**IRP\_MN\_查询\_电源**](https://msdn.microsoft.com/library/windows/hardware/ff551699)

[**IRP\_MN\_SET\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551744)

[**IRP\_MN\_WAIT\_WAKE**](https://msdn.microsoft.com/library/windows/hardware/ff551766)

[**IRP\_MN\_POWER\_SEQUENCE**](https://msdn.microsoft.com/library/windows/hardware/ff551644)

设备堆栈中的所有驱动程序接收此类 Irp;通常情况下，仅设备电源策略管理器可以将这些 Irp 发送。 但是，电源管理器可以发送设备电源 IRP 时执行空闲检测代表一个设备，如中所述[空闲检测使用电源管理器例程](using-power-manager-routines-for-idle-detection.md)。

驱动程序将设备电源 IRP 发送任何原因如下：

-   若要查询或更改设备电源状态以响应系统电源 IRP

-   若要将处于睡眠状态，以便节约用电设备

-   若要将设备恢复为工作状态之后它一直处于睡眠状态

-   若要使设备能够唤醒以响应外部信号

-   若要启动设备时获取 power 序列值

下图显示了一系列步骤，会以发送、 转发、 完成设备电源 IRP。

![说明设备电源 irp 的路径的关系图](images/devpoirp.png)

上图所示，发送 IRP，设备电源转发，并完成以下步骤中：

1.  设备电源策略所有者调用[ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734)分配设备电源 IRP，并指定 PDO IRP 和回调例程 IRP 完成时要调用的目标。

2.  电源管理器分配设备电源 IRP，并将其发送到目标 PDO 设备堆栈中的顶部驱动程序。

3.  该驱动程序将执行以下操作：

    -   集[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程，如果有必要。

    -   调用[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776) （Windows Server 2003、 Windows XP 和 Windows 2000） 如果未使用完成例程。 从 Windows Vista 开始，此调用不需要且此类调用会执行任何电源管理操作。

    -   调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336) （Windows 7 和 Windows Vista） 或调用[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654) （Windows Server 2003、 Windows XP 和 Windows 2000) 要传递到下一步低驱动程序 IRP。

    堆栈中的每个驱动程序执行此操作直到 IRP 达到总线驱动程序。 如果驱动程序时不能 IRP，它应立即执行此操作，并调用[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)。

4.  维护设备 PDO，总线驱动程序执行请求的操作，然后调用**IoCompleteRequest**完成 IRP。 总线驱动程序可能会失败设备强化 IRP 移除某个设备或正被删除。

5.  I/O 管理器调用*IoCompletion*例程作为它们传入 IRP 设置驱动程序的向下堆栈。 毕竟*IoCompletion*已调用例程，请运行回调例程。

有关设备电源 Irp 的详细信息，请参阅[管理的电源可用于单个设备](managing-power-for-individual-devices.md)和[该有唤醒功能的支持设备](supporting-devices-that-have-wake-up-capabilities.md)。 有关 power 序列 IRP 的详细信息，请参阅[ **IRP\_MN\_POWER\_序列**](https://msdn.microsoft.com/library/windows/hardware/ff551644)。

 

 




