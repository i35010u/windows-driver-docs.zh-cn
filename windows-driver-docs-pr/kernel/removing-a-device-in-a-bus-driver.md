---
title: 在总线驱动程序中删除设备
description: 在总线驱动程序中删除设备
keywords:
- 总线驱动程序 WDK PnP
- DispatchPnP 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7c76e3ca4758f71e9ff70a3303d967474907f4e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834447"
---
# <a name="removing-a-device-in-a-bus-driver"></a>在总线驱动程序中删除设备





 (子 PDO) 删除子设备时，父总线驱动程序必须撤消它为添加和启动设备执行的任何操作。

总线驱动程序在其 [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程中删除具有如下过程的子设备：

1.  驱动程序是否已处理此 PDO 的以前的 [**IRP \_ MN \_ 意外 \_ 删除**](./irp-mn-surprise-removal.md) 请求？

    如果是这样，请执行剩余的任何清理操作，并跳到步骤4。

    驱动程序通常在设备扩展中维护一个标志，该标志指示驱动程序是否已处理对设备的 **IRP \_ MN \_ 意外 \_ 删除** 请求。

2.  完成驱动程序中排队的任何请求。

3.  如果总线驱动程序能够执行此操作，请从设备上拔下电源，并通过调用 [**PoSetPowerState**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)通知电源管理器。

    总线驱动程序会关闭子设备，如有可能，并通知电源管理器设备的电源状态更改。 总线驱动程序将执行此项以响应 [**IRP \_ MN \_ REMOVE \_ 设备**](./irp-mn-remove-device.md) 请求; 设备的电源策略所有者在删除设备时不会发送 [**IRP \_ MN \_ 设置 \_ 电源**](./irp-mn-set-power.md) 请求。 有关其他信息，请参阅 [电源管理](./introduction-to-power-management.md)。

4.  如果总线驱动程序已将此设备报告到针对 **BusRelations** 的 [**IRP \_ MN \_ 查询 \_ 设备 \_ 关系**](./irp-mn-query-device-relations.md)请求，则该设备仍将在物理上出现在计算机上。 在这种情况下，总线驱动程序：

    -   保留设备的 PDO，直到设备被物理删除。

    -   将 **&gt; IoStatus** 状态设置为 "成功" \_ 。

    -   完成 IRP with [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)。

    -   从 [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程返回。

    总线驱动程序必须在后续枚举中继续报告此设备 (**IRP \_ MN \_ 查询 \_ 设备 \_ 关系** for **BusRelations**) ，直到设备被物理删除。 PnP 管理器跟踪是否已添加并启动了枚举设备。

5.  如果设备未包括在总线驱动程序的 **IRP \_ MN \_ 查询 \_ 设备 \_ 关系** 请求 **BusRelations** 中，则总线驱动程序会将设备从物理上删除。 在这种情况下，总线驱动程序会执行以下操作：

    -   清理特定于设备的分配、内存和事件等。

    -   将 **&gt; IoStatus** 状态设置为 "成功" \_ 。

    -   完成 IRP with [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)。

    -   通过 [**IoDeleteDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)释放 PDO。

        如果驱动程序从最新的 **BusRelations** 列表中省略设备，则总线驱动程序必须删除 PDO。 如果用户重新将设备插入到计算机中，则总线驱动程序必须创建新的 PDO 来响应下一 **BusRelations** 查询。 如果总线驱动程序对新的设备实例重用相同的 PDO，计算机将无法正常运行。

    -   从 *DispatchPnP* 例程返回。

如果 PnP 管理器发送 **IRP \_ MN \_ REMOVE \_ 设备** 请求时设备仍存在，则总线驱动程序将保留 PDO。 如果在以后的某个时间从总线中删除了设备，则 PnP 管理器将发送另一个 **IRP \_ MN \_ 删除 \_ 设备**。 接收到后续删除 IRP 后，总线驱动程序将删除设备的 PDO。

总线驱动程序必须能够为它已删除且 PDO 标记为删除的设备处理 **IRP \_ MN \_ 删除 \_ 设备** 。 为了响应此类 IRP，总线驱动程序可以成功完成 IRP 或返回状态 " \_ 无 \_ 此类 \_ 设备"。 尽管总线驱动程序之前对 **IoDeleteDevice** 的调用，但该设备的 PDO 尚未删除，因为某些组件仍有对该对象的引用。 因此，在处理第二个 remove IRP 时，总线驱动程序可以访问 PDO。 对于 PDO，总线驱动程序不得再次调用 **IoDeleteDevice** ;i/o 系统在其引用计数达到零时删除 PDO。

在接收到设备的 **IRP \_ MN \_ remove \_ 设备** 请求之前，总线驱动程序不会删除其子设备的数据结构。 总线驱动程序可能检测到设备已被删除并调用 [**IoInvalidateDeviceRelations**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations)，但在 PnP 管理器发送 **IRP \_ MN \_ 删除 \_ 设备** 请求之前，不能删除设备的 PDO。

 

