---
title: 指示来电
description: 指示来电
ms.assetid: ca7f4a1f-47a2-4ac0-b4a2-d0367163135f
keywords:
- 调用设置 WDK CoNDIS
- 传入呼叫 WDK CoNDIS
- 指示传入呼叫 WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98105b99f67daa32d53988bb141c16a3a85307e7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824728"
---
# <a name="indicating-an-incoming-call"></a>指示来电





呼叫管理器或 MCM 驱动程序通过从网络发出消息通知传入呼叫。 通过这些信号消息，呼叫管理器或 MCM 驱动程序将提取呼叫的调用参数，包括传入呼叫寻址到的 SAP。

下图显示了指示传入呼叫的 MCM 驱动程序。

![说明指示传入呼叫的呼叫管理器的关系图](images/cm-13.png)

下图显示了指示传入呼叫的呼叫管理器。

![指示通过 mcm 驱动程序的传入呼叫](images/fig1-13.png)

如果呼叫管理器或 MCM 驱动程序无法接受传入呼叫参数，则它可能会尝试在信号协议允许此类协商的情况下与远程方协商这些参数的更改。 或者，传入呼叫定向到的客户端在收到来自呼叫管理器或 MCM 驱动程序的调用指示后，可能会尝试协商调用参数（请参阅[客户端启动的更改调用参数的请求](client-initiated-request-to-change-call-parameters.md)）。 如果调用管理器或 MCM 驱动程序无法与远程方协商可接受的调用参数，则它可能会拒绝调用。 信号协议确定了在这种情况下可能会发生的情况。

在指示对客户端的传入调用之前，呼叫管理器或 MCM 驱动程序必须确定调用定向到的 SAP。 SAP 之前必须已由客户端[注册](registering-a-sap.md)。 调用管理器或 MCM 驱动程序还必须启动[vc 的创建](creating-a-vc.md)并启动[此 vc 的激活](activating-a-vc.md)。

然后，调用管理器或 MCM 驱动程序指示对注册了传入呼叫的 SAP 的客户端的传入调用。 呼叫管理器使用[**NdisCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingcall)指示传入呼叫。 MCM 驱动程序指示使用[**NdisMCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchincomingcall)的传入呼叫。

在调用**Ndis （M） CmDispatchIncomingCall**时，调用管理器或 MCM 驱动程序将传递以下内容：

-   一个*NdisSapHandle* ，用于标识传入呼叫寻址到的 SAP。

-   标识传入调用的虚拟线路的*NdisVcHandle* 。

-   指向类型为[**CO\_调用**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))的结构的指针\_参数，其中包含调用的调用参数。

调用**ndis （M） CmDispatchIncomingCall**会使 ndis 调用客户端的[**ProtocolClIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_incoming_call)函数，其中客户端接受或拒绝请求的连接。 *ProtocolClIncomingCall*应验证 SAP、VC 和 call 参数。

*ProtocolClIncomingCall*可以同步完成，也可以返回 NDIS\_状态\_挂起，并与[**NdisClIncomingCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclincomingcallcomplete)异步完成。 调用**NdisClIncomingCallComplete**会导致 NDIS 调用调用管理器或 MCM 驱动程序的[**ProtocolCmIncomingCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_incoming_call_complete)函数。

*ProtocolClIncomingCall*或提供给**NdisClIncomingCallComplete**的同步完成返回的 NDIS\_状态代码指示客户端接受或拒绝传入呼叫。 客户端还会在缓冲联\_调用\_参数结构中返回调用的调用参数。 如果客户端发现调用参数不可接受，则它可以（如果是由信号协议允许）通过使用 CALL\_参数设置 CO\_调用\_参数结构中的**Flags**成员来请求更改调用参数\_更改，并通过在缓冲联\_调用\_参数结构中提供修改后的调用参数。

如果客户端接受传入呼叫，则呼叫管理器或 MCM 驱动程序应发送信号消息，向调用方指明调用已被接受。 否则，呼叫管理器或 MCM 驱动程序应发送信号消息，指示调用已被拒绝。 如果客户端在调用参数中请求更改，则调用管理器或 MCM 驱动程序将发送信号消息，请求在调用参数中进行更改。

如果客户端接受呼叫，或者客户端在调用参数中请求的更改已被远程方接受，则呼叫管理器将调用[**NdisCmDispatchCallConnected**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchcallconnected)，MCM 驱动程序将调用[**NdisMCmDispatchCallConnected**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchcallconnected)。 调用**ndis （M） CmDispatchCallConnected**会使 ndis 调用客户端的*ProtocolClCallConnected*函数。

如果客户端拒绝了呼叫，并且调用管理器或 MCM 驱动程序已经为传入呼叫激活了一个 VC，则调用管理器或 MCM 驱动程序将调用**Ndis （M） CmDeactivateVc**来停用 vc （如果启用了 vc）。 然后，调用管理器或 MCM 驱动程序可以通过在调用管理器的情况下调用[**NdisCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscodeletevc)或[**NDISMCMDELETEVC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeletevc) （对于 MCM 驱动程序）来启动[删除 VC](deleting-a-vc.md) 。

如果客户端接受呼叫但未成功建立端到端连接（例如，远程方 t) 调用），则调用管理器或 MCM 驱动程序将不会调用**Ndis （M） CmDispatchCallConnected**。 相反，它将调用**ndis （M） CmDispatchIncomingCloseCall**，这会导致 ndis 调用客户端的*ProtocolClIncomingCloseCall*函数。 然后，客户端必须调用[**NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall)来完成拆卸呼叫。 然后，调用管理器或 MCM 驱动程序调用**Ndis （M） CmDeactivateVC**来[停用](deactivating-a-vc.md)它为传入调用创建的 VC。 然后，调用管理器或 MCM 驱动程序可以通过在调用管理器的情况下调用[**NdisCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscodeletevc)或[**NDISMCMDELETEVC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeletevc) （对于 MCM 驱动程序）来启动[删除 VC](deleting-a-vc.md) 。

 

 





