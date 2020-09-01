---
title: 编写 ControllerControl 例程
description: 编写 ControllerControl 例程
ms.assetid: 9330e0ff-c4bb-4aa6-985e-ef89791f74df
keywords:
- 控制器对象 WDK 内核，编写 ControllerControl 例程
- ControllerControl 例程，编写
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00344da760416537b673c45169546eaefc319463
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184095"
---
# <a name="writing-controllercontrol-routines"></a>编写 ControllerControl 例程





使用控制器对象的驱动程序必须提供 [*ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049) 例程才能启动 i/o 操作。

必须通过物理控制器（如 "位于" 磁盘控制器）将操作同步到类似设备的最低级别设备驱动程序可以有 *ControllerControl* 例程。

当驱动程序调用 [**IoAllocateController**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioallocatecontroller)时，如果控制器对象表示的硬件可用于 i/o 操作，则其 *ControllerControl* 例程会立即运行。 否则， *ControllerControl* 例程会排入队列，直到控制器空闲。

**注意**   WDM 驱动程序无法使用控制器对象和*ControllerControl*例程。

 

 

