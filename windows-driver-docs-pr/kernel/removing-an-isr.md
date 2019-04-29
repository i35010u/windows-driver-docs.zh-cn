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
ms.openlocfilehash: ebb2bd039c9b372df276eb1f87459ac4ed05fefd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324485"
---
# <a name="removing-an-isr"></a>删除 ISR


驱动程序可以删除已注册到 ISR [ **IoConnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548378)通过调用[ **IoDisconnectInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff549093)。 **IoDisconectInterruptEx**采用单个*参数*参数，它是一个指针，到[ **IO\_断开连接\_中断\_参数** ](https://msdn.microsoft.com/library/windows/hardware/ff550569)结构。 用于结构的成员的值取决于用来注册 ISR 的版本

当注册 ISR 以更高版本中删除它，驱动程序必须保存某些信息。 Connect\_行\_基于和 CONNECT\_完全\_指定的版本中，该驱动程序必须保存中提供的值**LineBased.InterruptObject**或**FullySpecified.InterruptObject**的成员[ **IO\_CONNECT\_中断\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff550541)。 Connect\_消息\_基于版本，该驱动程序必须保存在所提供的值**版本**并**MessageBased.ConnectionContext**的成员**IO\_CONNECT\_中断\_参数**。

 

 




