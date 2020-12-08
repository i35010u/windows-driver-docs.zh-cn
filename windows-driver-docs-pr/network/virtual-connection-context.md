---
title: 虚拟连接上下文
description: 虚拟连接上下文
keywords:
- 虚拟连接 WDK 网络，上下文
- VCs WDK 网络，上下文
- 上下文 WDK 虚拟连接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 916c7254cb950ae3689b5687a2df9b246e2f43a8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840261"
---
# <a name="virtual-connection-context"></a>虚拟连接上下文





进行呼叫之前，面向连接的客户端请求面向连接的微型端口驱动程序来设置虚拟连接 (VC) 可以通过该连接来传输或接收数据包。 同样，在指示对面向连接的客户端的传入调用之前，呼叫管理器或集成微型端口调用管理器 (MCM) 驱动程序请求微型端口驱动程序为传入调用设置 VC。

VC 是两个面向连接的实体之间的逻辑连接。 面向连接的传输和接收始终发生在特定的 VC 上。

面向连接的微型端口驱动程序在与它设置的每个 VC 有关的小型小型驱动程序分配上下文区域中维护状态信息。 此每个 VC 上下文由微型端口驱动程序维护，不透明到 NDIS 和协议驱动程序。 在 [**MiniportCoCreateVc**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_create_vc) 函数中，面向连接的微型端口驱动程序将指向 VC 上下文区域的句柄传递给 NDIS，而 ndis 会将已创建的 VC 唯一标识的 *NdisVcHandle* 传递回微型端口驱动程序，并将其传递给相应的面向连接的客户端，并 (MCM) 驱动程序。

在 VC 上可以发送或接收数据之前，必须激活 VC。 调用管理器通过调用 **Ndis (M) CmActivateVc** 和传递调用参数（其中包含要激活的 VC 的特性）来启动 VC 的激活。 为响应此调用，NDIS 调用微型端口驱动程序的 [**MiniportCoActivateVc**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_activate_vc) 函数，该函数可激活 VC。

完成调用或不需要 VC 后，调用管理器可以通过调用 [**ndis (M) CmDeactivateVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdeactivatevc)来停用 vc，这会导致 ndis 调用微型端口驱动程序的 [**MiniportCoDeactivateVc**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_deactivate_vc) 函数。 面向连接的客户端或调用管理器都可以通过调用 [**NdisCoDeleteVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscodeletevc)来启动删除 VC，这会导致 NDIS 调用微型端口驱动程序的 [**MiniportCoDeleteVc**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_delete_vc) 函数。

有关 VCs 上微型端口驱动程序操作的详细信息，请参阅 [vcs 上的操作](creating-a-vc.md)。

 

