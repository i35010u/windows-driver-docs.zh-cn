---
title: 客户端发出的更改呼叫参数请求
description: 客户端发出的更改呼叫参数请求
ms.assetid: 1534dbf9-3ee0-490a-9633-55827ffbcb1a
keywords:
- 调用参数将更改 WDK 的 CoNDIS
- 客户端发起的呼叫参数将更改 WDK 的 CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e0bf10fdaba812a0fea23f29b3a2ef40527a372
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374976"
---
# <a name="client-initiated-request-to-change-call-parameters"></a>客户端发出的更改呼叫参数请求





客户端请求的服务质量 (QoS) 上的活动的虚拟连接 (VC) 中的更改与[ **NdisClModifyCallQoS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclmodifycallqos)。

下图显示了调用管理器请求的服务质量中的更改的客户端。

![说明调用管理器请求的服务质量中的更改的客户端的关系图](images/cm-15.png)

下图显示了请求的服务质量中的更改的 MCM 驱动程序的客户端。

![说明客户端的请求的服务质量中的更改的 mcm 驱动程序的关系图](images/fig1-15.png)

在调用**NdisClModifyCallQoS**，客户端提供：

-   *NdisVcHandle*标识 VC 参数。

-   一个指向[**共同\_调用\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))结构，其中包含客户端正在请求的调用参数。

信号协议取决于在其下一个客户端可以请求 QoS 中的更改的情况。

在调用**NdisClModifyCallQoS** NDIS 调用管理器的调用或 MCM 驱动程序将导致[ **ProtocolCmModifyCallQoS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cm_modify_qos_call)函数，哪些输入*NdisVcHandle*和缓冲 CO\_调用\_客户端传递到的参数结构**NdisClModifyCallQoS**。 **ProtocolCmModifyQoS**与网络控制设备或其他特定于媒体的代理，如需其媒体，可以修改已建立的虚拟连接的特定于媒体的调用参数。

在出现网络通信，并确定所做的更改已成功完成之后, 呼叫管理器必须调用[ **NdisCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmactivatevc)(和 MCM 驱动程序必须调用[ **NdisMCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmactivatevc)) 来激活使用新的调用参数指定的 VC。

如果网络不接受新的调用参数或呼叫管理器或 MCM 驱动程序的基础的微型端口驱动程序不能接受参数，如果必须还原到之前尝试进行任何修改，即已存在的状态的 VC 并返回 NDIS\_状态\_失败。

若要指示要更改 QoS 的客户端的请求的状态，调用管理器会调用[ **NdisCmModifyCallQoSComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmmodifycallqoscomplete)，并调用 MCM 驱动程序[ **NdisMCmModifyCallQoSComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmmodifycallqoscomplete)。 在此调用中，呼叫管理器或 MCM 驱动程序将传递：

-   NDIS\_指示请求的状态的状态。

-   *NdisVcHandle*标识 VC。

-   指针到 CO\_调用\_VC 包含调用参数的参数结构。

如果允许信号协议，呼叫管理器或 MCM 驱动程序可以修改后的调用将参数传递回客户端。 这些修改可以是与网络的协商的产品或它们可以通过呼叫管理器或 MCM 驱动程序本身提供。 呼叫管理器或 MCM 驱动程序应指示调用参数已被修改的设置在调用\_参数\_CHANGED 标志中产生的 CO\_调用\_参数结构。

在调用**Ndis (M) CmModifyCallQoSComplete**会导致调用客户端的 NDIS [ **ProtocolClModifyCallQoSComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_modify_call_qos_complete)函数。 NDIS 将传递到以下*ProtocolClModifyCallQoSComplete*:

-   NDIS\_状态，指示要更改 QoS 的客户端的请求的状态。

-   一个*ProtocolVcContext*标识 VC 句柄。

-   指针到 CO\_调用\_包含通过调用管理器或 MCM 驱动程序添加到传递的调用参数的参数结构**Ndis (M) CmModifyCallQoSComplete**。

如果在调用\_参数\_CHANGED 标志设置中产生的 CO\_调用\_参数结构客户端必须检查返回的调用参数并确定是否可接受所做的修改。 如果客户端的调用**NdisClModifyCallQoS**成功， *ProtocolClModifyCallQoSComplete* QoS 更改通过简单地返回控件可以接受。 否则为*ProtocolClModifyCallQoSComplete*可以吸引进一步协商与呼叫管理器中，如果允许通过信号协议和，只要客户端的开发人员的各种可能的放置一些合理的限制重协商。 或者， *ProtocolClModifyCallQoSComplete*只需拆开与调用[ **NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclclosecall)(请参阅[Client-Initiated 请求到关闭调用](client-initiated-request-to-close-a-call.md)) 每当呼叫管理器会拒绝请求以更改 QoS 和以前建立的 QoS 变得无法接受客户端。

 

 





