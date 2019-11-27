---
title: 在总线驱动程序中启动设备
description: 在总线驱动程序中启动设备
ms.assetid: 1babeabb-1866-4ca5-b5a3-380c246596e5
keywords:
- 总线驱动程序 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2719ef400061892af5df236cd64880f87f25bac2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838414"
---
# <a name="starting-a-device-in-a-bus-driver"></a>在总线驱动程序中启动设备





总线驱动程序使用以下过程启动子设备（子*PDO*）： [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

1.  启动设备。

    具体步骤因设备而异。

    例如，PCI 总线驱动程序会将其映射注册为启用 PCI 总线上的请求。 PnP ISA 总线驱动程序启用 PnP ISA 卡，以便函数驱动程序可以访问它。

2.  完成 IRP。

    如果总线驱动程序的启动操作成功，则驱动程序将**Irp&gt;的 IoStatus**设置为 STATUS\_SUCCESS，并调用[**IOCOMPLETEREQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)以指定 IO\_不\_增量的优先级提升。 总线驱动程序从其*DispatchPnP*例程返回状态\_成功。

    如果总线驱动程序在启动操作过程中遇到错误，则驱动程序会在 IRP 中设置错误状态，使用 IO\_调用**IoCompleteRequest** ，而不\_递增，并从其*DispatchPnP*例程返回错误。

如果总线驱动程序需要一段时间才能启动设备，则可以将 IRP 标记为 "挂起"，并返回状态\_"挂起"。

 

 




