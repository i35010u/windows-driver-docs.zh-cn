---
title: 客户端发起的结束呼叫请求
description: 客户端发起的结束呼叫请求
ms.assetid: 1eb9c898-086a-463f-a4ae-d5a8727f7d73
keywords:
- 客户端启动的关闭呼叫请求 WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9ce9ba9b3240657ef29dd29012e5075e660a734
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835175"
---
# <a name="client-initiated-request-to-close-a-call"></a>客户端发起的结束呼叫请求





如果客户端正在关闭多个参与方仍处于连接状态的 multipoint 调用，则必须首先调用[**NdisClDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscldropparty) ，以删除来自呼叫的所有其他参与方（请参阅[从 Multipoint 调用中删除参与方](dropping-a-party-from-a-multipoint-call.md)）。

客户端使用[**NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall)启动调用的结束。 下图显示一个客户端，该客户端通过调用管理器启动调用的结束。

![说明客户端通过调用管理器启动调用结束的关系图](images/cm-20.png)

下图显示一个客户端，该客户端通过 MCM 驱动程序启动调用的结束。

![说明客户端通过 mcm 驱动程序启动调用结束的关系图](images/fig1-20.png)

面向连接的客户端通常会在以下任何一种情况下调用**NdisClCloseCall** ：

-   关闭已建立的传出或传入呼叫。

-   通过[**ProtocolClIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_incoming_close_call)函数来细分已建立的调用（请参阅[传入请求以关闭呼叫](incoming-request-to-close-a-call.md)）。

-   在[*ProtocolClIncomingCallQoSChange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_incoming_call_qos_change)函数中，如果远程方提议的 QoS 更改不可接受，则将其拉出已建立的调用（请参阅[传入请求以更改调用参数](incoming-request-to-change-call-parameters.md)）。

-   在[**ProtocolClModifyCallQoSComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_modify_call_qos_complete)函数中，如果客户端提议的 QoS 更改对于远程方是不可接受的，则从该函数中断开已建立的调用（请参阅[客户端启动的更改调用参数的请求](client-initiated-request-to-change-call-parameters.md)）。

客户端对**NdisClCloseCall**的调用会使 NDIS 调用调用管理器或 MCM 驱动程序的[**ProtocolCmCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_close_call)函数。 *ProtocolCmCloseCall*必须与网络控制设备通信，以终止本地节点和远程节点之间的连接。

如果向*ProtocolCmCloseCall*传递了显式*CallMgrPartyContext*，则终止的调用是一个 multipoint 调用。 调用管理器或 MCM 驱动程序必须根据其媒体类型对其网络硬件执行任何必要的网络通信，以将调用作为 multipoint 调用终止。

NDIS 可以向*ProtocolCmCloseCall*传递指向包含客户端在调用**NdisClClose**时提供的数据的缓冲区的指针。 此数据可以是诊断数据，用于指示调用被关闭的原因或信号协议所需的任何其他数据。 在完成呼叫终止之前， *ProtocolCmCloseCall*必须在网络中发送任何此类数据。 如果不支持使用连接终止的连接来发送数据，则调用管理器或 MCM 驱动程序应返回 NDIS\_状态\_无效的\_数据。

*ProtocolCmCloseCall*可以使用[**NdisCmCloseCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmclosecallcomplete)（在调用管理器的情况下）或[**NdisMCmCloseCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmclosecallcomplete)（在 MCM 驱动程序的情况下）以同步方式同步完成。 调用**ndis （M） CmCloseCallComplete**导致 ndis 调用客户端的[**ProtocolClCloseCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_close_call_complete)函数。

然后，调用管理器或 MCM 驱动程序必须通过分别调用[**NdisCmDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdeactivatevc)或[**NdisMCmDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeactivatevc)（请参阅[停用 vc](deactivating-a-vc.md)）启动用于调用的 VC 的停用。 然后，VC （客户端、调用管理器或 MCM 驱动程序）的创建者可以选择启动 VC 的删除（请参阅[删除 vc](deleting-a-vc.md)）。

 

 





