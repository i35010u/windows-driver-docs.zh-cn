---
title: 获取池句柄
description: 获取池句柄
keywords:
- 池处理 WDK 网络
- 协议驱动程序 WDK 网络，池句柄
- NDIS 协议驱动程序 WDK，池句柄
- 微型端口驱动程序 WDK 网络，池句柄
- NDIS 微型端口驱动程序 WDK，池句柄
- 中间驱动程序 WDK 网络，po
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b53b8d8f2ab190a38ff9ea9294e01d922bef79a
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248692"
---
# <a name="obtaining-pool-handles"></a>获取池句柄





以下 NDIS 池分配函数需要一个分配资源的句柄：

-   [**NdisAllocateNetBufferPool**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisallocatenetbufferpool)

-   [**NdisAllocateNetBufferListPool**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisallocatenetbufferlistpool)

NDIS 6.0 驱动程序获取一个句柄，如下所示：

<a href="" id="protocol-drivers"></a>协议驱动程序  
协议驱动程序调用 [**NdisRegisterProtocolDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver) 函数以获取句柄。

<a href="" id="miniport-drivers"></a>微型端口驱动程序  
NDIS 调用 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数将句柄传递给微型端口驱动程序。

<a href="" id="intermediate-drivers"></a>中间驱动程序  
中间驱动程序调用 [**NdisRegisterProtocolDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver) 函数，以获取在发送操作中使用的池的句柄，并调用 *MiniportInitializeEx* 将句柄传递给在接收操作中使用的池的中间驱动程序的句柄。

<a href="" id="filter-drivers"></a>筛选器驱动程序  
NDIS 调用 [*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach) 函数将句柄传递给筛选器驱动程序。

<a href="" id="other-drivers"></a>其他驱动程序  
如果驱动程序无法通过上述方法之一获得句柄，驱动程序可以调用 [**NdisAllocateGenericObject**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocategenericobject) 函数以获取句柄。

 

