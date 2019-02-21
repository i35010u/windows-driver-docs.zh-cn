---
title: 避免轮询设备
description: 避免轮询设备
ms.assetid: c50c9c6f-c8eb-4e52-854a-3ebc4fdc874c
keywords:
- I/O WDK 内核设备轮询
- 轮询 WDK I/O 的设备
- 轮询设备 WDK I/O
- 循环计数器 WDK I/O
- 计数器 WDK I/O
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: eacadeb33d891735c29b35ec5d596a067b119daa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541791"
---
# <a name="avoid-polling-devices"></a>避免轮询设备





设备驱动程序应避免轮询其设备，除非绝对必要，并且应永远不会使用整个时间片的轮询。 轮询设备是代价高昂的操作，使计算密集型轮询驱动程序中的任何操作系统。 执行多轮询设备驱动程序干扰其他设备上的 I/O 操作，可以对用户进行系统缓慢甚至失去反应。

最近开发的设备，让高级作为在其 Windows 旨在运行，很少需要使用驱动程序或者轮询其设备，以确保设备已准备好启动 I/O 操作或操作已完成的处理器。

不过，仍在使用某些设备旨在使用旧有窄数据总线、 缓慢时钟速率和单用户、 任务单调度操作系统执行同步 I/O 的处理器。 此类设备可能需要轮询或其他方法来等待要更新其注册的设备。

尽管它看起来有点逻辑通过编码递增计数器的简单循环来解决慢速设备问题，从而"浪费"最小时间间隔而设备更新寄存器，这样的驱动程序不太能够在 Windows 平台之间移植。 循环计数器的最大值将为每个平台需要自定义。 此外，如果具有很好的优化编译器编译驱动程序时，编译器可能会删除驱动程序的计数器变量，它就会增加的循环。

**请注意**  如果而设备硬件更新状态，必须停止该驱动程序，请遵循此实现准则：驱动程序可以调用[ **KeStallExecutionProcessor** ](https://msdn.microsoft.com/library/windows/hardware/ff553295)读取设备注册之前。 该驱动程序应尽量少停滞不前，并应，一般情况下，指定停滞间隔不超过 50 微秒的间隔。

粒度**KeStallExecutionProcessor**间隔是一个低至微秒。

如果设备经常需要多个 50 微秒，来更新状态，请考虑设置[设备专用线程](device-dedicated-threads.md)驱动程序中。

 

 

 




