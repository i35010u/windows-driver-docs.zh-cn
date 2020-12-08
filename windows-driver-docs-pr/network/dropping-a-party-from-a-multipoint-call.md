---
title: 从多点呼叫中删除参与方
description: 从多点呼叫中删除参与方
keywords:
- 参与方 WDK CoNDIS
- multipoint 调用 WDK CoNDIS
- 从 multipoint 调用中删除参与方
- 从 multipoint 调用中删除参与方
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ef80834847d6b143d141764822f76210c28ad3c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823041"
---
# <a name="dropping-a-party-from-a-multipoint-call"></a>从多点呼叫中删除参与方





作为 multipoint 调用的根的面向连接的客户端必须最终从该调用中删除使用 [**NdisClDropParty**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscldropparty) 或 [**NdisClCloseCall**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall)的每个参与方。

在下列情况下，客户端会从调用中删除参与方：

-   在通过 **NdisClCloseCall** 启动对 multipoint 调用的细分之前 (，请参阅 [客户端启动的请求以关闭调用](client-initiated-request-to-close-a-call.md)) ，客户端必须删除除最后一方这样的所有 **NdisClDropParty**。 客户端通过 **NdisClCloseCall** 指定要从调用中删除的最后一方。

-   为了响应远程方的请求从 multipoint 调用中删除 (请参阅 [传入请求从 Multipoint 调用中删除参与方](incoming-request-to-drop-a-party-from-a-multipoint-call.md)) ，客户端从其 [**ProtocolClIncomingDropParty**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_incoming_drop_party) 函数调用 **NdisClDropParty**。

客户端对 **NdisClDropParty** 的调用会使 NDIS 调用调用管理器或 MCM 驱动程序的 [**ProtocolCmDropParty**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_drop_party) 函数，该驱动程序将同一 *NdisVcHandle* 共享到 multipoint VC。

下图显示了请求从 multipoint 调用中删除参与方的呼叫管理器的客户端。

![说明请求从 multipoint 调用中删除参与方的呼叫管理器客户端的关系图](images/cm-18.png)

下图显示了 MCM 驱动程序的客户端，该驱动程序请求从 multipoint 调用中删除参与方。

![说明 mcm 驱动程序客户端的关系图，该驱动程序请求从 multipoint 调用中删除参与方](images/fig1-18.png)

*ProtocolCmDropParty* 与网络控制设备通信，以便从现有的 multipoint 调用中删除参与方。 NDIS 可以将指针传递给 *ProtocolCmDropParty* 一个指向缓冲区的指针，该缓冲区包含在对 **NdisClDropParty**) 的调用中提供给客户端的数据 (。 在断开连接之前， *ProtocolCmDropParty* 必须在网络中发送任何此类数据。

对于调用管理器，或在 [**NdisMCmDropPartyComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdroppartycomplete)（对于 MCM 驱动程序）的情况下， *ProtocolCmDropParty* 可能会以异步方式（或更多）与 [**NdisCmDropPartyComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdroppartycomplete)同步完成。

调用 **ndis (M) CmDropPartyComplete** 导致 ndis 调用客户端的 [**ProtocolClDropPartyComplete**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_drop_party_complete) 函数。 如果客户端正在撕裂它创建的 multipoint VC， *ProtocolClDropPartyComplete* 可以使用任何有效的 *NdisPartyHandle* 将 **NdisClDropParty** 调用到客户端的活动 multipoint VC 上的其余一方。 如果只有一个参与方仍保留在其 multipoint VC 上，则客户端应通过将其 *NdisPartyHandle* 传递到 **NdisClCloseCall** 来删除该参与方 (参阅 [客户端启动的请求以关闭调用](client-initiated-request-to-close-a-call.md)) 。

 

