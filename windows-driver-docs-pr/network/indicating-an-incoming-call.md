---
title: 指示传入呼叫
description: 指示传入呼叫
ms.assetid: ca7f4a1f-47a2-4ac0-b4a2-d0367163135f
keywords:
- 调用安装 WDK 的 CoNDIS
- 传入呼叫 WDK 的 CoNDIS
- 指示传入呼叫 WDK 的 CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2576b6cbe67185f5e224526094acf25330c55eeb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525235"
---
# <a name="indicating-an-incoming-call"></a>指示传入呼叫





呼叫管理器或 MCM 驱动程序是向你发出警报的传入呼叫到从网络信号消息。 从这些信号消息，则呼叫管理器或 MCM 驱动程序提取的调用中，包括的 SAP 向其发送传入调用的调用参数。

下图显示了指示的传入呼叫的 MCM 驱动程序。

![说明的传入呼叫，该值指示呼叫管理器的关系图](images/cm-13.png)

下图显示了调用，该值指示传入的呼叫管理器。

![该值指示通过 mcm 驱动程序的传入呼叫](images/fig1-13.png)

如果传入的调用参数无法接受呼叫管理器或 MCM 驱动程序，它可以尝试协商与远程方这些参数中的更改，如果的信号协议允许此类协商。 或者，传入调用定向到客户端可能会尝试从呼叫管理器或 MCM 驱动程序收到的调用指示后协商调用参数 (请参阅[Client-Initiated 请求更改调用参数](client-initiated-request-to-change-call-parameters.md)). 如果呼叫管理器或 MCM 驱动程序无法协商与远程方调用的可接受调用参数，它可能会拒绝该调用。 信号协议确定什么是可以在这种情况下。

之前，该值指示对客户端的传入呼叫，呼叫管理器或 MCM 驱动程序必须标识调用定向到 SAP。 以前必须已将 SAP[注册](registering-a-sap.md)由客户端。 呼叫管理器或 MCM 驱动程序还必须启动[创建 VC](creating-a-vc.md) ，并启动[激活此 VC](activating-a-vc.md)。

呼叫管理器或 MCM 驱动程序，则表示对注册的 SAP 传入调用定向到的客户端的传入调用。 呼叫管理器指示的传入呼叫[ **NdisCmDispatchIncomingCall**](https://msdn.microsoft.com/library/windows/hardware/ff561664)。 MCM 驱动程序指示使用的传入呼叫[ **NdisMCmDispatchIncomingCall**](https://msdn.microsoft.com/library/windows/hardware/ff562830)。

在调用**Ndis (M) CmDispatchIncomingCall**，呼叫管理器或 MCM 驱动程序将传递以下：

-   *NdisSapHandle*标识传入呼叫发送到 SAP。

-   *NdisVcHandle* ，用于标识虚拟电路的传入呼叫。

-   指向类型的结构的指针[**共同\_调用\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff545384)，其中包含调用的调用参数。

在调用**Ndis (M) CmDispatchIncomingCall**会导致调用客户端的 NDIS [ **ProtocolClIncomingCall** ](https://msdn.microsoft.com/library/windows/hardware/ff570228)函数，在其中客户端接受或拒绝请求的连接。 *ProtocolClIncomingCall*应验证 SAP VC，并调用参数。

*ProtocolClIncomingCall*可以同步完成，或者它可以返回 NDIS\_状态\_挂起的和使用以异步方式完成[ **NdisClIncomingCallComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561632). 调用**NdisClIncomingCallComplete** NDIS 调用管理器的调用或 MCM 驱动程序将导致[ **ProtocolCmIncomingCallComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570245)函数。

NDIS\_同步完成的返回状态代码*ProtocolClIncomingCall*或者提供给**NdisClIncomingCallComplete**表明客户端的接受或传入呼叫 rejection。 客户端还将调用的调用参数返回中缓冲共同\_调用\_参数结构。 如果客户端查找调用参数不可接受，它可以如果的信号协议，允许请求在调用参数中的更改通过设置**标志**成员中产生的 CO\_调用\_参数调用具有结构\_参数\_已更改，并通过提供修改后调用参数中缓冲共同\_调用\_参数结构。

如果客户端接受传入呼叫，呼叫管理器或 MCM 驱动程序应发送信号消息来指示发给调用实体调用已被接受。 否则，呼叫管理器或 MCM 驱动程序应将发送信号消息来指示调用已被拒绝。 如果客户端正在请求中调用参数、 呼叫管理器或 MCM 驱动程序发送信号消息，以请求更改调用参数中的更改。

如果客户端接受调用，或如果客户端的请求由远程方已接受在调用参数中的更改，则调用的呼叫管理器[ **NdisCmDispatchCallConnected**](https://msdn.microsoft.com/library/windows/hardware/ff561661)，和 MCM 驱动程序调用[**NdisMCmDispatchCallConnected**](https://msdn.microsoft.com/library/windows/hardware/ff562826)。 在调用**Ndis (M) CmDispatchCallConnected**会导致调用客户端的 NDIS *ProtocolClCallConnected*函数。

如果客户端已拒绝调用和呼叫管理器或 MCM 驱动程序已激活的传入呼叫 VC，呼叫管理器或 MCM 驱动程序调用**Ndis (M) CmDeactivateVc**如果激活 VC 停用 VC。 呼叫管理器或 MCM 驱动程序可以故障[删除 VC](deleting-a-vc.md)通过调用[ **NdisCoDeleteVc** ](https://msdn.microsoft.com/library/windows/hardware/ff561698)在呼叫管理器的情况下或[ **NdisMCmDeleteVc** ](https://msdn.microsoft.com/library/windows/hardware/ff562819)在 MCM 驱动程序的情况下。

如果客户端接受调用，但未 （因为，例如，远程方撕裂的调用） 成功建立端到端连接，呼叫管理器或 MCM 驱动程序将不会调用**Ndis (M) CmDispatchCallConnected**. 相反，它将调用**Ndis (M) CmDispatchIncomingCloseCall**，这将导致调用客户端的 NDIS *ProtocolClIncomingCloseCall*函数。 然后，客户端必须调用[ **NdisClCloseCall** ](https://msdn.microsoft.com/library/windows/hardware/ff561627)完成调用的拆解。 呼叫管理器或 MCM 驱动程序然后调用**Ndis (M) CmDeactivateVC**到[停用 VC](deactivating-a-vc.md)它为传入的调用创建的。 呼叫管理器或 MCM 驱动程序可以故障[删除 VC](deleting-a-vc.md)通过调用[ **NdisCoDeleteVc** ](https://msdn.microsoft.com/library/windows/hardware/ff561698)在呼叫管理器的情况下或[ **NdisMCmDeleteVc** ](https://msdn.microsoft.com/library/windows/hardware/ff562819)在 MCM 驱动程序的情况下。

 

 





