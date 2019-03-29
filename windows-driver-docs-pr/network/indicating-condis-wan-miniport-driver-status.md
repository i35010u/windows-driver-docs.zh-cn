---
title: 指示 CoNDIS WAN 微型端口驱动程序状态
description: 指示 CoNDIS WAN 微型端口驱动程序状态
ms.assetid: c12492d7-e25d-4c80-8f2d-1e89931577ed
keywords:
- WAN 的 CoNDIS 驱动程序 WDK 网络状态
- 状态指示 WDK 网络，WAN 的 CoNDIS 微型端口驱动程序
- NDIS_STATUS_WAN_CO_LINKPARAMS
- NDIS_STATUS_WAN_CO_FRAGMENT
- 指示 WDK 的 CoNDIS WAN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02b25983a82137ac9b73b3853a478bb4c47539bc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567851"
---
# <a name="indicating-condis-wan-miniport-driver-status"></a>指示 CoNDIS WAN 微型端口驱动程序状态





CoNDIS WAN 的微型端口驱动程序调用[ **NdisMCoIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563562)达指示状态更改绑定协议驱动程序。 指示从 CoNDIS 微型端口驱动程序或 MCM 的状态的详细信息，请参阅[，该值指示微型端口驱动程序状态](indicating-miniport-driver-status.md)。

绑定的协议驱动程序可以忽略这些状态指示。 但是，处理这些指示通常会导致改进了协议驱动程序和微型端口驱动程序的性能。

NDISWAN 中间驱动程序将状态指示转发到 NDIS。 NDIS 调用[ **ProtocolCoStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff570258)绑定的协议驱动程序或配置管理器的函数。 这些协议驱动程序或配置管理器可以登录这些迹象，并可能采取纠正措施，如有必要。

WAN 的 CoNDIS 微型端口驱动程序，调用[ **NdisMCoIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563562)是相同的 CoNDIS 任何微型端口驱动程序，不同之处在于 CoNDIS WAN 微型端口驱动程序指示为每个特定于 WAN 的状态微型端口驱动程序的 nic 的虚拟连接 (VC) 微型端口驱动程序调用**NdisMCoIndicateStatusEx**显式 VC 句柄来指示这些更改会给共享此 VC 协议驱动程序。 如果该驱动程序指定 **NULL * * * NdisVcHandle*，状态与 NIC 的状态的常规更改

每个状态指示提供信息的两个基本的部分：

-   指定的常规状态的状态代码。 有有限的数量的已定义的常规状态代码;此列表受到将来的扩展。

-   包含状态信息的缓冲区。 此状态信息可以是特定 NIC，或 WAN 的 CoNDIS 微型端口驱动程序，特定于 NIC 上 VC 例如，一个缓冲区可能包含 X.25 连接，最近减少到原来的两个新的传输的速度。

CoNDIS WAN VC 状态指示是：

-   NDIS\_状态\_WAN\_共同\_LINKPARAMS

    CoNDIS WAN 的微型端口驱动程序调用[ **NdisMCoIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563562)以指示已更改的 NIC 处于活动状态的特定 VC 参数。 在此调用中，微型端口驱动程序将该句柄传递给在 VC *NdisVcHandle*参数，NDIS\_状态\_WAN\_CO\_LINKPARAMS 中的*GeneralStatus*参数，并指向的指针[ **WAN\_共同\_LINKPARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff565819)结构*StatusBuffer*参数。 WAN\_CO\_LINKPARAMS VC 介绍了新的参数。

-   NDIS\_状态\_WAN\_共同\_片段

    CoNDIS WAN 的微型端口驱动程序调用**NdisMCoIndicateStatusEx**以指示它已收到部分数据包从 VC 的终结点。 在此调用中，微型端口驱动程序将该句柄传递给在 VC *NdisVcHandle*参数，NDIS\_状态\_WAN\_CO\_片段中*GeneralStatus*参数，并指向的指针[ **NDIS\_WAN\_CO\_片段**](https://msdn.microsoft.com/library/windows/hardware/ff559030)结构*StatusBuffer*参数。 NDIS\_WAN\_共同\_片段介绍了已接收到的部分数据包的原因。

    此指示发生后，面向连接的客户端应将帧发送到另一端的 VC 面向连接的客户端。 这些帧将通知部分数据包种情况下，在对方端点，以便在对方端点不需要等待的超时发生。

    NDISWAN 监视器丢弃数据包，方法是计算上每个 VC 片段指示的项数。

 

 





