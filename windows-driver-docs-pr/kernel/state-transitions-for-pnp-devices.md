---
title: PnP 设备的状态转换
description: PnP 设备的状态转换
ms.assetid: 31969515-899b-407e-ab73-f6f7f36adb85
keywords:
- 即插即用 WDK 内核，状态转换
- 插 WDK 内核，状态转换
- 状态转换 WDK 即插即用
- 设备状态 WDK 即插即用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59b44472d466c52daf24e4d28b4a7448f58104d0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382994"
---
# <a name="state-transitions-for-pnp-devices"></a>PnP 设备的状态转换


## <a href="" id="ddk-state-transitions-for-pnp-devices-kg"></a>


即插即用及的系统上，通过即插即用的各种状态的设备转换的配置，启动，可能已停止，以重新平衡资源，可能删除。 本部分概述的即插即用设备状态。 概述是用于在驱动程序所需的即插即用支持众多的路线图。 本文档其他部分描述了每个状态转换详细信息中。

下图显示即插即用设备和如何在设备从一个状态转换到另一个状态。

![说明从插角度来看的设备状态的关系图](images/pnp-states.png)

开始左上角上图中，即插即用设备是在系统中实际存在，因为用户只需插入设备或设备在启动时出现。 设备还不知道对系统软件。

若要开始在设备的软件配置，即插即用管理器和父总线驱动程序枚举设备。 PnP 管理器中，可能是用户模式组件的帮助下，标识设备，包括功能驱动程序和任何可选的筛选器驱动程序的驱动程序。 PnP 管理器调用[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程的每个驱动程序，如果尚未加载该驱动程序。 有关报告并枚举即插即用设备的详细信息，请参阅[添加到运行系统的即插即用设备](adding-a-pnp-device-to-a-running-system.md)。

初始化一个驱动程序，它必须准备好初始化其设备。 PnP 管理器中调用的驱动程序[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例行为每个设备驱动程序控制。

当驱动程序收到[ **IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求从 PnP 管理器中，该驱动程序使设备开始，并已准备好处理 I/O 请求设备。 有关处理信息**IRP\_MN\_启动\_设备**请求，请参阅[启动设备](starting-a-device.md)。

如果 PnP 管理器必须重新配置的活动设备的硬件资源，则会发送[ **IRP\_MN\_查询\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)和[**IRP\_MN\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)对设备的驱动程序的请求。 PnP 管理器重新配置硬件资源后，将驱动程序以重启设备，通过发送定向[ **IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求。 有关处理信息停止 Irp，请参阅[停止设备](stopping-a-device.md)。 (启动配置设备的驱动程序可以接收**IRP\_MN\_查询\_停止\_设备**并**IRP\_MN\_停止\_设备**请求之前启动设备后，尽管此步骤中未显示在上图中。)

在 Windows 98 上 / 我，即插即用管理器还会发送**IRP\_MN\_查询\_停止\_设备**并**IRP\_MN\_停止\_设备**请求时设备将被禁用。 这些系统上的驱动程序还会收到**IRP\_MN\_停止\_设备**后失败的启动请求。

当即插即用设备正在以物理方式从系统删除或已删除时，PnP 管理器将发送各种删除 Irp 到设备的驱动程序引导他们以删除设备的软件表示形式 （设备对象等）。 有关处理信息删除 Irp，请参阅[删除设备](removing-a-device.md)。

在某一时刻已删除的所有驱动程序的设备后，即插即用管理器调用的驱动程序[ *Unload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)例程并卸载该驱动程序。

 

 




