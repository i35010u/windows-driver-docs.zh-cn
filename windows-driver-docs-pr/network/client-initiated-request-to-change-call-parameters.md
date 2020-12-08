---
title: 客户端发出的更改呼叫参数请求
description: 客户端发出的更改呼叫参数请求
keywords:
- 调用参数更改 WDK CoNDIS
- 客户端启动的调用参数更改 WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd94b107d7485ef62e2650a15cca2a49b4634fcf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826979"
---
# <a name="client-initiated-request-to-change-call-parameters"></a>客户端发出的更改呼叫参数请求





客户端通过 [**NdisClModifyCallQoS**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclmodifycallqos) (VC) ，请求活动虚拟连接上的服务质量 (QoS) 的更改。

下图显示了请求服务质量变化的呼叫管理器的客户端。

![说明请求服务质量变化的呼叫管理器客户端的关系图](images/cm-15.png)

下图显示了 MCM 驱动程序的客户端，该驱动程序请求更改服务质量。

![说明 mcm 驱动程序的客户端请求服务质量变化的关系图](images/fig1-15.png)

在对 **NdisClModifyCallQoS** 的调用中，客户端提供：

-   标识 VC 的 *NdisVcHandle* 参数。

-   一个指针，指向包含客户端正在请求的调用参数的 [**联合 \_ 调用 \_ 参数**](/previous-versions/windows/hardware/network/ff545384(v=vs.85)) 结构。

客户端可以在 QoS 中请求更改的情况由信号协议确定。

对 **NdisClModifyCallQoS** 的调用会使 NDIS 调用调用管理器或 MCM 驱动程序的 [**ProtocolCmModifyCallQoS**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_modify_qos_call)函数，该函数将 *NdisVcHandle* 输入 \_ \_ 客户端传递给 **NdisClModifyCallQoS** 的 NdisVcHandle 和缓冲的联合调用参数结构。 **ProtocolCmModifyQoS** 与网络控制设备或其他特定于媒体的代理（如其媒体的需要）进行通信，以修改已建立的虚拟连接的特定于媒体的调用参数。

与网络通信并确定更改成功后，调用管理器必须调用 [**NdisCmActivateVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmactivatevc) (并且 MCM 驱动程序必须调用 [**NdisMCmActivateVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmactivatevc)) 才能使用新的调用参数激活指定的 VC。

如果网络不接受新调用参数，或者基础微型端口驱动程序无法接受参数，则调用管理器或 MCM 驱动程序必须将 VC 还原到在尝试进行任何修改之前已存在的状态，并返回 NDIS \_ 状态 \_ 失败。

为指示客户端请求更改 QoS 的状态，调用管理器调用 [**NdisCmModifyCallQoSComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmmodifycallqoscomplete)，MCM 驱动程序调用 [**NdisMCmModifyCallQoSComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmmodifycallqoscomplete)。 在此调用中，呼叫管理器或 MCM 驱动程序通过：

-   \_指示请求状态的 NDIS 状态。

-   标识 VC 的 *NdisVcHandle* 。

-   一个指针，指向 \_ \_ 包含 VC 的调用参数的 CO 调用参数结构。

如果信号协议允许，则调用管理器或 MCM 驱动程序可以将修改后的调用参数传递回客户端。 这些修改可以是与网络协商的产品，也可以由呼叫管理器或 MCM 驱动程序提供。 调用管理器或 MCM 驱动程序应指示已通过 \_ \_ 在 CO \_ 调用参数结构中设置调用参数 CHANGED 标志来修改了调用参数 \_ 。

调用 **ndis (M) CmModifyCallQoSComplete** 导致 ndis 调用客户端的 [**ProtocolClModifyCallQoSComplete**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_modify_call_qos_complete) 函数。 NDIS 将以下内容传递给 *ProtocolClModifyCallQoSComplete*：

-   一个 NDIS \_ 状态，指示客户端更改 QoS 的请求的状态。

-   标识 VC 的 *ProtocolVcContext* 句柄。

-   指向 CO \_ 调用 \_ 参数结构的指针，该结构包含调用管理器或 MCM 驱动程序传递给 **Ndis (M) CmModifyCallQoSComplete** 的调用参数。

如果在 \_ \_ CO 调用参数结构中设置了调用参数 CHANGED 标志 \_ \_ ，客户端必须检查返回的调用参数并确定是否可以接受修改。 如果客户端对 **NdisClModifyCallQoS** 的调用成功，则 *ProtocolClModifyCallQoSComplete* 可以通过只返回 control 来接受 QoS 更改。 否则，如果信号协议允许， *ProtocolClModifyCallQoSComplete* 可以与调用管理器进行进一步的协商，只要客户端的开发人员对可能的 renegotiations 数施加了合理的限制。 或者， *ProtocolClModifyCallQoSComplete* 可以只是使用 [**NdisClCloseCall**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall) (的调用，请参阅 [客户端启动的请求以关闭调用](client-initiated-request-to-close-a-call.md)) 只要调用管理器拒绝更改 QoS 的请求，并且以前建立的 QoS 已经变为不可接受的客户端。

 

