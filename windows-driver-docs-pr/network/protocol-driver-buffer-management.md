---
title: 协议驱动程序缓冲区管理
description: 协议驱动程序缓冲区管理
ms.assetid: 1f91b58e-d432-46c8-994e-d95c3aadfe43
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 294cb388f13d180d0ea24f0ee7d353ed7c241b4c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390282"
---
# <a name="protocol-driver-buffer-management"></a>协议驱动程序缓冲区管理





协议驱动程序必须管理[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构池并[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构池发送操作。 若要创建这些池，驱动程序，请调用以下函数：

[**NdisAllocateNetBufferListPool**](https://msdn.microsoft.com/library/windows/hardware/ff561611)

[**NdisAllocateNetBufferPool**](https://msdn.microsoft.com/library/windows/hardware/ff561613)

协议驱动程序可以使用以下函数来从池中分配结构：

[**NdisAllocateNetBufferAndNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff561608)

[**NdisAllocateNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff561609)

[**NdisAllocateNetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff561607)

调用**NdisAllocateNetBufferAndNetBufferList**比调用效率更高**NdisAllocateNetBufferList**跟**NdisAllocateNetBuffer**。 但是， **NdisAllocateNetBufferAndNetBufferList**只会创建一个 NET\_缓冲区结构的网上\_缓冲区\_列表结构。 若要使用**NdisAllocateNetBufferAndNetBufferList**，该驱动程序必须设置*AllocateNetBuffer*参数**TRUE**当调用**NdisAllocateNetBufferListPool**。

协议驱动程序可以使用 OID 请求的查询的基础驱动程序后填充和上下文空间需求。 协议驱动程序应确定中的一个绑定后填充和上下文要求*左*或*正在重新启动*状态。 驱动程序应为整个堆栈分配足够的后填充和上下文空间。 如果有必要，协议驱动程序可以可用池，并重新分配其*正在重新启动*状态。

协议驱动程序使用以下函数可用池：

[**NdisFreeNetBufferListPool**](https://msdn.microsoft.com/library/windows/hardware/ff562590)

[**NdisFreeNetBufferPool**](https://msdn.microsoft.com/library/windows/hardware/ff562592).

协议驱动程序使用以下函数以释放从池中分配的结构：

[**NdisFreeNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff562583)

[**NdisFreeNetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff562582)

驱动程序应释放 NET\_缓冲区结构分配带有**NdisAllocateNetBuffer**之前释放相关联的 NET\_缓冲区\_列表结构。 NET\_缓冲区结构分配带有**NdisAllocateNetBufferAndNetBufferList**时，驱动程序调用释放**NdisFreeNetBufferList**于关联的网络\_缓冲区\_列表结构。

 

 





