---
title: PnP 设备的状态转换
description: PnP 设备的状态转换
ms.assetid: 31969515-899b-407e-ab73-f6f7f36adb85
keywords:
- PnP WDK 内核，状态转换
- 即插即用 WDK 内核，状态转换
- 状态转换 WDK PnP
- 设备状态 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c5d0e011bb9e06cff7a247116fcc44e765527b7
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184743"
---
# <a name="state-transitions-for-pnp-devices"></a>PnP 设备的状态转换


## <a href="" id="ddk-state-transitions-for-pnp-devices-kg"></a>


在 PnP 系统上，设备会在配置、启动时通过各种 PnP 状态进行转换，并可能已停止重新平衡资源，并可能被删除。 本部分提供 PnP 设备状态的概述。 概述介绍了驱动程序所需的大部分 PnP 支持。 此文档的其他部分详细介绍了每种状态转换。

下图显示了设备的 PnP 状态以及设备如何从一种状态转换到另一种状态。

![从即插即用角度说明设备状态的示意图](images/pnp-states.png)

从上图的左上角开始，PnP 设备在物理上出现在系统中，因为刚插入设备的用户或设备在启动时都存在。 设备对于系统软件尚不可知。

若要开始设备的软件配置，PnP 管理器和父总线驱动程序将枚举设备。 PnP 管理器可能会提供用户模式组件的帮助，其中标识了设备的驱动程序，包括功能驱动程序和任何可选的筛选器驱动程序。 如果尚未加载驱动程序，PnP 管理器将调用每个驱动程序的 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程。 有关报告和枚举 PnP 设备的详细信息，请参阅 [将 Pnp 设备添加到正在运行的系统](adding-a-pnp-device-to-a-running-system.md)。

初始化驱动程序后，必须准备好对其设备进行初始化。 PnP 管理器会为驱动程序控制的每个设备调用驱动程序的 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程。

当驱动程序从 PnP 管理器接收 [**IRP \_ MN \_ 开始 \_ 设备**](./irp-mn-start-device.md) 请求时，驱动程序将启动设备，并准备好处理设备的 i/o 请求。 有关处理 **IRP \_ MN \_ 启动 \_ 设备** 请求的信息，请参阅 [启动设备](starting-a-device.md)。

如果 PnP 管理器必须重新配置活动设备的硬件资源，则会将 [**irp \_ MN \_ QUERY \_ stop \_ device**](./irp-mn-query-stop-device.md) 和 [**irp \_ MN \_ STOP \_ device**](./irp-mn-stop-device.md) requests 发送到设备的驱动程序。 重新配置硬件资源后，PnP 管理器会通过发送 [**IRP \_ MN \_ START \_ 设备**](./irp-mn-start-device.md) 请求来指示驱动程序重启设备。 有关处理停止 Irp 的信息，请参阅 [停止设备](stopping-a-device.md)。  (启动配置的设备的驱动程序可以在设备启动之前接收 **IRP \_ MN \_ QUERY \_ 停止 \_ 设备** 和 **irp \_ MN \_ 停止 \_ 设备** 请求，但上图中未显示此步骤。 ) 

在 Windows 98/Me 上，PnP 管理器还会在设备被禁用时发送 **IRP \_ MN \_ 查询 \_ 停止 \_ 设备** 和 **irp \_ MN \_ 停止 \_ 设备** 请求。 这些系统上的驱动程序还会在启动失败后收到 **IRP \_ MN \_ 停止 \_ 设备** 请求。

当 PnP 设备从系统中实际删除或已被删除时，PnP 管理器会将各种删除的 Irp 发送到设备的驱动程序，定向它们以删除设备的软件表示形式 (设备对象，等等) 。 有关处理删除 Irp 的信息，请参阅 [删除设备](removing-a-device.md)。

在删除驱动程序的所有设备后的某个时间点，PnP 管理器会调用驱动程序的 [*Unload*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 例程并卸载驱动程序。

 

