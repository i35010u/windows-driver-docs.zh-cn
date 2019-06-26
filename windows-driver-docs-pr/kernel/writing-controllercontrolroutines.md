---
title: 编写 ControllerControl 例程
description: 编写 ControllerControl 例程
ms.assetid: 9330e0ff-c4bb-4aa6-985e-ef89791f74df
keywords:
- 控制器对象 WDK 内核，编写 ControllerControl 例程
- ControllerControl 例程编写
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4835a144472bc9f80019630ff64fd76a8996e51c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374118"
---
# <a name="writing-controllercontrol-routines"></a>编写 ControllerControl 例程





使用控制器对象的驱动程序必须提供[ *ControllerControl* ](https://msdn.microsoft.com/library/windows/hardware/ff542049)例程，以启动 I/O 操作。

必须同步的操作，通过物理控制器，例如"AT"磁盘控制器、 到类似的设备的最低级别的设备驱动程序可以具有*ControllerControl*例程。

当驱动程序调用[ **IoAllocateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioallocatecontroller)，将其*ControllerControl*如果硬件由控制器对象可立即运行时例程对于 I/O 操作。 否则为*ControllerControl*例程会排队，直到该控制器是免费的。

**请注意**  WDM 驱动程序不能使用控制器对象和*ControllerControl*例程。

 

 

 




