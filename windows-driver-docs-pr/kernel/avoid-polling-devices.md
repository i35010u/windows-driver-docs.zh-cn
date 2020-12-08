---
title: 避免轮询设备
description: 避免轮询设备
keywords:
- I/o WDK 内核，设备轮询
- 设备轮询 WDK i/o
- 轮询设备 WDK i/o
- 循环计数器 WDK i/o
- 计数器 WDK i/o
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f680c2954a3c8636fc21a22b71a3541a0eea459
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789803"
---
# <a name="avoid-polling-devices"></a>避免轮询设备





除非绝对必要，否则设备驱动程序应避免对设备进行轮询，并且决不能使用整个时间片进行轮询。 轮询设备是一项成本高昂的操作，用于在轮询驱动程序内对任何操作系统进行计算。 执行大量轮询的设备驱动程序会影响其他设备上的 i/o 操作，并可能使系统变慢，使用户无法响应。

最近开发的设备与运行 Windows 的处理器相比，其技术高级，很少需要驱动程序来轮询其设备，以确保设备已准备好启动 i/o 操作或操作完成。

尽管如此，某些仍在使用中的设备已设计用于处理旧的处理器，其中包含的数据总线较窄、时钟速率较慢，以及执行同步 i/o 的单用户单任务操作系统。 此类设备可能需要轮询或其他一些方法来等待设备更新其寄存器。

尽管通过编写递增计数器的简单循环来编写简单的循环来解决速度较慢的设备问题似乎是合乎逻辑的，因此，在设备更新注册时，此类驱动程序在 Windows 平台中不太可能是可移植的。 循环计数器的最大值需要为每个平台自定义。 此外，如果使用良好的优化编译器对驱动程序进行编译，则编译器可能会删除驱动程序的计数器变量，并且循环 (s) 在其中递增。

**注意**   如果驱动程序必须在设备硬件更新状态时停止，请遵循此实现准则：驱动程序可以在读取设备寄存器之前调用 [**KeStallExecutionProcessor**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-kestallexecutionprocessor) 。 驱动程序应最大限度地减少间隔时间间隔，并且应在一般情况下指定一个不超过50微秒的间隔时间间隔。

**KeStallExecutionProcessor** 间隔的粒度为一微秒。

如果设备的更新状态需要超过50微秒，请考虑在驱动程序中设置 [设备专用线程](device-dedicated-threads.md) 。

 

 

