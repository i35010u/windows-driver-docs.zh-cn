---
title: 在总线驱动程序中删除设备
description: 在总线驱动程序中删除设备
ms.assetid: f3961c29-02e1-41f0-bb7f-784bcdb57eb0
keywords:
- 总线驱动程序 WDK 即插即用
- DispatchPnP 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 458d7ddcb9c339d395d7ed64be7ef1b7c61f1aba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373426"
---
# <a name="removing-a-device-in-a-bus-driver"></a>在总线驱动程序中删除设备





父总线驱动程序时删除子设备 （子 PDO），必须撤消任何操作它执行添加和启动设备。

总线驱动程序将如下所示中的过程与子设备中删除其[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程：

1.  已处理该驱动程序上一次[ **IRP\_MN\_惊讶\_删除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)此 PDO 请求？

    如果是这样，执行任何剩余的清理并跳到步骤 4。

    驱动程序通常维护设备扩展，该值指示是否已处理该驱动程序中的标志**IRP\_MN\_惊讶\_删除**对设备的请求。

2.  完成的任何请求排队驱动程序中。

3.  从设备删除 power 总线驱动程序是否能够执行此操作，并通过调用通知电源管理器[ **PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-posetpowerstate)。

    如果可能，总线驱动程序关闭子设备，并通知的设备的电源状态更改电源管理器。 总线驱动程序执行此响应[ **IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)请求; 设备的电源策略所有者不会发送[**IRP\_MN\_设置\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)请求时删除该设备。 有关其他信息，请参阅[电源管理](implementing-power-management.md)。

4.  如果总线驱动程序报告此设备以其最新响应[ **IRP\_MN\_查询\_设备\_关系**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations) 请求**BusRelations**，设备是物理计算机上存在。 在此情况下，总线驱动程序：

    -   将保留设备 PDO，直到已以物理方式删除设备。

    -   集**Irp-&gt;IoStatus.Status**于状态\_成功。

    -   完成与 IRP [ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)。

    -   返回从[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

    总线驱动程序必须继续报告此设备在后续枚举中的 (**IRP\_MN\_查询\_设备\_关系**为**BusRelations**) 以物理方式删除设备之前。 跟踪是否已添加并开始枚举的设备的即插即用管理器。

5.  如果设备未包含在总线驱动程序的最新响应**IRP\_MN\_查询\_设备\_关系**请求**BusRelations**，总线驱动程序会考虑从计算机中以物理方式删除设备。 在这种情况下，总线驱动程序执行以下任务：

    -   清除特定于设备的分配、 内存、 事件和等。

    -   集**Irp-&gt;IoStatus.Status**于状态\_成功。

    -   完成与 IRP [ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)。

    -   释放与 PDO [ **IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice)。

        如果该驱动程序省略其最新的设备，总线驱动程序必须删除 PDO **BusRelations**列表。 如果用户再次插入到计算机的设备，总线驱动程序必须响应到下一步中创建新 PDO **BusRelations**查询。 如果总线驱动程序重复使用相同的设备的新实例 PDO，计算机将无法正常运行。

    -   返回从*DispatchPnP*例程。

如果该设备仍然存在时即插即用管理器发送**IRP\_MN\_删除\_设备**请求，总线驱动程序将保留 PDO。 如果在以后某一时间，该设备以物理方式移除从总线，即插即用管理器将发送另一个**IRP\_MN\_删除\_设备**。 收到后的后续删除 IRP，总线驱动程序删除设备 PDO。

总线驱动程序必须能够处理**IRP\_MN\_删除\_设备**设备它已移除和其 PDO 标记为待删除。 在响应此类 IRP，总线驱动程序可以成功 IRP 或返回状态\_否\_SUCH\_设备。 设备 PDO 尚未在这种情况下，删除总线驱动程序的以前调用尽管**IoDeleteDevice**，这是因为某些组件仍具有对对象的引用。 因此，总线驱动程序可以处理第二个删除 IRP 时访问 PDO。 总线驱动程序不能调用**IoDeleteDevice** PDO; 第二次 I/O 系统将删除 PDO 当其引用计数达到零时。

总线驱动程序不会删除子设备及其数据结构，直到收到**IRP\_MN\_删除\_设备**对设备的请求。 总线驱动程序可能会检测设备已删除，并调用[ **IoInvalidateDeviceRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinvalidatedevicerelations)，但 PnP 管理器将发送之前必须删除设备的 PDO **IRP\_MN\_删除\_设备**请求。

 

 




