---
title: 释放 VM 队列
description: 释放 VM 队列
ms.assetid: 32679638-eeef-4e11-bf56-c96f047e4de7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57417c984633c4672b67817a9f4025ab360fbbc5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323441"
---
# <a name="freeing-a-vm-queue"></a>释放 VM 队列





要释放接收队列，基础驱动程序将发出[OID\_接收\_筛选器\_免费\_队列](https://msdn.microsoft.com/library/windows/hardware/ff569789)集 OID 请求。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_接收\_队列\_免费\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567201)结构类型的队列标识符**NDIS\_接收\_队列\_ID**。

[OID\_接收\_筛选器\_免费\_队列](https://msdn.microsoft.com/library/windows/hardware/ff569789)释放基础驱动程序通过使用分配的接收队列[OID\_接收\_筛选器\_分配\_队列](https://msdn.microsoft.com/library/windows/hardware/ff569784)OID。 有关分配接收队列的详细信息，请参阅[分配 VM 队列](allocating-a-vm-queue.md)。

**请注意**  默认队列，都有一个队列标识符的**NDIS\_默认\_接收\_队列\_ID**始终分配，且不能为释放。

 

基础驱动程序必须释放它在释放队列前在队列设置的所有筛选器。 此外，基础驱动程序必须释放它分配网络适配器调用之前的所有接收队列[ **NdisCloseAdapterEx** ](https://msdn.microsoft.com/library/windows/hardware/ff561640)函数以关闭到的网络适配器的绑定。 NDIS 释放之前它将调用微型端口驱动程序的网络适配器分配的所有队列[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)函数。

当微型端口驱动程序收到请求以释放队列时，执行以下操作：

-   与队列相关联的共享的内存资源，必须立即停止 DMA。

-   生成状态指示，以指示 DMA 已停止。

-   等待所有未完成[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构，与队列，若要返回相关联。

-   释放关联的共享的内存和硬件资源。

当微型端口驱动程序收到[OID\_接收\_筛选器\_免费\_队列](https://msdn.microsoft.com/library/windows/hardware/ff569789)集请求队列必须输入停止 DMA 状态，它将停止 DMA 上队列及其包含的微型端口驱动程序必须通过使用指示的状态更改[ **NDIS\_状态\_接收\_队列\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567417)状态指示。 队列状态的详细信息，请参阅[队列状态和操作](queue-states-and-operations.md)。

微型端口驱动程序问题后[ **NDIS\_状态\_接收\_队列\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567417)状态指示，它必须等待所有挂起接收指示完成之前它可以释放相关联的共享的内存。 有关释放共享的内存的详细信息，请参阅[共享的内存资源分配](shared-memory-resource-allocation.md)。

 

 





