---
title: 编写 StartIo 例程
description: 编写 StartIo 例程
ms.assetid: b2a380ae-549c-4ca2-9c69-1e20c17ed2e6
keywords:
- StartIo 例程，有关 StartIo 例程
- StartIo 例程编写
- 启动 I/O 操作
- I/O 操作起始 WDK 内核
- Irp WDK 内核队列
- 队列的 Irp
- 取消排队的 Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7097e21699724fb9cf539e40110268278803bb9e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384532"
---
# <a name="writing-a-startio-routine"></a>编写 StartIo 例程





顾名思义， [ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程负责启动物理设备上的 I/O 操作。

大多数的最低级别驱动程序提供*StartIo*例程和依赖于系统提供的设备队列到队列 Irp I/O 管理器。 某些最低级别驱动程序旨在设置和管理其自己补充的 IRP 队列，但即使这样它们通常还提供*StartIo*例程。 (有关补充队列的详细信息，请参阅[设置和使用设备队列](setting-up-and-using-device-queues.md)并[管理设备队列](managing-device-queues.md)。)

更高级别的驱动程序，包括 FSDs 和即插即用函数和筛选器驱动程序，很少需要*StartIo*例程，因为它可能妨碍性能。 相反，大多数文件系统驱动程序设置和维护的 Irp 的内部队列。 其他更高级别的驱动程序内部队列的 Irp，或只需将 Irp 传递到较低的驱动程序，从其调度例程。 请参阅[Driver-Managed IRP 队列](driver-managed-irp-queues.md)有关详细信息。

可以使用[ **IoSetStartIoAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff550330)例程对集属性的修改*StartIo*处理您的驱动程序。

本部分包含以下主题：

[在最低级别驱动程序中的 StartIo 例程](startio-routines-in-lowest-level-drivers.md)

[在更高级别的驱动程序中的 StartIo 例程](startio-routines-in-higher-level-drivers.md)

[要考虑 StartIo 例程的事项](points-to-consider-for-startio-routines.md)

 

 




