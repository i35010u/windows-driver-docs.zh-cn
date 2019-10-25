---
title: 传入的从多点呼叫中删除参与方请求
description: 传入的从多点呼叫中删除参与方请求
ms.assetid: 3345f6f6-339f-4349-97fd-9ca9d5b2d241
keywords:
- 参与方 WDK CoNDIS
- multipoint 调用 WDK CoNDIS
- 从 multipoint 调用中删除参与方
- 从 multipoint 调用中删除参与方
- 传入的丢弃方请求 WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72c31694d0733a230c2ada4a90920a2e318ea4a0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843631"
---
# <a name="incoming-request-to-drop-a-party-from-a-multipoint-call"></a>传入的从多点呼叫中删除参与方请求





呼叫管理器或 MCM 驱动程序将收到来自远程方的传入请求的警报，通过从网络发出消息通知消息从 multipoint 调用中删除该参与方。 如果呼叫管理器或 MCM 驱动程序检测到阻止在 VC 上进一步传输数据的网络问题，则该驱动程序也可以发出信号来发送发送方。

如果从调用中删除的参与方不是 VC 上的最后一方，则调用管理器将调用[**NdisCmDispatchIncomingDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingdropparty)。 MCM 驱动程序调用[**NdisMCmDispatchIncomingDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchincomingdropparty)。 如果要删除的参与方是 VC 上的最后一方，则调用管理器会调用[**NdisCmDispatchIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingclosecall)，而 MCM 驱动程序将调用[**NdisMCmDispatchIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchincomingclosecall)（请参阅[传入请求以关闭呼叫](incoming-request-to-close-a-call.md)）。

调用**ndis （M） CmDispatchIncomingDropParty**导致 ndis 调用客户端的[**ProtocolClIncomingDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_incoming_drop_party)函数。

下面显示了通过呼叫管理器通过多点呼叫删除参与方的传入请求。

![演示通过呼叫管理器通过多点呼叫删除参与方的传入请求的关系图](images/cm-19.png)

下图显示了通过 MCM 驱动程序传入的请求，通过多点呼叫删除参与方。

![说明通过 mcm 驱动程序传入的请求通过 multipoint 调用删除参与方的关系图](images/fig1-19.png)

*ProtocolClIncomingDropParty*应执行任何协议确定的操作，以便从客户端的 multipoint VC 中删除参与方。 如果要删除的参与方不是 VC 上的最后一方，则*ProtocolClIncomingDropParty*必须调用**NdisClDropParty**（请参阅[从 Multipoint 调用中删除参与方](dropping-a-party-from-a-multipoint-call.md)）。 如果要删除的参与方是 VC 上的最后一方，则*ProtocolClIncomingDropParty*必须调用**NdisClCloseCall**（请参阅[客户端启动的请求以关闭调用](client-initiated-request-to-close-a-call.md)）。

 

 





