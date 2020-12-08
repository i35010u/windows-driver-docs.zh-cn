---
title: 网络驱动程序中的多处理器支持
description: 网络驱动程序中的多处理器支持
keywords:
- 网络驱动程序 WDK，处理器支持
- 多处理器支持 WDK 网络
- 处理器 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37cb736163576098e594950db3fdffda1227b085
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803509"
---
# <a name="multiprocessor-support-in-network-drivers"></a>网络驱动程序中的多处理器支持





若要为所有 Microsoft Windows 版本编写便携驱动程序，需要编写代码，以便安全地在运行多个并发运行的处理器的计算机上运行。 网络驱动程序必须是多处理器安全的，并且必须使用提供的 NDIS 库函数。

在单处理器环境中，单个处理器一次只运行一条计算机指令，即使网络接口卡 (NIC) 或其他设备可以在数据包到达或计时器中断时中断当前执行流。 通常，在操作数据结构（如数据包队列）时，驱动程序将禁用 NIC 上的中断，执行操作，然后会中断。 多处理器环境中的许多线程似乎同时运行，但实际上是在交错时间段内运行。

在多处理器环境中，处理器同时运行多个计算机指令。 驱动程序必须进行同步，以便当一个驱动程序函数操作通用数据结构时，另一个处理器上的相同或其他驱动程序函数不会试图同时修改共享数据。 所有驱动程序代码都可在 (SMP) 计算机的对称多处理器中进行重入。 为了消除此资源保护问题，Windows 设备驱动程序使用自旋锁。 有关详细信息，请参阅 [网络驱动程序中的同步和通知](synchronization-and-notification-in-network-drivers.md)。

 

 





