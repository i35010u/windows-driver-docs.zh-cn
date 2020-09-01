---
title: 删除 ISR
description: 删除 ISR
ms.assetid: 23d84edb-763f-4383-b05c-832b4249b604
keywords:
- 中断服务例程 WDK 内核，删除 Isr
- 中断对象 WDK 内核，删除 Isr
- Isr WDK 内核，删除 Isr
- 删除 Isr WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59f156793b166f15bf14f7eb712106795a6bcf9a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189291"
---
# <a name="removing-an-isr"></a>删除 ISR


驱动程序可以通过调用[**IoDisconnectInterruptEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterruptex)删除注册到[**IoConnectInterruptEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)的 ISR。 **IoDisconectInterruptEx** 采用单个 parameter 参数， *该参数是* 一个指向 [**IO \_ 断开连接 \_ 中断 \_ 参数**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_disconnect_interrupt_parameters) 结构的指针。 结构成员所使用的值取决于用于注册 ISR 的版本。

驱动程序必须在注册 ISR 时保存某些信息，以后再将其删除。 对于基于连接 \_ 线 \_ 并连接 \_ 完全 \_ 指定的版本，驱动程序必须保存在[**IO \_ CONNECT \_ 中断 \_ 参数**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_connect_interrupt_parameters)的**LineBased**或**FullySpecified**成员中提供的值。 对于基于连接 \_ 消息的 \_ 版本，驱动程序必须保存 MessageBased 中提供的值**Version** ，以及**IO \_ CONNECT \_ 中断 \_ 参数**的**microsoft.sqlserver.replication.replicationobject.connectioncontext**成员。

 

