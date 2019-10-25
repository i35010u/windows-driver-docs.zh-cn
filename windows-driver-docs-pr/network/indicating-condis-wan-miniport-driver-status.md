---
title: 指示 CoNDIS WAN 微型端口驱动程序状态
description: 指示 CoNDIS WAN 微型端口驱动程序状态
ms.assetid: c12492d7-e25d-4c80-8f2d-1e89931577ed
keywords:
- CoNDIS WAN 驱动程序 WDK 网络，状态
- 状态指示 WDK 网络，CoNDIS WAN 微型端口驱动程序
- NDIS_STATUS_WAN_CO_LINKPARAMS
- NDIS_STATUS_WAN_CO_FRAGMENT
- 指示 WDK CoNDIS WAN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 495da24443a92f9d70320983f545af027bc4d6cb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824710"
---
# <a name="indicating-condis-wan-miniport-driver-status"></a>指示 CoNDIS WAN 微型端口驱动程序状态





CoNDIS WAN 微型端口驱动程序调用[**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex) ，以指示状态更改向上到绑定协议驱动程序。 有关从 CoNDIS 微型端口驱动程序或 MCM 指示状态的详细信息，请参阅[指示微型端口驱动程序状态](indicating-miniport-driver-status.md)。

绑定协议驱动程序可以忽略这些状态指示。 不过，处理这些指示通常会提高协议驱动程序和微型端口驱动程序的性能。

NDISWAN 中间驱动程序将状态指示转发到 NDIS。 NDIS 调用绑定协议驱动程序或配置管理器的[**ProtocolCoStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_status_ex)函数。 这些协议驱动程序或 configuration manager 可以记录这些指示，并在必要时采取纠正措施。

对于 CoNDIS WAN 微型端口驱动程序，对[**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)的调用与任何 CoNDIS 微型端口驱动程序中的调用相同，只是 CoNDIS wan 微型端口驱动程序指示微型端口驱动程序 NIC 上每个虚拟连接（VC）的特定于 WAN 的状态。 微型端口驱动程序使用显式 VC 句柄调用**NdisMCoIndicateStatusEx** ，以指示对共享此 VC 的协议驱动程序所做的更改。 如果驱动程序指定了 **NULL ** * * NdisVcHandle，则状态将是 NIC 状态的常规更改。

每个状态指示都提供两条基本信息：

-   指定常规状态的状态代码。 定义的常规状态代码数量有限：此列表取决于将来的扩展。

-   包含状态信息的缓冲区。 此状态信息可以特定于 NIC，或特定于 NIC 上的 VC 的 CoNDIS WAN 微型端口驱动程序。 例如，缓冲区可能包含连接速度最快的 X 25 连接，这是最近降低了两倍。

CoNDIS WAN VC 状态指示如下：

-   \_WAN\_CO\_LINKPARAMS 的 NDIS\_状态

    CoNDIS WAN 微型端口驱动程序调用[**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex) ，以指示 NIC 上处于活动状态的特定 VC 的参数已发生更改。 在此调用中，微型端口驱动程序将句柄传递给*NdisVcHandle*参数中的 VC，NDIS\_状态\_WAN\_*GeneralStatus*参数中的 CO\_LINKPARAMS，并将指针连接到[**wan\_co\_** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565819(v=vs.85)) *StatusBuffer*参数中的 LINKPARAMS 结构。 WAN\_CO\_LINKPARAMS 介绍了 VC 的新参数。

-   \_WAN\_CO\_片段的 NDIS\_状态

    CoNDIS WAN 微型端口驱动程序调用**NdisMCoIndicateStatusEx** ，以指示它从 VC 终结点接收到部分数据包。 在此调用中，微型端口驱动程序将句柄传递给*NdisVcHandle*参数中的 VC，NDIS\_状态\_WAN\_*GeneralStatus*参数中的 CO\_片段，并将指针连接到[**ndis\_WAN\_** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559030(v=vs.85)) *StatusBuffer*参数中的 _ CO\_片段结构。 NDIS\_WAN\_CO\_片段描述接收部分数据包的原因。

    出现这种情况后，面向连接的客户端应将帧发送到 VC 的另一端的面向连接的客户端。 这些帧将通知部分数据包情况的反向终结点，以便相反的终结点不需要等待超时。

    NDISWAN 通过计算每个 VC 上碎片指示的数目来监视丢弃的数据包。

 

 





