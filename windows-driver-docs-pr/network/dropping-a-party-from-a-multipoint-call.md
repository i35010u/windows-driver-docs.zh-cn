---
title: 从多点呼叫中删除参与方
description: 从多点呼叫中删除参与方
ms.assetid: db23e911-7c70-432e-992a-fdfdf8cb28ae
keywords:
- 参与方 WDK CoNDIS
- multipoint 调用 WDK CoNDIS
- 从 multipoint 调用中删除参与方
- 从 multipoint 调用中删除参与方
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6364fd1a2e55d0df092ccd1dfe66503c47197e7d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834822"
---
# <a name="dropping-a-party-from-a-multipoint-call"></a>从多点呼叫中删除参与方





作为 multipoint 调用的根的面向连接的客户端必须最终从该调用中删除使用[**NdisClDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscldropparty)或[**NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall)的每个参与方。

在下列情况下，客户端会从调用中删除参与方：

-   在使用**NdisClCloseCall**（请参阅[客户端启动的请求来关闭调用](client-initiated-request-to-close-a-call.md)）之前，客户端必须删除除了最后一方的所有调用**NdisClDropParty**。 客户端通过**NdisClCloseCall**指定要从调用中删除的最后一方。

-   为了响应从 multipoint 调用中删除远程方的请求（请参阅[传入请求从 Multipoint 调用中删除参与方](incoming-request-to-drop-a-party-from-a-multipoint-call.md)），客户端从其[**ProtocolClIncomingDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_incoming_drop_party)函数调用**NdisClDropParty**。

客户端对**NdisClDropParty**的调用会使 NDIS 调用调用管理器或 MCM 驱动程序的[**ProtocolCmDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_drop_party)函数，该驱动程序将同一*NdisVcHandle*共享到 multipoint VC。

下图显示了请求从 multipoint 调用中删除参与方的呼叫管理器的客户端。

![说明请求从 multipoint 调用中删除参与方的呼叫管理器客户端的关系图](images/cm-18.png)

下图显示了 MCM 驱动程序的客户端，该驱动程序请求从 multipoint 调用中删除参与方。

![说明 mcm 驱动程序客户端的关系图，该驱动程序请求从 multipoint 调用中删除参与方](images/fig1-18.png)

*ProtocolCmDropParty*与网络控制设备通信，以便从现有的 multipoint 调用中删除参与方。 NDIS 可以传递到*ProtocolCmDropParty*指向包含数据的缓冲区的指针（在对**NdisClDropParty**的调用中提供给客户端）。 在断开连接之前， *ProtocolCmDropParty*必须在网络中发送任何此类数据。

对于调用管理器，或在[**NdisMCmDropPartyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdroppartycomplete)（对于 MCM 驱动程序）的情况下， *ProtocolCmDropParty*可能会以异步方式（或更多）与[**NdisCmDropPartyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdroppartycomplete)同步完成。

调用**ndis （M） CmDropPartyComplete**会使 ndis 调用客户端的[**ProtocolClDropPartyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_drop_party_complete)函数。 如果客户端正在撕裂它创建的 multipoint VC，则*ProtocolClDropPartyComplete*可以使用任何有效的*NdisPartyHandle*对客户端的活动 multipoint VC 上的其余一方调用**NdisClDropParty**. 如果只有一个参与方仍保留在其 multipoint VC 上，则客户端应通过将其*NdisPartyHandle*传递到**NdisClCloseCall**来删除该参与方（请参阅[客户端启动的请求以关闭调用](client-initiated-request-to-close-a-call.md)）。

 

 





