---
title: 编写 StartIo 例程
description: 编写 StartIo 例程
keywords:
- StartIo 例程，关于 StartIo 例程
- StartIo 例程，编写
- 启动 i/o 操作
- 启动 WDK 内核时的 i/o 操作
- Irp WDK 内核，队列
- 队列 Irp
- 出列的 Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ef668b52a55ef9cf796f8175b2d68af14b4fd4a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782615"
---
# <a name="writing-a-startio-routine"></a>编写 StartIo 例程





顾名思义， [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程负责在物理设备上启动 i/o 操作。

最底层的驱动程序提供 *StartIo* 例程，并依赖于 i/o 管理器将 irp 排队到系统提供的设备队列。 某些最低级别的驱动程序旨在设置和管理其自己的补充 IRP 队列，但这通常还提供 *StartIo* 例程。  (有关补充队列的详细信息，请参阅 [设置和使用设备队列](setting-up-and-using-device-queues.md) 和 [管理设备队列](managing-device-queues.md)。 ) 

较高级别的驱动程序（包括 FSDs 和 PnP 函数和筛选器驱动程序）很少具有 *StartIo* 例程，因为它可能会妨碍性能。 相反，大多数文件系统驱动程序都设置并维护 Irp 的内部队列。 其他较高级别的驱动程序要么具有用于 Irp 的内部队列，要么只是将 Irp 从其调度例程传递到较低的驱动程序。 有关详细信息，请参阅 [驱动程序管理的 IRP 队列](driver-managed-irp-queues.md) 。

可以使用 [**IoSetStartIoAttributes**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iosetstartioattributes) 例程设置用于修改驱动程序的 *StartIo* 处理的属性。

本节包含下列主题：

[最低级驱动程序中的 StartIo 例程](startio-routines-in-lowest-level-drivers.md)

[较高级驱动程序中的 StartIo 例程](startio-routines-in-higher-level-drivers.md)

[StartIo 例程的注意事项](points-to-consider-for-startio-routines.md)

 

