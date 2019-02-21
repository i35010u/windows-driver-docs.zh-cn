---
title: PSHED 插件简介
description: PSHED 插件简介
ms.assetid: 31c540ec-c1d0-48e3-9eab-b458a5213f7e
keywords:
- 特定于平台的硬件错误驱动程序插件 WDK WHEA，有关特定于平台的硬件错误驱动程序插件
- PSHED 插件 WDK WHEA，有关特定于平台的硬件错误驱动程序插件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f864db184a687a7128a8e2dda2865dfa6ca115e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540790"
---
# <a name="introduction-to-pshed-plug-ins"></a>PSHED 插件简介


平台供应商可以通过提供 PSHED 插件，充分利用特定于平台的功能补充默认 PSHED 功能。 PSHED 插件是实现一个回调接口，由 PSHED 调用的专用的 Windows 设备驱动程序。 PSHED 插件旨在补充或替代 PSHED 由 Microsoft 提供的默认行为。

作为实现插件 PSHED [Windows 驱动程序模型](https://msdn.microsoft.com/library/windows/hardware/ff565698)(WDM) 设备驱动程序特定的硬件标识符枚举在系统启动时加载插即用 (PnP) 管理器。 平台供应商指定启动加载的插件 PSHED 的硬件标识符。 此硬件标识符可以是在 ACPI 名称空间中，也可以是另一个设备命名空间中。

PSHED 插件不处理任何用户模式应用程序或更高级别驱动程序启动的 I/O 请求。 因此，PSHED 插件仅用于实现驱动程序调度例程 (请参阅[ **DRIVER_DISPATCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)) 来处理[IRP_MJ_PNP](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)和[IRP_MJ_POWER](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power) Irp。 PSHED 插件无需注册设备接口或创建为它们的设备对象的符号链接。

PSHED 插件参与一个或多个以下[功能区域](functional-areas.md)硬件错误的处理与相关联的：

-   [错误源发现](error-source-discovery.md)

-   [错误源控件](error-source-control.md)

-   [错误记录持久性](error-record-persistence.md)

-   [错误的信息检索](error-information-retrieval.md)

-   [错误恢复](error-recovery.md)

-   [错误注入](error-injection.md)

对于每个功能区域，PSHED 插件实现由 PSHED 调用的回调函数。 PSHED 插件指定它参与并提供指向相关联的回调函数的指针的功能区域时它[注册](registering-a-pshed-plug-in.md)与 PSHED 本身。 在同一时间可以与 PSHED 注册多个 PSHED 插件。 但是，如果多个已注册的 PSHED 插件指定参与某一特定功能区域，仅最后一个注册自己实际上将加入该功能区域中。

PSHED 插件旨在由平台供应商为硬件平台的硬件错误报告和恢复功能的软件接口实现。 PSHED 插件可与使用任何专用接口的平台固件或由平台供应商定义的机制。 这样，平台供应商联系以继续使用现有的固件硬件错误处理。 时间，Microsoft 需要更多的硬件错误报告和恢复功能将进行标准化。 此时，PSHED 插件的常规错误处理和报告需求将导致降低以便 PSHED 插件将仅需要支持提供附加价值超出标准硬件错误处理的特定于供应商的功能功能。

 

 




