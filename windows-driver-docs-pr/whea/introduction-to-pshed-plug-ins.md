---
title: PSHED 插件简介
description: PSHED 插件简介
ms.assetid: 31c540ec-c1d0-48e3-9eab-b458a5213f7e
keywords:
- 平台特定硬件错误驱动程序插件 WDK WHEA，关于特定于平台的硬件错误驱动程序插件
- PSHED 插件 WDK WHEA，关于特定于平台的硬件错误驱动程序插件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee857070490c7c2888bea13bd1eab17b58a1e117
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844398"
---
# <a name="introduction-to-pshed-plug-ins"></a>PSHED 插件简介


平台供应商可以通过提供利用特定于平台的功能的 PSHED 插件来补充默认的 PSHED 功能。 PSHED 插件是一种特殊用途的 Windows 设备驱动程序，可实现 PSHED 调用的回调接口。 PSHED 插件的用途是增加或覆盖 Microsoft 提供的 PSHED 的默认行为。

在系统启动期间枚举特定硬件标识符时，PSHED 插件作为即插即用（PnP）管理器加载的[Windows 驱动模型](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)（WDM）设备驱动程序实现。 平台供应商指定启动 PSHED 插件加载的硬件标识符。 此硬件标识符可以位于 ACPI 命名空间中，也可以位于另一个设备命名空间中。

PSHED 插件不会处理用户模式应用程序或更高级别的驱动程序启动的任何 i/o 请求。 因此，只需实施驱动程序调度例程（请参阅[**DRIVER_DISPATCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)）来处理[IRP_MJ_PNP](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)和[IRP_MJ_POWER](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power) irp，PSHED 插件才是必需的。 PSHED 插件不必注册设备接口或为其设备对象创建符号链接。

PSHED 插件参与了与硬件错误处理相关的以下一个或多个[功能区域](functional-areas.md)：

-   [错误源发现](error-source-discovery.md)

-   [错误源代码管理](error-source-control.md)

-   [错误记录持久性](error-record-persistence.md)

-   [检索错误信息](error-information-retrieval.md)

-   [错误恢复](error-recovery.md)

-   [错误注入](error-injection.md)

对于每个功能区域，PSHED 插件实现由 PSHED 调用的回调函数。 PSHED 插件指定它所参与的功能区域，并在向 PSHED[注册](registering-a-pshed-plug-in.md)自身时提供指向关联的回调函数的指针。 可以同时向 PSHED 注册多个 PSHED 插件。 但是，如果有多个已注册的 PSHED 插件指定它参与某个特定功能区域，则只有最后一个注册到该功能区域，才会实际参与该功能区域。

PSHED 插件旨在由平台供应商实现为硬件平台硬件错误报告和恢复功能的软件接口。 使用平台供应商定义的任何专用接口或机制，PSHED 插件可与平台固件交互。 这允许平台供应商继续使用现有固件进行硬件错误处理。 在此期间，Microsoft 期望将更多的硬件错误报告和恢复功能标准化。 此时，需要对 PSHED 插件进行常规错误处理和报告，因此，只有在支持特定于供应商的功能的情况下才需要 PSHED 插件，这些功能提供了超出标准硬件错误处理的额外价值性能.

 

 




