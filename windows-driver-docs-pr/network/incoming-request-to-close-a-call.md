---
title: 传入的结束呼叫请求
description: 传入的结束呼叫请求
ms.assetid: ecdcb74d-6151-4e2b-8fe7-95f455f4deb4
keywords:
- 传入的关闭呼叫请求 WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6891838bcbe172aa51ca7b0296b7f4ce4fed35b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843633"
---
# <a name="incoming-request-to-close-a-call"></a>传入的结束呼叫请求





当远程客户端关闭调用时，本地调用管理器或 MCM 驱动程序必须指示此传入请求到本地客户端。 若要指示此类请求，调用管理器将调用[**NdisCmDispatchIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingclosecall) ，并将*CLOSESTATUS*设置为 NDIS\_状态\_成功（见下图）。

![说明通过调用管理器来结束呼叫的传入请求的关系图 ](images/cm-22.png)

MCM 驱动程序调用[**NdisMCmDispatchIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchincomingclosecall) ，以指示关闭调用的传入请求（见下图）。

![说明通过 mcm 驱动程序来结束呼叫的传入请求的关系图 ](images/fig1-22.png)

调用管理器或 MCM 驱动程序还可以调用**Ndis （M） CmDispatchIncomingCloseCall**：

-   如果它确定面向连接的客户端在调用参数中请求无法接受的更改，以响应之前调用管理器或 MCM 指示的传入调用，则从其[**ProtocolCmIncomingCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_incoming_call_complete)函数。驱动程序（请参阅[传入请求以更改调用参数](incoming-request-to-change-call-parameters.md)）。

-   如果异常网络条件强制调用管理器清除活动调用。

调用**ndis （M） CmDispatchIncomingCloseCall**会使 ndis 在该连接上调用面向连接的客户端的[**ProtocolClIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_incoming_close_call)函数。 *ProtocolClIncomingCloseCall*应执行任何协议确定的操作，例如通知其自己的客户端或连接中断的客户端。 如果要关闭的调用是客户端创建的 multipoint VC，则*ProtocolClIncomingCloseCall*必须一次或多次调用[**NdisClDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscldropparty) （请参阅[从 Multipoint 调用中删除参与方](dropping-a-party-from-a-multipoint-call.md)）。

然后， *ProtocolClIncomingCloseCall*必须调用[**NDISCLCLOSECALL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall)（如果 vc 是客户端创建的 multipoint VC，则为 vc 上最后一方的句柄），以确认客户端将不再尝试发送或预期接收数据此特定的 VC。 如果调用管理器或 MCM 驱动程序创建了此 VC，则*ProtocolClIncomingCloseCall*应在调用**NdisClCloseCall**后返回 control。 调用管理器或 MCM 驱动程序还必须停用 VC （请参阅[停用 vc](deactivating-a-vc.md)）。

如果客户端最初为传出调用创建了此 VC，而*CloseStatus*为 NDIS\_状态\_成功，则*ProtocolClIncomingCloseCall*可以选择性地使用[**NdisCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscodeletevc)删除 vc （请参阅[删除 vc](deleting-a-vc.md)）或为另一调用重用 VC。 如果*CloseStatus*不是 NDIS\_状态\_SUCCESS，则*ProtocolClIncomingCloseCall*必须调用**NdisCoDeleteVc**。

如果调用管理器或 MCM 驱动程序最初为传入调用创建了此 VC，则调用管理器或 MCM 驱动程序可以选择通过分别调用**NdisCoDeleteVc**或[**NDISMCMDELETEVC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeletevc)来[删除 vc](deleting-a-vc.md) 。

 

 





