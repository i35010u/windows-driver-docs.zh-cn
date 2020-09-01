---
title: 传入的更改呼叫参数请求
description: 传入的更改呼叫参数请求
ms.assetid: f7b9483c-070e-4a5d-a1b0-fadb65843a1e
keywords:
- 调用参数更改 WDK CoNDIS
- 传入呼叫参数更改请求 WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6f20cb107cb72cd016c96092082404f58f0a4e3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217834"
---
# <a name="incoming-request-to-change-call-parameters"></a>传入的更改呼叫参数请求





呼叫管理器或 MCM 驱动程序将收到来自远程方的传入请求的警报，通过从网络发出消息通知来更改活动 VC 上的调用参数。 调用管理器或 MCM 驱动程序是否支持活动调用的动态 QoS 更改取决于信号协议。

下图显示了通过调用管理器来更改调用参数的传入请求。

![演示通过调用管理器更改调用参数的传入请求的关系图](images/cm-16.png)

下图显示了通过 MCM 驱动程序更改调用参数的传入请求。

![说明通过 mcm 驱动程序传入请求以更改调用参数的传入请求的关系图](images/fig1-16.png)

接收到更改调用参数的传入请求后，调用管理器会将相应修改的调用参数传递给 [**NdisCmActivateVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmactivatevc) ，以通知基础微型端口驱动程序已建议的 QoS 更改。 MCM 驱动程序将修改的调用参数传递给 [**NdisMCmActivateVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmactivatevc) (请参阅 [激活 VC](activating-a-vc.md)) 。 如果基础微型端口驱动程序接受更改的调用参数，则调用管理器将调用 [**NdisCmDispatchIncomingCallQosChange**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingcallqoschange) (参阅传入请求以更改调用参数) 。 MCM 驱动程序调用 [**NdisMCmDispatchIncomingCallQosChange**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchincomingcallqoschange) (参阅传入请求以更改调用参数) 。 调用管理器或 MCM 驱动程序将 *NdisVcHandle* 和缓冲的 [**联合 \_ 调用 \_ 参数**](/previous-versions/windows/hardware/network/ff545384(v=vs.85)) 结构传递到 **Ndis (M) CmDispatchIncomingCallQoSChange**。

调用 **ndis (M) CmDispatchIncomingCallQoSChange** 导致 ndis 调用客户端的 [*ProtocolClIncomingCallQoSChange*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_incoming_call_qos_change) 函数。 NDIS 将标识 VC 的 *ProtocolVcContext* 句柄和已进行缓冲的联合调用参数结构中的已修改调用参数传递 \_ \_ 给 *ProtocolClIncomingCallQoSChange*。

客户端通过不执行任何操作接受对 VC 的调用参数的建议的修改，但可能会更新其对 VC 的 QoS 和返回控件所维护的任何状态。 如果无法接受建议的修改，则客户端可以尝试使用 [**NdisClModifyCallQoS**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclmodifycallqos) 重新协商调用参数（如果有信号协议允许） (参阅 [客户端发起的更改调用参数](client-initiated-request-to-change-call-parameters.md)) 的请求。 否则，客户端会通过使用 [**NdisClCloseCall**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall) 来拆开调用来拒绝建议的 QoS 更改 (参阅 [客户端启动的请求以关闭调用](client-initiated-request-to-close-a-call.md)) 。

**ProtocolClIncomingCallQoS**返回后，调用管理器或 MCM 驱动程序会将建议的更改的接受或拒绝传递给发出请求的远程参与方。

 

