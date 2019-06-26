---
title: 设置 ControllerControl 例程
description: 设置 ControllerControl 例程
ms.assetid: 007247c1-b51e-4677-9a46-78ff9f1c8996
keywords:
- 控制器对象 WDK 内核，编写 ControllerControl 例程
- ControllerControl 例程编写
- ControllerControl 例程设置
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf65cdb54c6599ae2f265f66a39a49a89551b4b7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383026"
---
# <a name="setting-up-controllercontrol-routines"></a>设置 ControllerControl 例程





驱动程序的[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程必须执行以下操作，当它收到[ **IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求，设置[ *ControllerControl* ](https://msdn.microsoft.com/library/windows/hardware/ff542049)例程：

1.  调用[ **IoCreateController** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatecontroller)若要设置控制器对象，指定驱动程序确定*大小*控制器扩展，系统会从分配非分页缓冲的池并将用零初始化。

2.  保存*ControllerObject*返回指针**IoCreateController**，通常在每个设备对象，表示控制的硬件的物理或逻辑设备的设备扩展中由控制器对象。

3.  设置和/或初始化的驱动程序确定内容 * ControllerObject * **-&gt;ControllerExtension**。

返回*ControllerObject*指针、 驱动程序的入口点*ControllerControl*例程*DeviceObject*指针来表示的目标设备当前的 IRP，和一个*上下文*指向已设置了一个区域*ControllerControl*例程必须对驱动程序的调用中传递[ **IoAllocateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioallocatecontroller)。 通常情况下，驱动程序的[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)的区域设置例程*上下文*调用之前**IoAllocateController**。

 

 




