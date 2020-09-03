---
title: DispatchPnP 例程
description: DispatchPnP 例程
ms.assetid: 909d99ac-5bd3-4b12-bfb4-79713cf2a156
keywords:
- 调度例程 WDK 内核，DispatchPnP 例程
- DispatchPnP 例程
- PnP 调度例程 WDK 内核
- Irp WDK 内核，即插即用调度例程
- 即插即用调度例程 WDK 内核
- IRP_MJ_PNP i/o 函数代码
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d868199cde20249350cc168778955e0d4dc9f4b6
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403228"
---
# <a name="dispatchpnp-routines"></a>DispatchPnP 例程





驱动程序的[*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程通过处理[**irp \_ MJ \_ PNP**](./irp-mj-pnp.md) i/o 函数代码的 irp 来支持[即插即用](introduction-to-plug-and-play.md)。 与 **IRP \_ MJ \_ PNP** 函数代码关联的是多个次要 i/o 函数代码 (参阅 [即插即用次要 irp](./plug-and-play-minor-irps.md)) ，其中一些驱动程序必须处理，其中某些驱动程序必须可以选择处理。 PnP 管理器使用这些次要函数代码指示驱动程序启动、停止和删除设备，并查询有关其设备的驱动程序。

设备的所有驱动程序都必须有机会处理设备的 PnP Irp，但在某些情况下，允许函数或筛选器驱动程序失败 IRP 的情况除外。

每个驱动程序的 *DispatchPnP* 例程必须遵循以下规则：

-   函数或筛选器驱动程序必须将 PnP Irp 向下传递到设备堆栈中的下一个驱动程序，除非函数或筛选器驱动程序处理 IRP，并因资源不足而遇到故障 (例如) 。

    设备的所有驱动程序都必须有机会为设备处理 PnP Irp，除非其中一个驱动程序遇到错误。 PnP 管理器将 Irp 发送到设备堆栈中的顶部驱动程序。 函数和筛选器驱动程序将 IRP 传递到下一个驱动程序，并且父总线驱动程序完成 IRP。 有关详细信息，请参阅 [将 PnP Irp 传递到设备堆栈中](passing-pnp-irps-down-the-device-stack.md) 。

    如果 IRP 试图处理 IRP 并遇到错误 (例如资源不足) ，则该驱动程序可能会失败。 如果驱动程序收到的 IRP 的代码不是，则该驱动程序不能使 IRP 失败。 它必须将此类 IRP 传递到下一个驱动程序，而无需修改 IRP 的状态。

-   驱动程序必须处理某些 PnP Irp，还可以选择处理其他 Irp。

    需要每个 PnP 驱动程序来处理某些 Irp，如 [**irp \_ MN \_ REMOVE \_ DEVICE**](./irp-mn-remove-device.md)，还可以选择处理其他 irp。 请参阅 [即插即用次 irp](./plug-and-play-minor-irps.md) ，获取有关所需的 irp 的信息，以及每种驱动程序 (函数驱动程序、筛选器驱动程序和总线驱动程序) 的可选信息。

    驱动程序可能会使所需的 PnP IRP 失败，并出现相应的错误状态，但驱动程序不能返回 \_ \_ 此类 IRP 不支持的状态。

-   如果驱动程序成功处理 PnP IRP，驱动程序会将 IRP 状态设置为 "成功"。 它不依赖于堆栈中的另一个驱动程序来设置状态。

    驱动程序将 **Irp- &gt; IoStatus** 设置为状态 " \_ 成功" 以通知 PnP 管理器驱动程序已成功处理 Irp。 对于某些 Irp，非总线驱动程序可能能够依赖其父总线驱动程序将状态设置为 "成功"。 但这是一种风险的做法。 为了保持一致性和可靠性，驱动程序必须将 IRP 状态设置为成功处理的每个 PnP IRP。

-   如果某个驱动程序失败了 IRP，则该驱动程序将完成 IRP 并带有错误状态，并且不会将 IRP 向下传递到下一个驱动程序。

    为了使 irp （如 [**irp \_ MN \_ QUERY \_ 停止 \_ 设备**](./irp-mn-query-stop-device.md)）失败，驱动程序将 **irp- &gt; IoStatus** 设置为状态 "未 \_ 成功"。 其他 Irp 的其他错误状态值包括 " \_ 资源不足" \_ 和 "状态 \_ 无效" \_ 设备 \_ 状态。

    \_对于它们处理的 irp，驱动程序不会设置 \_ 其状态。 这是 PnP 管理器设置的初始状态。 如果 IRP 完成时具有此状态，则意味着堆栈中没有驱动程序处理 IRP;所有驱动程序都将 IRP 传递到下一个驱动程序。

-   驱动程序必须在其调度例程中处理 PnP IRP， (按照 irp 中的设备堆栈) ，在 [**IoCompletion**](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程 (基于 irp 的 "引用" 页中所指定的) 方法，在

    某些 PnP Irp （如 [**IRP \_ MN \_ REMOVE \_ DEVICE**](./irp-mn-remove-device.md)）必须首先由设备堆栈顶部的驱动程序处理，然后再由下一个低的驱动程序处理。 其他人（如 [**IRP \_ MN \_ START \_ DEVICE**](./irp-mn-start-device.md)）必须首先由父总线驱动程序处理。 还有其他一些功能，如 [**IRP \_ MN \_ 查询 \_ 功能**](./irp-mn-query-capabilities.md)，可同时在设备堆栈和备份的方式上进行处理。 请参阅即插即用适用于每个 PnP IRP 的规则的 [次要 irp](./plug-and-play-minor-irps.md) 。 请参阅 [推迟 PNP IRP 处理，直到较低版本的驱动程序完成](postponing-pnp-irp-processing-until-lower-drivers-finish.md) 有关处理 PnP irp （必须首先由父总线驱动程序处理）的信息。

-   驱动程序必须将信息添加到 IRP 上的 IRP，并按设备堆栈向下修改或删除有关 IRP 的备份方法的信息。

    当返回响应 PnP 查询 IRP 的信息时，驱动程序必须遵循此约定，以支持设备的分层驱动程序传递有序的信息。

-   除了明确记录的情况外，驱动程序不能依赖于以任何特定顺序发送 PnP Irp。

-   当驱动程序发送 PnP IRP 时，它必须将 IRP 发送到设备堆栈中的顶层驱动程序。

    大多数 PnP Irp 由 PnP 管理器发送，但有些可由驱动程序发送 (例如， [**IRP \_ MN \_ QUERY \_ INTERFACE**](./irp-mn-query-interface.md)) 。 驱动程序必须将 PnP IRP 发送到设备堆栈顶部的驱动程序。 调用 [**IoGetAttachedDeviceReference**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetattacheddevicereference) 可获取指向设备堆栈顶部驱动程序的设备对象的指针。


 

