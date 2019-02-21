---
title: 网络驱动程序中的多处理器支持
description: 网络驱动程序中的多处理器支持
ms.assetid: df01d8b0-0740-45b6-abe0-a7a7bf6b9334
keywords:
- 网络驱动程序 WDK，处理器支持
- 多个处理器支持 WDK 网络
- 处理器 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd49fe62bc53d70c07426c79aa6f5ae93bff32d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520713"
---
# <a name="multiprocessor-support-in-network-drivers"></a>网络驱动程序中的多处理器支持





若要编写用于所有 Microsoft Windows 版本的可移植驱动程序，您需要编写代码来安全地在计算机上运行具有多个并发运行的处理器。 网络驱动程序必须是安全的包含多个处理器，并且必须使用提供的 NDIS 库函数。

在单处理器环境中，单个处理器运行只有一台计算机指令一次，即使它是可能的网络接口卡 (NIC) 或其他设备或数据包到达时对计时器中断发生时中断当前的执行流。 通常情况下，当操作数据结构，例如数据包队列时，驱动程序禁用的 NIC 上的中断、 执行操作，然后重新启用中断。 在单处理器环境中的多个线程看起来同时运行，但实际上在交错的时间段中运行。

在多处理器环境中，处理器同时运行多个计算机指令。 驱动程序必须同步，以便当一个驱动程序函数操作通用数据结构，相同或另一个处理器上的另一个驱动程序函数不会尝试在同一时间修改共享的数据。 所有驱动程序代码的可重入对称多处理器 (SMP) 计算机中。 若要消除此资源保护问题，Windows 设备驱动程序，请使用自旋锁。 有关详细信息，请参阅[同步和网络驱动程序中的通知](synchronization-and-notification-in-network-drivers.md)。

 

 





