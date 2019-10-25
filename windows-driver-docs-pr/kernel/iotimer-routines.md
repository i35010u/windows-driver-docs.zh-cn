---
title: IoTimer 例程
description: IoTimer 例程
ms.assetid: bc69c7b5-ce63-435e-b5b4-0d65ee153d31
keywords:
- 同步 WDK 内核，计时器
- IoTimer
- 设备超时 WDK 内核
- 超时 WDK 内核
- 计时操作 WDK 内核
- 超时设备 i/o 操作 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4aa68224a0af2a5c1e0600a445e36c8540bcac57
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828158"
---
# <a name="iotimer-routines"></a>IoTimer 例程





需要定期调用来确定设备操作是否已超时的驱动程序，要更新某个驱动程序定义的变量（例如计数器），或对不需要较小时间间隔的任何操作进行时间，可以使用[*IoTimer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine)例程。 *IoTimer*例程实际上是一个与设备对象相关联的 DPC 例程，每秒 i/o 管理器会调用一次。 对于创建的每个设备对象，驱动程序可以有一个*IoTimer*例程。

通常，驱动程序应使用*IoTimer*例程执行需要定期一秒的时间间隔的操作。 若要使需要可变间隔或间隔的时间长度小于每秒的间隔时间，驱动程序应分配计时器对象。 有关详细信息，请参阅[Timer 对象和 dpc](timer-objects-and-dpcs.md)。

本部分包含以下主题：

[注册和启用 IoTimer 例程](registering-and-enabling-an-iotimer-routine.md)

[提供 IoTimer 上下文信息](providing-iotimer-context-information.md)

[使用 IoTimer 例程](using-an-iotimer-routine.md)

 

 




