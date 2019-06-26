---
title: 传入的更改呼叫参数请求
description: 传入的更改呼叫参数请求
ms.assetid: f7b9483c-070e-4a5d-a1b0-fadb65843a1e
keywords:
- 调用参数将更改 WDK 的 CoNDIS
- 传入的调用参数更改请求 WDK 的 CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21ba16f8dfea9f351d30e4c4c5383ffb3e9034ee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374835"
---
# <a name="incoming-request-to-change-call-parameters"></a>传入的更改呼叫参数请求





呼叫管理器或 MCM 驱动程序是向你发出警报与传入请求从远程方的信号消息从网络中更改活动 VC 调用参数。 是否呼叫管理器或 MCM 驱动程序支持在活动调用的动态 QoS 更改取决于信号协议。

下图显示了通过调用管理器的传入请求更改调用参数。

![说明通过调用管理器的传入请求以更改调用参数的关系图](images/cm-16.png)

下图显示了通过 MCM 驱动程序的传入请求更改调用参数。

![说明通过 mcm 驱动程序的传入请求以更改调用参数的关系图](images/fig1-16.png)

接收传入的请求以更改调用参数后, 呼叫管理器将传递到相应地修改的调用参数[ **NdisCmActivateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmactivatevc)通知的基础的微型端口驱动程序建议的 QoS 更改。 MCM 驱动程序将修改后的调用的参数传递[ **NdisMCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmactivatevc)(请参阅[激活 VC](activating-a-vc.md))。 如果基础微型端口驱动程序接受更改后的调用参数，然后调用呼叫管理器[ **NdisCmDispatchIncomingCallQosChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmdispatchincomingcallqoschange)（请参阅更改调用参数为传入请求）。 MCM 驱动程序调用[ **NdisMCmDispatchIncomingCallQosChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdispatchincomingcallqoschange)（请参阅更改调用参数为传入请求）。 呼叫管理器或 MCM 驱动程序将传递*NdisVcHandle*和缓冲[**共同\_调用\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))结构**Ndis (M) CmDispatchIncomingCallQoSChange**。

调用**Ndis (M) CmDispatchIncomingCallQoSChange**会导致调用客户端的 NDIS [ *ProtocolClIncomingCallQoSChange* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_incoming_call_qos_change)函数。 将传递 NDIS *ProtocolVcContext*标识 VC 和缓冲共同中的已修改的调用参数的句柄\_调用\_参数结构*ProtocolClIncomingCallQoSChange*.

客户端接受通过不执行任何操作，除可能更新它为 VC，维护有关 QoS 的任何状态，并将控制返回调用参数为 VC 所建议的修改。 如果执行建议的修改是不可接受，客户端可以尝试重新协商与调用参数[ **NdisClModifyCallQoS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclmodifycallqos)如果的信号协议允许 (请参阅[Client-Initiated 请求以更改调用参数](client-initiated-request-to-change-call-parameters.md))。 否则，客户端将拒绝通过关闭不带的调用所建议的 QoS 更改[ **NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclclosecall)(请参阅[Client-Initiated 请求关闭调用](client-initiated-request-to-close-a-call.md))。

之后**ProtocolClIncomingCallQoS**返回呼叫管理器或 MCM 驱动程序与客户端的接受或拒绝所建议的更改到发起请求的远程方进行通信。

 

 





