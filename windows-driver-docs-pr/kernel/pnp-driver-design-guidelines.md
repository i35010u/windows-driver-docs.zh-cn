---
title: PnP 驱动程序设计指导原则
description: PnP 驱动程序设计指导原则
ms.assetid: 4e4a6a8e-3c7f-4561-bbe1-a8c06fe22d0a
keywords:
- 即插即用 WDK 内核，设计指南
- 插 WDK 内核，设计指南
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbd66ec8c5055c10df64245ef73315e0d7deb7ef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383280"
---
# <a name="pnp-driver-design-guidelines"></a>PnP 驱动程序设计指导原则





插提供：

-   自动和动态识别的已安装硬件

-   硬件资源分配 （和重新分配）

-   正在加载的合适的驱动程序

-   与即插即用系统进行交互的驱动程序接口

-   驱动程序和应用程序若要了解硬件环境中的更改的机制

若要支持即插即用，驱动程序必须遵循以下准则：

-   它必须包含[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchpnp-routines#feedback)例程。

    必须处理此调度例程[ **IRP\_MJ\_PNP** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)请求和关联的次要函数代码。 有关详细信息，请参阅[DispatchPnP 例程](dispatchpnp-routines.md)。

-   它必须搜索硬件。

    PnP 管理器负责确定硬件设备存在。 当 PnP 管理器检测到设备时，它将通知该驱动程序通过调用其[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程。 启动系统，或任何时候用户添加的设备，或从正在运行的系统中删除时，可以检测到硬件。

-   它必须分配硬件资源。

    即插即用驱动程序必须提供的设备有可能使用的资源的列表的即插即用管理器。 PnP 管理器负责将资源分配给每个设备，以及时它将发送通知的每个设备分配驱动程序[ **IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求。 因此，驱动程序必须能够使用硬件资源的各种配置。

某些驱动程序可独立的即插即用的详细信息和系统提供的端口或类驱动程序的电源管理。 例如，SCSI 端口驱动程序隔离的 SCSI 微型端口驱动程序由许多的强大功能和即插即用系统的详细信息，因此不需要直接处理能力和 PnP Irp SCSI 微型端口驱动程序。 此类驱动程序，请参阅所需的即插即用支持的详细信息的特定于驱动程序的文档。

 

 




