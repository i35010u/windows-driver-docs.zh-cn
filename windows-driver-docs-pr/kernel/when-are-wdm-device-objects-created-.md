---
title: 何时创建 WDM 设备对象
description: 何时创建 WDM 设备对象
ms.assetid: aeb8039d-2e5d-4700-a9e5-e5ee97c6b0b1
keywords:
- 设备对象在创建时的 WDK 内核
- 分层设备对象 WDK 内核
- 功能设备对象 WDK 内核
- FDO WDK 内核
- 物理设备对象 WDK 内核
- PDOs WDK 内核
- 筛选 DOs WDK 内核
- 设备堆栈 WDK 内核，设备对象层可能
- 附加设备对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9f74cd5c7bd23998fede8cdb05b92136a449bcc
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189253"
---
# <a name="when-are-wdm-device-objects-created"></a>何时创建 WDM 设备对象？





本部分介绍每种类型的设备对象以及每个设备对象的提到。

下图显示了可以附加到设备堆栈中的设备对象的可能类型，这些对象表示设备的驱动程序处理 i/o 请求。

![说明设备可能的设备对象层的关系图](images/objlyr.png)

从此图底部开始：

-   总线驱动程序为它在其总线上枚举的每个设备创建一个 PDO。

    总线驱动程序在枚举设备时为其子设备创建 PDO。 总线驱动程序会枚举设备，以响应对 PnP 管理器中**BusRelations**的[**IRP \_ MN \_ 查询 \_ 设备 \_ 关系**](./irp-mn-query-device-relations.md)请求。 如果自上一次总线驱动程序对 (**BusRelations** 的查询关系请求进行了响应，则总线驱动程序会为子设备创建一个 PDO，如果这是自计算机启动以来第一个查询关系请求) ，则为。

    PDO 表示设备到总线驱动程序以及其他内核模式系统组件（例如，电源管理器、PnP 管理器和 i/o 管理器）。

    设备的其他驱动程序在 PDO 顶部附加设备对象，但 PDO 始终位于设备堆栈的底部。

-   可选的总线筛选器驱动程序为其筛选的每个设备创建筛选器 DOs。

    当 PnP 管理器检测到 **BusRelations** 列表中的新设备时，它将确定设备是否有任何总线筛选器驱动程序。 如果是这样，则对于每个此类驱动程序，PnP 管理器都确保 (调用 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) ，如有必要) 并调用驱动程序的 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程。 如果总线筛选器驱动程序筛选此设备的操作，筛选器驱动程序将创建一个设备对象，并将其连接到其 *AddDevice* 例程中的设备堆栈。 如果存在多个总线筛选器驱动程序，并且这些驱动程序与此设备相关，则每个此类筛选器驱动程序将创建并附加其自己的设备对象。

-   可选的低级别筛选器驱动程序为其筛选的每个设备创建筛选器 DOs。

    如果此设备有一个可选的低级别筛选器驱动程序，则 PnP 管理器可确保在总线驱动程序和任何总线筛选器驱动程序之后加载此类驱动程序。 PnP 管理器调用筛选器驱动程序的 *AddDevice* 例程。 在其 *AddDevice* 例程中，低级筛选器驱动程序为设备创建筛选器，并将其附加到设备堆栈。 如果存在多个低级筛选器驱动程序，则每个此类驱动程序都将创建并附加自己的筛选器。

-   函数驱动程序为设备创建 FDO。

    PnP 管理器可确保加载设备的函数驱动程序并调用函数驱动程序的 *AddDevice* 例程。 函数驱动程序创建一个 FDO 并将其附加到设备堆栈。

-   可选，上层筛选器驱动程序为其筛选的每个设备创建筛选器。

    如果设备有任何可选的高级筛选器驱动程序，则 PnP 管理器可确保在函数驱动程序之后加载这些驱动程序并调用其 *AddDevice* 例程。 每个此类筛选器驱动程序会将其设备对象附加到设备堆栈。

在摘要中，设备堆栈包含每个驱动程序的设备对象，每个驱动程序都涉及到对特定设备的 i/o 处理。 父总线驱动程序具有 PDO，函数驱动程序具有 FDO，并且每个可选筛选器驱动程序都具有筛选器。

请注意，所有设备、总线适配器/控制器设备和 nonbus 设备在其设备堆栈中都有一个 PDO 和一个 FDO。 总线适配器/控制器的 PDO 由父总线的总线驱动程序创建。 例如，如果 SCSI 适配器插入 PCI 总线，PCI 总线驱动程序将为 SCSI 适配器创建 PDO。

如果在 raw 模式下使用设备，则没有任何 FDO 或 filter DOs)  (的函数或筛选器驱动程序。 父总线驱动程序和零个或多个总线筛选器 DOs 只有一个 PDO。

请参阅 [创建设备对象](creating-a-device-object.md) ，获取有关哪些驱动程序例程负责创建和附加设备对象的信息。

设备堆栈以及一些其他信息构成了设备的 *devnode* 。 PnP 管理器会在设备的 devnode 中维护信息，例如设备是否已启动以及哪些驱动程序（如果有）已注册到设备上的更改通知。 内核调试器命令 **！ devnode** 显示有关 devnode 的信息。

 

