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
- 中间驱动程序 WDK 网络、 采购订单
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37a2b132d4f371e0461511950017cd60e16a32fa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354507"
---
# <a name="obtaining-pool-handles"></a>获取池句柄





以下 NDIS 池分配函数需要分配资源的句柄：

-   [**NdisAllocateNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbufferpool)

-   [**NdisAllocateNetBufferListPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbufferlistpool)

NDIS 6.0 驱动程序，如下所示获取句柄：

<a href="" id="protocol-drivers"></a>协议驱动程序  
协议驱动程序调用[ **NdisRegisterProtocolDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisregisterprotocoldriver)函数来获取句柄。

<a href="" id="miniport-drivers"></a>微型端口驱动程序  
NDIS 调用[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数以将该句柄传递给微型端口驱动程序。

<a href="" id="intermediate-drivers"></a>中间驱动程序  
驱动程序调用的中间[ **NdisRegisterProtocolDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisregisterprotocoldriver)函数中使用的池发送操作和 NDIS 获取句柄调用*MiniportInitializeEx*到将句柄传递给中间驱动程序，用于在中使用的池接收操作。

<a href="" id="filter-drivers"></a>筛选器驱动程序  
NDIS 调用[ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)函数以将该句柄传递给筛选器驱动程序。

<a href="" id="other-drivers"></a>其他驱动程序  
如果驱动程序无法通过上述方法之一获取句柄，该驱动程序可以调用[ **NdisAllocateGenericObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocategenericobject)函数来获取的句柄。

 

 





