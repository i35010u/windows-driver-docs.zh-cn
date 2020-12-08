---
title: 打开和使用并行设备
description: 打开和使用并行设备
keywords:
- 并行设备 WDK，打开
- 并行设备 WDK，共享
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b229b7a0057fbaf9e05a7dac3f0f26a1f44336fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812629"
---
# <a name="opening-and-using-a-parallel-device"></a>打开和使用并行设备





系统提供的并行端口总线驱动程序强制对连接到并行端口的并行设备进行独占访问。 如果某个并行设备处于打开状态，则在关闭该设备之前，并行端口总线驱动程序将无法执行任何后续 [**IRP \_ MJ \_ 创建**](/previous-versions/ff544131(v=vs.85)) 设备请求。 客户端必须在将其他 i/o 请求发送到设备之前打开并行设备，或调用 [并行设备回调例程](/windows-hardware/drivers/ddi/index)。 客户端在设备上关闭其文件后，不能尝试与并行设备通信。 客户端必须关闭设备以允许其他客户端访问设备。

客户端通常会执行以下操作：

-   打开并行设备

-   连接到并行设备-请参阅 [连接到并行设备](connecting-to-a-parallel-device.md)

-   获取有关并行设备的信息−参阅 [获取有关并行设备的信息](obtaining-information-about-a-parallel-device.md)

-   锁定设备−参阅 [锁定和解锁并行端口以供并行设备使用](locking-and-unlocking-a-parallel-port-for-use-by-a-parallel-device.md)

-   在设备上执行一系列操作

-   与并行设备断开连接−参阅 [连接到并行设备](connecting-to-a-parallel-device.md)

-   解锁设备−参阅 [锁定和解锁并行端口以供并行设备使用](locking-and-unlocking-a-parallel-port-for-use-by-a-parallel-device.md)

-   关闭设备

请注意，在即插即用环境中，每当设备上没有打开的文件时，可以删除或添加设备。 通常，每次添加并行设备时，即插即用会分配不同的位置和资源。

 

