---
title: 系统的电源 IRP
description: 系统的电源 IRP
ms.assetid: a37e8dda-af7a-4f28-bf04-908a74bb5b2f
keywords:
- power Irp WDK 内核系统
- 系统电源 Irp WDK 内核
- IRP_MJ_POWER
- IRP_MN_SET_POWER
- IRP_MN_QUERY_POWER
- 浪涌 power WDK 内核
- 系统浪涌 power WDK 内核
- 更改电源状态 WDK 内核
- 重申的电源状态
- 空闲超时 WDK 电源管理
- 过期的电池 WDK 电源管理
- 电池过期 WDK 电源管理
- 用户请求 power 更改 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a37ec3e3d472b333257e6041a55fc77c9569142
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369180"
---
# <a name="power-irps-for-the-system"></a>系统的电源 IRP





一个*系统电源 IRP*指定主要 IRP 代码[ **IRP\_MJ\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff550784)、 一个下面列出，次要电源 IRP 代码和值**SystemPowerState**中**Power.Type** IRP 堆栈的成员。 电源管理器可以发送此类 IRP;驱动程序不能发送系统电源 IRP。

电源管理器将系统电源 IRP 发送出于以下原因之一：

-   若要更改空闲超时、 系统活动中的更改，用户请求或即将到期的电池响应中的系统电源状态 ([**IRP\_MN\_设置\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744))

-   向查询设备，以确定系统是否可以进入睡眠状态 ([**IRP\_MN\_查询\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551699))

-   若要在查询后重申的当前系统电源状态 (**IRP\_MN\_设置\_POWER**)

电源管理器发送**IRP\_MN\_查询\_POWER**并**IRP\_MN\_设置\_POWER**代表的请求系统。 驱动程序可能会失败**IRP\_MN\_查询\_POWER**请求但不能故障**IRP\_MN\_设置\_POWER**。

例如，若要更改的系统电源状态，电源管理器向系统电源 IRP 中设备树的每个设备节点上的堆栈的顶部驱动程序。 下图显示了单个设备堆栈中的驱动程序如何处理系统电源 IRP。

![说明系统电源 irp 的路径的关系图](images/s2dirp.png)

上一图所示：

1.  电源管理器调用 I/O 管理器以将系统电源 IRP 发送到设备树中每个叶节点。

2.  如果可能，将 IRP 的驱动程序句柄[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程，如有必要，并调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336) （Windows 7 和 WindowsVista) 或[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654) （Windows Server 2003、 Windows XP 和 Windows 2000） 转发 IRP 堆栈。 如果驱动程序必须失败 IRP，驱动程序将立即执行此操作，并完成 IRP。 驱动程序可能会失败**IRP\_MN\_查询\_POWER** Irp，但不得失败**IRP\_MN\_设置\_POWER** Irp，设置系统电源状态。

3.  当拥有电源策略的设备接收 IRP 的驱动程序，该驱动程序集*IoCompletion*例行系统 IRP 和然后转发 IRP。

4.  如果可能，将堆栈句柄 IRP 中的任何其他驱动程序*IoCompletion*例程，如有必要和转发到的下一步较低的驱动程序，如步骤 2 中所示 IRP。

5.  最后，总线驱动程序接收并完成系统 IRP。

6.  I/O 管理器调用任意*IoCompletion*例程作为驱动程序传入系统 IRP 设置向下设备堆栈。

7.  在其*IoCompletion*例程，设备电源策略所有者调用[ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734)发送设备电源 IRP，指定是否为有效的设备电源状态在系统 IRP 的系统电源状态。 驱动程序设置设备电源 IRP 完成时要调用的回调例程。

    如果有必要，驱动程序咨询**DeviceState**在其缓存副本中的成员[**设备\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)结构 (请参阅[报告设备电源功能](reporting-device-power-capabilities.md)) 若要确定哪些设备的电源状态对应到 IRP 中的系统电源状态。

8.  设备 IRP 完毕并运行了任何设备 IRP 完成例程后，会调用电源策略所有者的回调例程。 在回调例程中，该驱动程序将其返回的状态复制到系统 IRP。 在 Windows Server 2003、 Windows XP 和 Windows 2000 中，调用该回调[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776)启动下一个幂 IRP。 但是，在 Windows 7 和 Windows Vista 中，调用**PoStartNextPowerIrp**不是必需的和此类调用会执行任何电源管理操作。 最后，调用该回调[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)完成系统 IRP。

有关详细信息，请参阅[处理系统电源状态请求](handling-system-power-state-requests.md)。

由于某些设备需要当前涌入时它们开启，系统浪涌电源 Irp 的整个系统以同步方式并按顺序处理。 一次，只有一个此类 IRP 可以处于活动状态。 有关详细信息，请参阅[调用 IoCallDriver vs。调用 PoCallDriver](calling-iocalldriver-versus-calling-pocalldriver.md)。

 

 




