---
title: 客户端发起的结束呼叫请求
description: 客户端发起的结束呼叫请求
keywords:
- 客户端启动的关闭呼叫请求 WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cec2babb36f68dd16bf244655e1f25700d24dd1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787277"
---
# <a name="client-initiated-request-to-close-a-call"></a>客户端发起的结束呼叫请求





如果客户端正在关闭多个参与方仍处于连接状态的 multipoint 调用，则必须先调用 [**NdisClDropParty**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscldropparty) ，以删除来自呼叫的所有 (，请参阅 [从 Multipoint 调用中删除参与方](dropping-a-party-from-a-multipoint-call.md)) 。

客户端使用 [**NdisClCloseCall**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall)启动调用的结束。 下图显示一个客户端，该客户端通过调用管理器启动调用的结束。

![说明客户端通过调用管理器启动调用结束的关系图](images/cm-20.png)

下图显示一个客户端，该客户端通过 MCM 驱动程序启动调用的结束。

![说明客户端通过 mcm 驱动程序启动调用结束的关系图](images/fig1-20.png)

面向连接的客户端通常会在以下任何一种情况下调用 **NdisClCloseCall** ：

-   关闭已建立的传出或传入呼叫。

-   通过 [**ProtocolClIncomingCloseCall**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_incoming_close_call) 函数来细分已建立的呼叫 (参阅 [传入请求以关闭呼叫](incoming-request-to-close-a-call.md)) 。

-   在 [*ProtocolClIncomingCallQoSChange*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_incoming_call_qos_change) 函数中，如果远程方提议的 QoS 更改不可接受，则从该功能中拉出已建立的呼叫 (参阅 [传入请求更改调用参数](incoming-request-to-change-call-parameters.md)) 。

-   在 [**ProtocolClModifyCallQoSComplete**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_modify_call_qos_complete) 函数中，如果客户端提议的 QoS 更改对于远程方是不可接受的，则从该函数中断开已建立的调用 (参阅 [客户端发起的更改调用参数](client-initiated-request-to-change-call-parameters.md)) 的请求。

客户端对 **NdisClCloseCall** 的调用会使 NDIS 调用调用管理器或 MCM 驱动程序的 [**ProtocolCmCloseCall**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_close_call) 函数。 *ProtocolCmCloseCall* 必须与网络控制设备通信，以终止本地节点和远程节点之间的连接。

如果向 *ProtocolCmCloseCall* 传递了显式 *CallMgrPartyContext*，则终止的调用是一个 multipoint 调用。 调用管理器或 MCM 驱动程序必须根据其媒体类型对其网络硬件执行任何必要的网络通信，以将调用作为 multipoint 调用终止。

NDIS 可以向 *ProtocolCmCloseCall* 传递指向包含客户端在调用 **NdisClClose** 时提供的数据的缓冲区的指针。 此数据可以是诊断数据，用于指示调用被关闭的原因或信号协议所需的任何其他数据。 在完成呼叫终止之前， *ProtocolCmCloseCall* 必须在网络中发送任何此类数据。 如果不支持使用连接终止的连接来发送数据，则调用管理器或 MCM 驱动程序应返回 NDIS \_ 状态 " \_ 无效数据" \_ 。

如果调用管理器) 或 [**NdisMCmCloseCallComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmclosecallcomplete) (为 MCM driver) ，则 *ProtocolCmCloseCall* 可能会以同步方式同步或更好地与 [**NdisCmCloseCallComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmclosecallcomplete) (异步完成。 调用 **ndis (M) CmCloseCallComplete** 导致 ndis 调用客户端的 [**ProtocolClCloseCallComplete**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_close_call_complete) 函数。

然后，调用管理器或 MCM 驱动程序必须通过分别调用 [**NdisCmDeactivateVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdeactivatevc) 或 ([**NdisMCmDeactivateVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeactivatevc) 来启动用于调用的 VC 的停用，请参阅 [停用 vc](deactivating-a-vc.md)) 。 然后，VC (client、call manager 或 MCM driver) 的创建者可以根据需要启动 VC (的删除操作，请参阅 [删除 vc](deleting-a-vc.md)) 。

 

