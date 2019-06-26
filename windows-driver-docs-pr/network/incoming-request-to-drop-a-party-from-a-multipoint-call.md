---
title: 传入的从多点呼叫中删除参与方请求
description: 传入的从多点呼叫中删除参与方请求
ms.assetid: 3345f6f6-339f-4349-97fd-9ca9d5b2d241
keywords:
- WDK 的 CoNDIS 的参与方
- 多点调用 WDK 的 CoNDIS
- 从 multipoint 调用删除参与方
- 从 multipoint 调用中删除参与方
- 传入下拉方请求 WDK 的 CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bd3c784ded5fd6059bb590acfeb252d6476d0cd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374854"
---
# <a name="incoming-request-to-drop-a-party-from-a-multipoint-call"></a>传入的从多点呼叫中删除参与方请求





呼叫管理器或 MCM 驱动程序是向你发出警报与传入请求从远程方从网络信号消息从 multipoint 调用中删除该参与方。 呼叫管理器或 MCM 驱动程序还可以发出信号检测到网络问题而导致进一步 VC 上的传输数据时删除参与方的传入请求。

如果正在删除从调用方不是在 VC 的最后一个参与方，呼叫管理器会调用[ **NdisCmDispatchIncomingDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmdispatchincomingdropparty)。 MCM 驱动程序调用[ **NdisMCmDispatchIncomingDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdispatchincomingdropparty)。 如果要删除的参与方是 VC 上的最后一个参与方，呼叫管理器将调用[ **NdisCmDispatchIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmdispatchincomingclosecall)，并调用 MCM 驱动程序[ **NdisMCmDispatchIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdispatchincomingclosecall)(请参阅[传入的请求，以关闭调用](incoming-request-to-close-a-call.md))。

调用**Ndis (M) CmDispatchIncomingDropParty**会导致调用客户端的 NDIS [ **ProtocolClIncomingDropParty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_incoming_drop_party)函数。

下图显示通过调用传入的请求管理器来删除通过 multipoint 调用方。

![说明通过调用管理器的传入请求，若要删除通过 multipoint 调用方的关系图](images/cm-19.png)

下图显示了通过 MCM 驱动程序的传入请求，若要删除通过 multipoint 调用方。

![说明通过 mcm 驱动程序的传入请求，若要删除通过 multipoint 调用方的关系图](images/fig1-19.png)

*ProtocolClIncomingDropParty*应执行任何协议确定从客户端的 multipoint VC 删除参与方的操作。 如果要删除的参与方不是在 VC 的最后一个参与方*ProtocolClIncomingDropParty*必须调用**NdisClDropParty**(请参阅[Multipoint 调用正在删除参与方](dropping-a-party-from-a-multipoint-call.md)). 如果要删除的参与方是在 VC 的最后一个参与方*ProtocolClIncomingDropParty*必须调用**NdisClCloseCall**(请参阅[Client-Initiated 请求关闭调用](client-initiated-request-to-close-a-call.md))。

 

 





