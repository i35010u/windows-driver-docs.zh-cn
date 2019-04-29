---
title: 使 ISR 处于活动或非活动状态
description: 从 Windows 8 开始，驱动程序可以调用 IoReportInterruptActive 或 IoReportInterruptInactive 例程，以使已注册的中断服务例程 (ISR) 活动或非活动。
ms.assetid: 788D9341-D1F8-4126-8C30-AA49DE27F4BB
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6dfb0b4a3e803d2368dbc0657cebf0df5d00f12d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378741"
---
# <a name="making-an-isr-active-or-inactive"></a>使 ISR 处于活动或非活动状态


从 Windows 8 开始，驱动程序可以调用[ **IoReportInterruptActive** ](https://msdn.microsoft.com/library/windows/hardware/jj158875)或[ **IoReportInterruptInactive** ](https://msdn.microsoft.com/library/windows/hardware/jj158876)例程，以使已注册的中断服务例程 (ISR) 活动或非活动。

若要注册 ISR 并连接中断或一系列中断 ISR，驱动程序调用[ **IoConnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548378)例程。 ISR 注册后，可以使用该驱动程序**IoReportInterruptActive**并**IoReportInterruptInactive**执行轻型 （或"软"） 以及断开其连接保留 ISR 的操作注册保持不变。 **IoReportInterruptInactive**禁用对 ISR 调用通过软断开关联的中断。 **IoReportInterruptActive**软连接以启用对 ISR 调用这些中断

例如，驱动程序可能会调用**IoReportInterruptInactive**软-断开的连接中断一组设备退出 D0 电源状态，并调用之前**IoReportInterruptActive**软连接这些设备重新输入 D0 后中断。 从原理上讲，驱动程序可能会改为调用[ **IoDisconnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549093)设备退出 D0，并调用之前**IoConnectInterruptEx**设备重新输入 D0 后。 但是， **IoReportInterrupt * Xxx*** 调用速度要快于**IoConnectInterruptEx**并**IoDisconnectInterruptEx**调用。 与此相反**IoConnectInterruptEx**并**IoDisconnectInterruptEx**调用，这可能会失败的原因 （例如，没有足够的系统资源） 有多种， **IoReportInterrupt * Xxx*** 调用很少 （如果有） 时，才会失败。 此外， **IoReportInterrupt * Xxx*** 例程可以调用在 IRQL &lt;= 调度\_级别，而**IoConnectInterruptEx**和**IoDisconnectInterruptEx**可以调用仅在被动\_级别。

默认情况下，ISR 处于活动状态 （和启用对 ISR 调用） 后**IoConnectInterruptEx**成功注册 ISR

调用**IoReportInterruptInactive**并**IoReportInterruptActive**都是可选的。 之前驱动程序调用一个驱动程序永远不会调用这些例程，如果已注册的 ISR 保持活动状态[ **IoDisconnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549093)例程，以取消注册 ISR

该驱动程序应配置要发出中断，仅当这些中断 ISR 处于活动状态的设备。 未能阻止设备 ISR 处于非活动状态时发出中断可能会导致系统不稳定。 例如，如果设备与其他设备共享级别触发中断的行，并且设备问题中断请求 ISR 处于非活动状态时，在行上的其他设备 Isr 也不会承认中断和中断将继续激发. 然后再调用**IoReportInterruptInactive**，驱动程序应配置设备停止发出中断。 在调用**IoReportInterruptActive**，驱动程序应配置设备开始发出中断。

若要取消注册 ISR，驱动程序可以调用**IoDisconnectInterruptEx**不管 ISR 是当前活动或非活动。

**IoReportInterruptActive** ISR 已处于活动状态时，会发生的调用不起作用，但不是会视为错误。 同样， **IoReportInterruptInactive** ISR 已处于非活动状态时，会发生的调用不起作用，但不是会视为错误。

 

 




