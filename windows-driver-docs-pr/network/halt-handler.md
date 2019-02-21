---
title: 微型端口驱动程序终止处理程序
description: 微型端口驱动程序终止处理程序
ms.assetid: 63b0b25e-f52f-4486-a57d-448985207fc8
keywords:
- MiniportHaltEx
- 停止处理程序 WDK NDIS
- 正在卸载的微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5080471ca9d0ce6094a2c4050dadb9eb352b5ea4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545277"
---
# <a name="miniport-driver-halt-handler"></a>微型端口驱动程序终止处理程序





NDIS 微型端口驱动程序必须提供[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)函数来[ **NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654)。

*MiniportHaltEx*应撤消所有内容， [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)未。 例如，可能会 NDIS 微型端口驱动程序：

-   可用端口。 (有关详细信息，请参阅[释放 NDIS 端口](freeing-an-ndis-port.md)。)

-   释放所有硬件资源的[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)声明。

-   通过调用释放中断资源[ **NdisMDeregisterInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff563575)。

-   释放任何内存， [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)分配。

-   停止 NIC，除非[ *MiniportShutdownEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559449)函数都还原到其初始状态 NIC。

下图说明了卸载微型端口驱动程序。

![说明卸载微型端口驱动程序的关系图](images/207-11.png)

*MiniportHaltEx*应完成所需卸载该驱动程序返回之前的操作。 如果具有所有未完成的微型端口驱动程序收到指示 （也就是说，它已指明最多的 NDIS 但 NDIS 接收的网络数据尚未返回）， *MiniportHaltEx*不能返回直到此类数据返回到微型端口驱动程序[ *MiniportReturnNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559437)函数。

上图显示了一组可以通过调用*MiniportHaltEx*函数。 这些调用将无法进行的调用的一个子集。 实际组调用取决于以前的微型端口驱动程序的操作。 微型端口驱动程序可以使这些调用中的相同*MiniportInitializeEx*如果它无法成功初始化的网络适配器，由于硬件问题或因为它无法获取其所需的资源。 在这种情况下， *MiniportInitializeEx*应卸载该驱动程序通过撤消其以前的操作。 否则为*MiniportHaltEx*将撤消的操作*MiniportInitializeEx*。

以下列表描述反向微型端口驱动程序可能需要某些操作所需的调用：

-   如果微型端口驱动程序已注册中断，则应调用[ **NdisMDeregisterInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff563575)。

-   如果微型端口驱动程序设置了一个计时器或计时器，则应调用[ **NdisCancelTimerObject** ](https://msdn.microsoft.com/library/windows/hardware/ff561624)为它创建的每个计时器。 如果调用**NdisCancelTimerObject**失败，计时器可能具有已激发。 在这种情况下，微型端口驱动程序应等待计时器处理程序，若要完成从返回前*MiniportHaltEx*。

-   如果微型端口驱动程序分配任何内存以及[ **NdisAllocateMemoryWithTagPriority**](https://msdn.microsoft.com/library/windows/hardware/ff561606)，则应调用[ **NdisFreeMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff562577)到释放该内存。

-   如果微型端口驱动程序分配任何内存以及[ **NdisMAllocateSharedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff562782)，或[ **NdisMAllocateSharedMemoryAsyncEx**](https://msdn.microsoft.com/library/windows/hardware/ff562784)，它应调用[ **NdisMFreeSharedMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff563589)来释放该内存。

-   如果微型端口驱动程序分配并初始化存储池使用的数据包描述符[ **NdisAllocateNetBufferPool**](https://msdn.microsoft.com/library/windows/hardware/ff561611)，则应调用[ **NdisFreeNetBufferPool** ](https://msdn.microsoft.com/library/windows/hardware/ff562592)来释放该存储。

-   如果微型端口驱动程序分配或保留的任何硬件资源，这些应返回。 例如，如果微型端口驱动程序映射 NIC 上的 I/O 端口范围，它应释放端口通过调用[ **NdisMDeregisterIoPortRange**](https://msdn.microsoft.com/library/windows/hardware/ff563577)。

## <a name="related-topics"></a>相关主题


[适配器状态的微型端口驱动程序](adapter-states-of-a-miniport-driver.md)

[释放 NDIS 端口](freeing-an-ndis-port.md)

[正在停止微型端口适配器](halting-a-miniport-adapter.md)

[微型端口适配器状态和操作](miniport-adapter-states-and-operations.md)

[微型端口驱动程序重置和 Halt 函数](https://msdn.microsoft.com/library/windows/hardware/ff564064)

 

 






