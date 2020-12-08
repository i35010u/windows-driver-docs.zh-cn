---
title: PnP 驱动程序设计指导原则
description: PnP 驱动程序设计指导原则
keywords:
- PnP WDK 内核，设计指南
- 即插即用 WDK 内核，设计指南
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e37485f98599e296675ad63312892e684c47e354
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838443"
---
# <a name="pnp-driver-design-guidelines"></a>PnP 驱动程序设计指导原则





即插即用提供：

-   自动和动态识别已安装的硬件

-   硬件资源分配 (和重新分配) 

-   加载相应的驱动程序

-   用于与 PnP 系统交互的驱动程序的接口

-   驱动程序和应用程序用于了解硬件环境中的更改的机制

若要支持 PnP，驱动程序必须遵循以下准则：

-   它必须包含 [*DispatchPnP*](./dispatchpnp-routines.md) 例程。

    此调度例程必须处理 [**IRP \_ MJ \_ PNP**](./irp-mj-pnp.md) 请求和相关的次要函数代码。 有关详细信息，请参阅 [DispatchPnP 例程](dispatchpnp-routines.md)。

-   它不得搜索硬件。

    PnP 管理器负责确定硬件设备是否存在。 当 PnP 管理器检测到设备时，它会通过调用其 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程通知驱动程序。 可在系统启动时或用户将设备添加到正在运行的系统中的任何时间检测到硬件。

-   它不能分配硬件资源。

    PnP 驱动程序必须为 PnP 管理器提供设备可能会使用的资源列表。 PnP 管理器负责将资源分配给每个设备，并在其发送 [**IRP \_ MN \_ START \_ 设备**](./irp-mn-start-device.md) 请求时通知每个设备的分配的驱动程序。 因此，该驱动程序必须能够使用各种硬件资源配置。

某些驱动程序与系统提供的端口或类驱动程序的 PnP 和电源管理的详细信息分开。 例如，SCSI 端口驱动程序将 SCSI 微型端口驱动程序与电源和 PnP 系统的许多详细信息隔离开来，因此，SCSI 微型端口驱动程序不需要直接处理电源和 PnP Irp。 有关此类驱动程序，请参阅特定于驱动程序的文档以了解所需 PnP 支持的详细信息。

 

