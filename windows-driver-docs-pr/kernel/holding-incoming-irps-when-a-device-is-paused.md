---
title: 设备暂停时保持传入的 IRP
description: 设备暂停时保持传入的 IRP
ms.assetid: 4964e06b-f1b9-4421-89d1-ad79ce7d7307
keywords:
- 持有 Irp
- WDK PnP Irp
- I/O 请求数据包 WDK 即插即用
- 正在暂停的即插即用设备
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20c680f3cd8438d462082b9f52a330b655ed9ec2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364301"
---
# <a name="holding-incoming-irps-when-a-device-is-paused"></a>设备暂停时保持传入的 IRP





其资源将被重新平衡时，设备的驱动程序必须暂停设备。 重新平衡资源，在某些驱动程序将暂停在响应中的设备[ **IRP\_MN\_查询\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551725)请求和其他直到它们接收暂停设备驱动程序延迟[ **IRP\_MN\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551755)请求。 在任一情况下，设备必须时暂停**IRP\_MN\_停止\_设备**成功。

驱动程序必须完成在设备上进行任何 Irp 和不启动任何新 Irp 需要访问设备。

若要暂停设备时，请保存 Irp，驱动程序实现的过程如下所示：

1.  在其[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程中，一个名称，如保留设备扩展插件中定义一个标志\_新建\_请求。 清除标志。

2.  创建用于保存 Irp 的先进先出队列。

    如果该驱动程序已排队 Irp，它可以重复使用同一个队列，因为暂停设备之前完成所有未完成请求所需的驱动程序。

    如果该驱动程序尚不包含 IRP 队列，它必须创建一个在其*AddDevice*例程。 它将创建队列的类型取决于驱动程序会在队列的刷新。 驱动程序可能使用互锁、 双向链接列表和**ExInterlocked*Xxx*列表**例程。

3.  在其*DispatchPnP*为代码**IRP\_MN\_查询\_停止\_设备**(或**IRP\_MN\_停止\_设备**)，完成任何未完成的请求和设置保留\_新建\_请求标志。

4.  在访问该设备，如的调度例程[ *DispatchWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)或[ *DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)，检查是否保持\_新建\_请求标志设置。 如果是这样，该驱动程序必须将挂起的 IRP 标记，并在队列中。

    在驱动程序*DispatchPnP*例程必须继续处理 PnP Irp，而不是保存它们并[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程必须继续处理 power Irp。

5.  在中*DispatchPnP*，以响应开始或取消停止 IRP，清除保留\_新建\_请求标志和启动 Irp IRP 控股队列中。

    这些操作可能是用于处理这些 PnP Irp 的最后一个步骤。 例如，开始 IRP 响应，该驱动程序必须首先执行任何操作以启动设备，然后它可以启动 Irp IRP 控股队列中。

    中从 IRP 控股队列处理 Irp 的错误不会影响返回的开始或取消停止 Irp 的状态。

 

 




