---
title: 当创建 WDM 设备对象
description: 当创建 WDM 设备对象
ms.assetid: aeb8039d-2e5d-4700-a9e5-e5ee97c6b0b1
keywords:
- 设备对象 WDK 内核，在创建时
- 分层式的设备对象 WDK 内核
- 功能的设备对象 WDK 内核
- FDO WDK 内核
- 物理设备对象 WDK 内核
- PDOs WDK 内核
- 筛选器 DOs WDK 内核
- 设备堆栈 WDK 内核，可能的设备对象层
- 附加设备对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ed3b8b263e8997a5175d4ef3f29c0a84fe25d84
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358106"
---
# <a name="when-are-wdm-device-objects-created"></a>何时创建 WDM 设备对象？





本部分介绍每种设备对象，并提到时创建的每条。

下图显示可能类型的可附加的设备对象表示处理 I/O 请求设备的驱动程序的设备堆栈中。

![说明可能的设备的设备的对象层关系图](images/objlyr.png)

在此图底部开始：

-   总线驱动程序在其总线上创建它枚举每个设备一个 PDO。

    当枚举设备时，总线驱动程序创建了子设备 PDO。 总线驱动程序枚举响应中的设备[ **IRP\_MN\_查询\_设备\_关系**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)请求**BusRelations**从 PnP 管理器。 如果设备已添加到总线自上次总线驱动程序的子设备响应的查询-关系请求总线驱动程序创建 PDO **BusRelations** (或者如果这是因为第一个查询关系请求计算机已启动）。

    PDO 总线驱动程序，以及电源管理器、 即插即用管理器和 I/O 管理器等其他内核模式系统组件表示的设备。

    其他驱动程序为设备附加设备对象之上 PDO，但 PDO 是始终在设备堆栈的底部。

-   可选总线筛选器驱动程序创建筛选器 DOs 中筛选出每个设备。

    当 PnP 管理器检测到中的新设备**BusRelations**列表中，它确定是否有任何设备的总线筛选器驱动程序。 因此，对于每个此类驱动程序 PnP 管理器可确保它是否已加载 (调用[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)如有必要)，并调用在驱动程序[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程。 如果总线筛选器驱动程序筛选器用于此设备的操作，筛选器驱动程序创建一个设备对象并将其附加到的设备堆栈中其*AddDevice*例程。 如果多个总线筛选器驱动程序存在，并且与此设备，每个此类筛选器驱动程序创建，并将其自己的设备对象。

-   可选的较低级别的筛选器驱动程序创建筛选器 DOs 中筛选出每个设备。

    如果可选的较低级别筛选器驱动程序存在为此设备，即插即用管理器可确保这样的驱动程序被加载时总线驱动程序和任何总线筛选器驱动程序。 PnP 管理器调用筛选器驱动程序*AddDevice*例程。 在其*AddDevice*例程，较低级别筛选器驱动程序创建的设备的筛选器执行操作并将其附加到设备堆栈。 如果存在多个较低级别筛选器驱动程序，每个此类驱动程序将创建并附加自己的筛选器执行操作。

-   功能驱动程序创建设备 FDO。

    PnP 管理器可确保设备的功能驱动程序加载，并调用功能驱动程序*AddDevice*例程。 功能驱动程序创建 FDO，并将其附加到设备堆栈。

-   可选的较高级别筛选器驱动程序创建每个设备中筛选出的筛选的器执行操作。

    如果任何可选的较高级别筛选器驱动程序存在设备，即插即用管理器可确保它们是加载后该功能驱动程序并调用其*AddDevice*例程。 每个此类筛选器驱动程序将其设备对象附加到设备堆栈。

总之，设备堆栈包含到特定设备处理 I/O 中涉及的每个驱动程序的设备对象。 父总线驱动程序有一个 PDO、 功能驱动程序具有 FDO 和每个可选的筛选器驱动程序有筛选器执行操作。

请注意，所有设备、 总线适配器/控制器设备和 nonbus 设备 PDO 和 FDO 其设备堆栈中。 总线适配器/控制器 PDO 创建的父总线总线驱动程序。 例如，如果 SCSI 适配器插入 PCI 总线，PCI 总线驱动程序将创建该 SCSI 适配器的 PDO。

如果设备 raw 模式中使用，没有函数或筛选器驱动程序 （任何 FDO 或筛选器 DOs）。 没有只是一个父总线驱动程序和零个或多个总线筛选器 DOs 的 PDO。

请参阅[创建一个设备对象](creating-a-device-object.md)有关哪些驱动程序例程的负责创建和附加设备对象。

设备堆栈加上一些额外信息构成*devnode*设备。 PnP 管理器中维护信息，例如设备是否已启动和哪些驱动程序的设备的 devnode 如果有，已注册的设备上的更改通知。 内核调试程序命令 **！ devnode**显示 devnode 有关的信息。

 

 




