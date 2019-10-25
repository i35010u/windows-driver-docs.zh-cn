---
title: 在总线驱动程序中删除设备
description: 在总线驱动程序中删除设备
ms.assetid: f3961c29-02e1-41f0-bb7f-784bcdb57eb0
keywords:
- 总线驱动程序 WDK PnP
- DispatchPnP 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 152f83dca65fe5bad3dfb8c999159e0b16a54614
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838454"
---
# <a name="removing-a-device-in-a-bus-driver"></a>在总线驱动程序中删除设备





删除子设备（子 PDO）时，父总线驱动程序必须撤消它为添加和启动设备执行的任何操作。

总线驱动程序在其[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中删除具有如下过程的子设备：

1.  驱动程序是否已处理了以前的[**IRP\_MN\_意外\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)此 PDO 的删除请求？

    如果是这样，请执行剩余的任何清理操作，并跳到步骤4。

    驱动程序通常会在设备扩展中保留一个标志，该标志指示驱动程序是否已处理**IRP\_MN\_** 对该设备的意外\_删除请求。

2.  完成驱动程序中排队的任何请求。

3.  如果总线驱动程序能够执行此操作，请从设备上拔下电源，并通过调用[**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)通知电源管理器。

    总线驱动程序会关闭子设备，如有可能，并通知电源管理器设备的电源状态更改。 总线驱动程序将执行此项以响应[**IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)请求;设备的电源策略所有者在删除设备时不会发送[**IRP\_MN\_集\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)请求。 有关其他信息，请参阅[电源管理](implementing-power-management.md)。

4.  如果总线驱动程序在其对[**IRP\_MN\_查询\_设备\_关系**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)请求中**报告了此设备，则**该设备仍将在物理上出现在计算机上。 在这种情况下，总线驱动程序：

    -   保留设备的 PDO，直到设备被物理删除。

    -   将**Irp&gt;IoStatus**的状态设置\_为 "成功"。

    -   完成 IRP with [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)。

    -   从[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程返回。

    在物理删除设备之前，总线驱动程序必须继续在后续枚举中报告此设备（**IRP\_MN\_查询\_设备\_关系** **）。** PnP 管理器跟踪是否已添加并启动了枚举设备。

5.  如果设备未包括在总线驱动程序对 IRP\_MN 的最新响应中 **\_查询\_设备\_关系**请求**BusRelations**，则总线驱动程序会将设备从物理上删除。设备. 在这种情况下，总线驱动程序会执行以下操作：

    -   清理特定于设备的分配、内存和事件等。

    -   将**Irp&gt;IoStatus**的状态设置\_为 "成功"。

    -   完成 IRP with [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)。

    -   通过[**IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)释放 PDO。

        如果驱动程序从最新的**BusRelations**列表中省略设备，则总线驱动程序必须删除 PDO。 如果用户重新将设备插入到计算机中，则总线驱动程序必须创建新的 PDO 来响应下一**BusRelations**查询。 如果总线驱动程序对新的设备实例重用相同的 PDO，计算机将无法正常运行。

    -   从*DispatchPnP*例程返回。

如果在 PnP 管理器发送 IRP\_MN 时设备仍然存在， **\_删除\_设备**请求，则总线驱动程序将保留 PDO。 如果在以后的某个时间从总线中删除了设备，则 PnP 管理器将发送另一个**IRP\_MN\_删除\_设备**。 接收到后续删除 IRP 后，总线驱动程序将删除设备的 PDO。

总线驱动程序必须能够处理**IRP\_MN\_删除**其已删除且 PDO 标记为删除的设备\_设备。 为了响应此类 IRP，总线驱动程序可以成功执行 IRP 或返回状态\_\_此类\_设备。 尽管总线驱动程序之前对**IoDeleteDevice**的调用，但该设备的 PDO 尚未删除，因为某些组件仍有对该对象的引用。 因此，在处理第二个 remove IRP 时，总线驱动程序可以访问 PDO。 对于 PDO，总线驱动程序不得再次调用**IoDeleteDevice** ;i/o 系统在其引用计数达到零时删除 PDO。

总线驱动程序在接收**IRP\_MN\_删除设备\_设备**请求之前，不会删除其子设备的数据结构。 总线驱动程序可能检测到设备已被删除并调用[**IoInvalidateDeviceRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations)，但在 PnP 管理器发送**IRP\_MN\_删除\_设备**请求之前，该驱动程序不能删除设备的 PDO。

 

 




