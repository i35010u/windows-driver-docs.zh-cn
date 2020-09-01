---
title: 在总线驱动程序中启动设备
description: 在总线驱动程序中启动设备
ms.assetid: 1babeabb-1866-4ca5-b5a3-380c246596e5
keywords:
- 总线驱动程序 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91e69d7fd0dde66021488412fb6f5344f5039312
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192585"
---
# <a name="starting-a-device-in-a-bus-driver"></a>在总线驱动程序中启动设备





总线驱动程序会启动子设备 (子 *PDO*) 并在其 [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程中使用如下所述的过程：

1.  启动设备。

    具体步骤因设备而异。

    例如，PCI 总线驱动程序会将其映射注册为启用 PCI 总线上的请求。 PnP ISA 总线驱动程序启用 PnP ISA 卡，以便函数驱动程序可以访问它。

2.  完成 IRP。

    如果总线驱动程序的启动操作成功，则驱动程序将 **Irp- &gt; IoStatus** 设置为 status \_ SUCCESS，并调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 来指定 IO 无增量的优先级提升 \_ \_ 。 总线驱动程序 \_ 从其 *DispatchPnP* 例程返回状态 SUCCESS。

    如果总线驱动程序在启动操作过程中遇到错误，则驱动程序会在 IRP 中设置错误状态，使用 IO 无增量调用 **IoCompleteRequest** ， \_ \_ 并从其 *DispatchPnP* 例程返回错误。

如果总线驱动程序需要一段时间才能启动设备，则可以将 IRP 标记为 "挂起" 并返回 "挂起" 状态 \_ 。

 

