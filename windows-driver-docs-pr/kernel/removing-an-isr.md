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
ms.openlocfilehash: 0ebd444eb6c00e9e16e2e529a50a15f5a69419c8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373423"
---
# <a name="removing-an-isr"></a>删除 ISR


驱动程序可以删除已注册到 ISR [ **IoConnectInterruptEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterruptex)通过调用[ **IoDisconnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodisconnectinterruptex)。 **IoDisconectInterruptEx**采用单个*参数*参数，它是一个指针，到[ **IO\_断开连接\_中断\_参数** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_disconnect_interrupt_parameters)结构。 用于结构的成员的值取决于用来注册 ISR 的版本

当注册 ISR 以更高版本中删除它，驱动程序必须保存某些信息。 Connect\_行\_基于和 CONNECT\_完全\_指定的版本中，该驱动程序必须保存中提供的值**LineBased.InterruptObject**或**FullySpecified.InterruptObject**的成员[ **IO\_CONNECT\_中断\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_connect_interrupt_parameters)。 Connect\_消息\_基于版本，该驱动程序必须保存在所提供的值**版本**并**MessageBased.ConnectionContext**的成员**IO\_CONNECT\_中断\_参数**。

 

 




