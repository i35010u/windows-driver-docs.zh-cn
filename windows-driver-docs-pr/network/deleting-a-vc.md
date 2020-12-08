---
title: 删除 VC
description: 删除 VC
keywords:
- 虚拟连接 WDK CoNDIS，删除
- 正在删除虚拟连接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afd5c4c4380973d850dd39820905dd32720ac9bd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782297"
---
# <a name="deleting-a-vc"></a>删除 VC





只有面向连接的客户端、调用管理器或 MCM 驱动程序启动 (VC) 创建虚拟线路后，才能启动删除该 VC。 因此，客户端会删除先前为传出呼叫创建的一个 VC，呼叫管理器或 MCM 驱动程序将删除以前为网络上的传入呼叫创建的 vc，并删除先前创建的用于通过网络交换信号消息的 VC。  (MCM 驱动程序不调用 NDIS 来删除它创建用于交换信号消息的 VC。 MCM 驱动程序将使用不透明的内部操作删除此类 VC。 ) 

面向连接的客户端或调用管理器使用 [**NdisCoDeleteVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscodeletevc)启动删除 VC。

下图显示了启动删除 VC 的呼叫管理器的客户端。

![说明启动删除 vc 的调用管理器客户端的关系图](images/cm-09.png)

下图显示了启动删除 VC 的 MCM 驱动程序的客户端。

![说明启动删除 vc 的 mcm 驱动程序的客户端的关系图](images/fig1-09.png)

下图显示了启动删除 VC 的调用管理器。

![说明调用管理器启动删除 vc 的关系图](images/cm-10.png)

当客户端或调用管理器调用 **NdisCoDeleteVc** 或 MCM 驱动程序调用 **NdisMCmDeleteVc** 时，给定 VC 上必须没有未处理的调用，并且 VC 必须已被 [停用](deactivating-a-vc.md)。 为了满足这些要求，意味着满足以下条件：

-   客户端已在给定的 *NdisVcHandle* 中调用了 [**NdisClCloseCall**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall) ，但其 [结束调用请求](client-initiated-request-to-close-a-call.md)已成功完成。

-   调用管理器已经调用了 [**NdisCmDeactivateVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdeactivatevc) ，或者 MCM 驱动程序已通过给定的 *NdisVcHandle* 调用了 [**NdisMCmDeactivateVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeactivatevc) ，而停用请求已成功完成 (参阅 [传入请求以关闭调用](incoming-request-to-close-a-call.md)) 。

客户端或调用管理器对 **NdisCoDeleteVc** 的调用会使 NDIS 调用基础微型端口驱动程序的 [**MiniportCoDeleteVc**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_delete_vc)函数，以及调用方用来共享 (*NdisVcHandle* 的客户端或调用管理器的 [**ProtocolCoDeleteVc**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_delete_vc)函数) 。

*MiniportCoDeleteVc* 释放为 vc 分配的任何资源，以及 vc 的微型端口驱动程序的上下文。 *ProtocolCoDeleteVc* 释放客户端或调用管理器用于对 VC 执行操作和跟踪状态的任何资源。 *MiniportCoDeleteVc* 和 *ProtocolCoDeleteVc* 都是同步函数，无法返回 NDIS \_ 状态 "挂起" \_ 。

MCM 驱动程序使用 [**NdisMCmDeleteVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeletevc) 启动删除 VC (参阅下图) 。

![说明启动删除 vc 的 mcm 驱动程序的示意图 ](images/fig1-10.png)

MCM 驱动程序对 **NdisMCmDeleteVc** 的调用会使 NDIS 调用 MCM 驱动程序与 *NdisVcHandle* 共享的客户端的 [**ProtocolCoDeleteVc**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_delete_vc)函数。

当 **NdisCoDeleteVc** 或 **NdisMCmDeleteVc** 返回 control 时， *NdisVcHandle* 不再有效。

 

