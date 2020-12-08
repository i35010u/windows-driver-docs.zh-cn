---
title: 使用网络驱动程序中的共享内存
description: 使用网络驱动程序中的共享内存
keywords:
- 网络驱动程序 WDK，共享内存
- 内存 WDK 网络
- 共享内存 WDK 网络
- 共享内存地址空间
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4783407b1958b9533e185c7283278f0062592de4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803485"
---
# <a name="using-shared-memory-in-network-drivers"></a>使用网络驱动程序中的共享内存





用于总线的微端口驱动程序-主直接内存访问 (DMA) 设备为网络接口卡分配共享内存，以供网络接口卡 (NIC) 和微型端口驱动程序使用。

[**NdisMAllocateSharedMemory**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatesharedmemory) 可由总线-主微型端口驱动程序调用，以分配内存，以便在网络适配器和微型端口驱动程序之间永久共享。 此函数返回共享内存的虚拟地址和物理地址。 在对 [**NdisMFreeSharedMemory**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreesharedmemory) 的调用释放内存之前，地址是有效的。

 

