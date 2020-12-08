---
title: 删除 ISR
description: 删除 ISR
keywords:
- 中断服务例程 WDK 内核，删除 Isr
- 中断对象 WDK 内核，删除 Isr
- Isr WDK 内核，删除 Isr
- 删除 Isr WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f417c13afbf51b98487f766445df0caf6a9a5a5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834431"
---
# <a name="removing-an-isr"></a>删除 ISR


驱动程序可以通过调用 [**IoDisconnectInterruptEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterruptex)删除注册到 [**IoConnectInterruptEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)的 ISR。 **IoDisconectInterruptEx** 采用单个 parameter 参数， *该参数是* 一个指向 [**IO \_ 断开连接 \_ 中断 \_ 参数**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_disconnect_interrupt_parameters) 结构的指针。 结构成员所使用的值取决于用于注册 ISR 的版本。

驱动程序必须在注册 ISR 时保存某些信息，以后再将其删除。 对于基于连接 \_ 线 \_ 并连接 \_ 完全 \_ 指定的版本，驱动程序必须保存在 [**IO \_ CONNECT \_ 中断 \_ 参数**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_connect_interrupt_parameters)的 **LineBased** 或 **FullySpecified** 成员中提供的值。 对于基于连接 \_ 消息的 \_ 版本，驱动程序必须保存 MessageBased 中提供的值 **Version** ，以及 **IO \_ CONNECT \_ 中断 \_ 参数** 的 **microsoft.sqlserver.replication.replicationobject.connectioncontext** 成员。

 

