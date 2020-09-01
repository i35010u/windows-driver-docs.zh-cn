---
title: 设置 ControllerControl 例程
description: 设置 ControllerControl 例程
ms.assetid: 007247c1-b51e-4677-9a46-78ff9f1c8996
keywords:
- 控制器对象 WDK 内核，编写 ControllerControl 例程
- ControllerControl 例程，编写
- ControllerControl 例程，设置
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf8d2543fe9f1bd04e96955b01aa6b39b0c6cc06
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189449"
---
# <a name="setting-up-controllercontrol-routines"></a>设置 ControllerControl 例程





驱动程序的 [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程在收到 [**IRP \_ MN \_ START \_ 设备**](./irp-mn-start-device.md) 请求时必须执行以下操作，以设置 [*ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049) 例程：

1.  调用 [**IoCreateController**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatecontroller) 以设置控制器对象，指定控制器扩展的驱动程序确定 *大小* ，该大小由系统从非分页池分配，并初始化为零。

2.  保存**IoCreateController**返回的*ControllerObject*指针，通常在代表由控制器对象表示的硬件控制的物理或逻辑设备的每个设备对象的设备扩展中。

3.  设置和/或初始化 * ControllerObject *** - &gt; ControllerExtension**的驱动程序确定内容。

返回的*ControllerObject*指针，驱动程序的*ControllerControl*例程的入口点，表示当前 IRP 的目标设备的*DeviceObject*指针，并且必须在驱动程序的调用中将*上下文*指针传递到[**IoAllocateController**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioallocatecontroller)。 *ControllerControl* 通常，驱动程序的[*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程在调用**IoAllocateController**之前，在*上下文*中设置区域。

 

