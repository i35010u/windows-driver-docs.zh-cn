---
title: 获取池句柄
description: 获取池句柄
ms.assetid: 752b0d64-2ca3-4dc0-a6cd-642e96af1f8f
keywords:
- 池处理 WDK 网络
- 协议驱动程序 WDK 网络，池句柄
- NDIS 协议驱动程序 WDK，池句柄
- 微型端口驱动程序 WDK 网络，池句柄
- NDIS 微型端口驱动程序 WDK，池句柄
- 中间驱动程序 WDK 网络，po
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3afff6a3b6b5f7616f47ca54e080ae917ad8d1ac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837743"
---
# <a name="obtaining-pool-handles"></a>获取池句柄





以下 NDIS 池分配函数需要一个分配资源的句柄：

-   [**NdisAllocateNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferpool)

-   [**NdisAllocateNetBufferListPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlistpool)

NDIS 6.0 驱动程序获取一个句柄，如下所示：

<a href="" id="protocol-drivers"></a>协议驱动程序  
协议驱动程序调用[**NdisRegisterProtocolDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver)函数以获取句柄。

<a href="" id="miniport-drivers"></a>微型端口驱动程序  
NDIS 调用[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数将句柄传递给微型端口驱动程序。

<a href="" id="intermediate-drivers"></a>中间驱动程序  
中间驱动程序调用[**NdisRegisterProtocolDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver)函数，以获取在发送操作中使用的池的句柄，并调用*MiniportInitializeEx*将句柄传递给在接收操作中使用的池的中间驱动程序的句柄。

<a href="" id="filter-drivers"></a>筛选器驱动程序  
NDIS 调用[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)函数将句柄传递给筛选器驱动程序。

<a href="" id="other-drivers"></a>其他驱动程序  
如果驱动程序无法通过上述方法之一获得句柄，驱动程序可以调用[**NdisAllocateGenericObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocategenericobject)函数以获取句柄。

 

 





