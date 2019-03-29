---
title: 分配 VM 队列
description: 分配 VM 队列
ms.assetid: 2645a6e5-3824-469c-84d5-8e49fa01f494
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e72a7e6a3ad280ce51e5bfb5774a6f7f8683925f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567419"
---
# <a name="allocating-a-vm-queue"></a>分配 VM 队列





若要分配具有一组初始配置参数的队列，基础驱动程序将发出[OID\_接收\_筛选器\_分配\_队列](https://msdn.microsoft.com/library/windows/hardware/ff569784)方法 OID 请求。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构最初包含一个指向[**NDIS\_接收\_队列\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567211)结构。 通过 OID 方法请求成功返回后**InformationBuffer**的成员**NDIS\_OID\_请求**结构包含一个指向**NDIS\_接收\_队列\_参数**结构，它具有一个新的队列标识符和 MSI X 表条目。

[ **NDIS\_接收\_队列\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567211)中使用结构[OID\_接收\_筛选器\_分配\_队列](https://msdn.microsoft.com/library/windows/hardware/ff569784)OID 并[OID\_接收\_筛选器\_队列\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569794)OID。 有关 VM 队列参数的详细信息，请参阅[Obtaining 和更新虚拟机队列参数](obtaining-and-updating-vm-queue-parameters.md)。

基础驱动程序初始化[ **NDIS\_接收\_队列\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567211)结构具有以下队列配置参数：

-   队列类型 (**NdisReceiveQueueTypeVMQueue**从[ **NDIS\_接收\_队列\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff567217)枚举。)

-   处理器关联的队列。

-   队列名称和虚拟机名称。

-   预测先行拆分的参数。

    **请注意**  从 NDIS 6.30 开始，将数据包数据拆分为单独的预测先行缓冲区不再受支持。

     

**请注意**  过量的驱动程序可以设置 NDIS\_接收\_队列\_参数\_每\_队列\_接收\_指示和NDIS\_接收\_队列\_参数\_预测先行\_拆分\_中的必需标志**标志**成员[ **NDIS\_接收\_队列\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567211)结构。 其他标志不能提供队列分配。

 

当 NDIS 收到 OID 请求分配接收队列时，它会验证队列参数。 NDIS 分配所需的资源和队列标识符后，它将提交对基础微型端口驱动程序的 OID 请求。 队列标识符是唯一的关联的网络适配器。

如果微型端口驱动程序能够成功地分配必要的软件和硬件资源接收队列，它完成时成功状态的 OID 请求。

NDIS NDIS OID 请求发送到微型端口驱动程序之前，将分配中的队列标识符**QueueId**的成员[ **NDIS\_接收\_队列\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567211)结构，并将方法请求传递给微型端口驱动程序。 微型端口驱动程序提供了中的 MSI X 表条目**MSIXTableEntry**成员。

微型端口驱动程序必须保留已分配的接收队列的队列标识符。 NDIS 以便后续调用微型端口驱动程序使用接收队列队列的标识符以接收队列上设置接收筛选器、 更改接收队列参数，或免费接收队列。

**请注意**  默认队列 （队列标识符零） 始终分配和无法被释放。

 

基础驱动程序必须使用 NDIS 提供了在 OID 的后续请求，例如，若要修改队列参数或释放队列的队列标识符。 上所有的 OOB 数据中还包含该队列的标识符[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)与队列相关联的结构。 驱动程序使用[ **NET\_缓冲区\_列表\_接收\_队列\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff568407)宏来检索 NET中的队列标识符\_缓冲区\_列表结构。

**请注意**  协议驱动程序可以在任何时候设置 VMQ 筛选器，它已成功分配一个队列之后之前删除队列。

 

协议驱动程序问题[OID\_接收\_筛选器\_队列\_分配\_完成](https://msdn.microsoft.com/library/windows/hardware/ff569793)方法 OID 请求完成队列分配。 微型端口驱动程序可以将共享的内存和其他资源分配，分配完成后。 有关如何将共享的内存资源分配的详细信息，请参阅[共享的内存资源分配](shared-memory-resource-allocation.md)。

后微型端口驱动程序将收到一个 OID\_接收\_筛选器\_队列\_分配 OID 请求并处理它成功，队列处于*已分配*状态。 队列状态的详细信息，请参阅[队列状态和操作](queue-states-and-operations.md)。

基础驱动程序分配后一个或多个接收队列 （和 （可选） 设置的初始的筛选器），必须颁发[OID\_接收\_筛选器\_队列\_分配\_完整](https://msdn.microsoft.com/library/windows/hardware/ff569793)设置 OID 请求用于通知微型端口驱动程序分配已完成当前批的接收队列。

如果没有该队列上设置筛选器，微型端口驱动程序必须保留在接收队列中的任何数据包。 如果队列永远不会有任何筛选器设置或已清除所有筛选器，该队列应为空，并且应丢弃任何数据包。 也就是说，它们不指示驱动程序堆栈中向上或保持在队列中。

驱动程序使用过量[OID\_接收\_筛选器\_免费\_队列](https://msdn.microsoft.com/library/windows/hardware/ff569789)OID 来释放它们所分配的队列。 释放队列的详细信息，请参阅[释放 VM 队列](freeing-a-vm-queue.md)。

 

 





