---
title: 在总线驱动程序中启动设备
description: 在总线驱动程序中启动设备
ms.assetid: 1babeabb-1866-4ca5-b5a3-380c246596e5
keywords:
- 总线驱动程序 WDK 即插即用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bd9c5f558bff02c2197ababdb3464bbe9c5befa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382998"
---
# <a name="starting-a-device-in-a-bus-driver"></a>在总线驱动程序中启动设备





总线驱动程序启动子设备 (子*PDO*) 等中的以下过程使用其[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程：

1.  启动设备。

    确切的步骤不同设备的。

    例如，PCI 总线驱动程序及其映射注册到启用 PCI 总线上的请求。 即插即用 ISA 总线驱动程序启用即插即用 ISA 卡以便功能驱动程序可以访问它。

2.  完成 IRP。

    如果总线驱动程序的启动操作已成功，驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功和调用[ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)指定的 IO 优先级提升\_否\_增量。 总线驱动程序将返回状态\_成功从其*DispatchPnP*例程。

    如果总线驱动程序在其开始操作过程中遇到错误，驱动程序将 IRP，调用中设置错误状态**IoCompleteRequest**与 IO\_否\_递增，并返回错误从其*DispatchPnP*例程。

如果总线驱动程序需要一些时间才能启动设备，它可以将标记为挂起的 IRP 并返回状态\_PENDING。

 

 




