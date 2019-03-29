---
title: 取消等待/唤醒 IRP
description: 取消等待/唤醒 IRP
ms.assetid: 08e1d11a-91a3-496a-b3ad-f99456e4ce1d
keywords:
- 电源管理 WDK 内核，唤醒功能
- 外部唤醒信号 WDK
- 唤醒设备
- 唤醒功能 WDK 电源管理
- 设备唤醒 ups WDK 电源管理
- IRP_MN_WAIT_WAKE
- 等待/唤醒 Irp WDK 电源管理，取消
- 正在取消等待/唤醒 Irp
- 取消例程，等待/唤醒 Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 930e7d6a365f2cc49c0588909e04062619cd4b40
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565430"
---
# <a name="canceling-a-waitwake-irp"></a>取消等待/唤醒 IRP





发送等待/唤醒 IRP 的驱动程序可以取消该 IRP。

驱动程序可能需要取消挂起等待/唤醒 IRP 在下列情况下：

-   即插即用驱动程序将收到[ **IRP\_MN\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551755)， [ **IRP\_MN\_查询\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551705)， [ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738)，或[ **IRP\_MN\_惊讶\_删除**](https://msdn.microsoft.com/library/windows/hardware/ff551760)对设备的请求。 该驱动程序应该重新发出等待/唤醒 IRP ([**PoRequestPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559734)) 重新启动设备后。

-   系统会进入睡眠状态，但是不应启用设备唤醒系统。

    例如，USB 集线器驱动程序可能会发送**IRP\_MN\_等待\_唤醒**请求在设备启动时，它更高版本会将其输入设备之一进入睡眠状态的情况下。 当系统处于工作状态时，从设备唤醒信号将设备返回到工作状态 （但具有对系统电源状态没有影响）。 时系统正准备关闭的情况下，USB 集线器驱动程序将取消此 IRP，如果设备不应允许进行唤醒系统。

-   系统即将进入睡眠状态从该设备无法唤醒它。 也就是说，它输入小于比提供支持的状态[ **SystemWake** ](systemwake.md)中指定的值及其[**设备\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)结构。

-   在设备进入中从其它无法响应唤醒信号的电源状态。 也就是说，它即将进入状态不太支持比[ **DeviceWake** ](devicewake.md)中指定的值及其**设备\_功能**结构。

若要取消等待/唤醒 IRP，发送 IRP 调用的驱动程序[ **IoCancelIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548338)，该驱动程序调用时将指针传递给 IRP，之前返回**PoRequestPowerIrp**.

驱动程序必须取消等待/唤醒未发送的 IRP。

### <a href="" id="ddk-cancel-routines-for-wait-wake-irps-kg"></a>等待/唤醒 Irp 的取消例程

许多函数和总线驱动程序应设置[*取消*](https://msdn.microsoft.com/library/windows/hardware/ff540742)例程的挂起的等待/唤醒 Irp; 以下类型的驱动程序必须设置此类例程：

-   更改设备设置来启用或禁用唤醒的驱动程序。

-   驱动程序发送[ **IRP\_MN\_等待\_唤醒**](https://msdn.microsoft.com/library/windows/hardware/ff551766)父设备的驱动程序的请求。

一个[*取消*](https://msdn.microsoft.com/library/windows/hardware/ff540742)例程使驱动程序禁用唤醒为其设备并清理与挂起等待/唤醒 IRP 相关的任何数据。 请求的驱动程序等待/唤醒 Irp 为父设备可以取消这些 Irp 也。

在其等待/唤醒*取消*例程，驱动程序应执行以下步骤：

1.  调用[ **IoSetCancelRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549674)若要重置*取消*到 IRP 为日常**NULL**。

2.  调用[ **IoReleaseCancelSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff549550)，并传递**CancelIRQL** IRP 取消自旋锁释放的 IRP 中指定。

3.  重置设备扩展中的任何相关字段。 例如，等待/唤醒 IRP 挂起时，大多数驱动程序将设置一个标志，并将指针保留在设备扩展 IRP。

    请注意，驱动程序以接收等待/唤醒 IRP，但它正在取消另一个此类 IRP 的可能。 该驱动程序必须检查以查看是否已具有 IRP 下数值调节钮锁保护 （或其等效项）。 如果是这样，该驱动程序必须仔细同步其处理，以确保它取消正确 IRP。 有关如何使用数值调节钮的详细信息中的锁*取消*例程，请参阅[取消 Irp](canceling-irps.md)。

4.  更改任何所需的设备设置。 例如，调制解调器驱动程序会禁用该设备的唤醒设置。

5.  设置**Irp-&gt;IoStatus.Status**于状态\_已取消。

6.  调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)完成等待/唤醒 IRP，并指定 IO\_否\_增量。

7.  如果该驱动程序以前请求过相关**IRP\_MN\_等待\_唤醒**父设备的驱动程序应取消该 IRP 中的其*取消*例程。 该驱动程序必须释放取消自旋锁之前取消父级的 IRP。

    例如，可用作设备的总线驱动程序，并为其父级拥有电源策略驱动程序的驱动程序应取消相关的等待/唤醒之前发送给其父级的 IRP。 调用[ **IoCancelIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548338)像调用父*取消*例程，关闭设备堆栈，依此类推。

 

 




