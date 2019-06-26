---
title: 虚拟连接上下文
description: 虚拟连接上下文
ms.assetid: 9b318f9d-70f4-41b5-acab-5a193f7d2ab4
keywords:
- 虚拟连接 WDK 网络、 上下文
- VCs WDK 网络上下文
- 上下文 WDK 虚拟连接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5da8eeff07fec2e74931944c90f440ab7124f94
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377009"
---
# <a name="virtual-connection-context"></a>虚拟连接上下文





调用前，面向连接的客户端请求的面向连接的微型端口驱动程序设置的数据包可以传输或接收到的虚拟连接 (VC)。 同样，在之前，该值指示对面向连接的客户端的传入呼叫，呼叫管理器或集成的微型端口调用管理器 (MCM) 驱动程序请求微型端口驱动程序，若要设置的传入呼叫 VC。

VC 是两个面向连接的实体之间的逻辑连接。 面向连接的传输和接收始终在特定 VC 上发生。

面向连接的微型端口驱动程序维护微型端口驱动程序分配的上下文区域中设置了每个 VC 有关的状态信息。 此上下文中每个 VC 维护的微型端口驱动程序，到 NDIS 和协议驱动程序不透明。 在其[ **MiniportCoCreateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_create_vc)函数、 NDIS 和 NDIS 的 VC 上下文区域的句柄通过面向连接的微型端口驱动程序传递*NdisVcHandle* ，唯一地标识创建的 VC 回微型端口驱动程序、 适当的面向连接的客户端，以及呼叫管理器或集成的微型端口调用管理器 (MCM) 驱动程序。

可以发送或接收上 VC 数据之前，必须激活 VC。 呼叫管理器通过调用启动激活 VC **Ndis (M) CmActivateVc**并传递包含 VC 要激活的特征的调用参数。 NDIS 以响应此调用，调用微型端口驱动程序[ **MiniportCoActivateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_activate_vc)函数，这便激活 VC。

呼叫管理器调用已完成或 VC 是否则不需要后，可以停 VC 用通过调用[ **Ndis (M) CmDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmdeactivatevc)，这将导致调用微型端口驱动程序的 NDIS [ **MiniportCoDeactivateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_deactivate_vc)函数。 面向连接的客户端或呼叫管理器可以通过调用启动的 VC 删除[ **NdisCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscodeletevc)，这将导致调用微型端口驱动程序的 NDIS [ **MiniportCoDeleteVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_delete_vc)函数。

有关对 VCs 的微型端口驱动程序操作的详细信息，请参阅[VCs 操作](operations-on-vcs.md)。

 

 





