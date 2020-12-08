---
title: 编写 ControllerControl 例程
description: 编写 ControllerControl 例程
keywords:
- 控制器对象 WDK 内核，编写 ControllerControl 例程
- ControllerControl 例程，编写
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f56b54127bbd52940c1dc75409dde23e63f75922
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782601"
---
# <a name="writing-controllercontrol-routines"></a>编写 ControllerControl 例程





使用控制器对象的驱动程序必须提供 [*ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049) 例程才能启动 i/o 操作。

必须通过物理控制器（如 "位于" 磁盘控制器）将操作同步到类似设备的最低级别设备驱动程序可以有 *ControllerControl* 例程。

当驱动程序调用 [**IoAllocateController**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioallocatecontroller)时，如果控制器对象表示的硬件可用于 i/o 操作，则其 *ControllerControl* 例程会立即运行。 否则， *ControllerControl* 例程会排入队列，直到控制器空闲。

**注意**  WDM 驱动程序无法使用控制器对象和 *ControllerControl* 例程。

 

 

