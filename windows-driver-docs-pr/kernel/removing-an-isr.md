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
ms.openlocfilehash: 82d0a102b7b81e855b535eca61f36d148e075ae7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836472"
---
# <a name="removing-an-isr"></a>删除 ISR


驱动程序可以通过调用[**IoDisconnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterruptex)删除注册到[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)的 ISR。 **IoDisconectInterruptEx**采用单个 parameter 参数，*该参数是*一个指向 IO\_的指针[ **\_中断\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_disconnect_interrupt_parameters)结构。 结构成员所使用的值取决于用于注册 ISR 的版本。

驱动程序必须在注册 ISR 时保存某些信息，以后再将其删除。 对于 "连接\_行\_" 和 "连接\_完全\_指定版本，驱动程序必须保存**InterruptObject**或**FullySpecified 的**成员中[**提供的值。\_连接\_中断\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_connect_interrupt_parameters)。 对于连接\_基于\_版本的消息，驱动程序必须保存**microsoft.sqlserver.replication.replicationobject.connectioncontext**的**version**和 MessageBased 成员中提供的值， **\_连接\_中断\_参数**。

 

 




