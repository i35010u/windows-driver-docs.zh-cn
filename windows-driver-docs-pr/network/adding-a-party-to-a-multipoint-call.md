---
title: 将参与方添加到多点呼叫
description: 将参与方添加到多点呼叫
keywords:
- 参与方 WDK CoNDIS
- multipoint 调用 WDK CoNDIS
- 将参与方添加到 multipoint 调用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6110145f033e0ffbffbea1ed97dbb0a237a848ca
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799417"
---
# <a name="adding-a-party-to-a-multipoint-call"></a>将参与方添加到多点呼叫





客户端请求使用 [**NdisClAddParty**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscladdparty)将参与方添加到 multipoint 调用。 客户端只能将一方添加到现有的 multipoint 调用中（即，客户端为其提供 *ProtocolPartyContext* 到 [**NdisClMakeCall**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclmakecall) 的调用） (查看) [进行调用](making-a-call.md) 。

下图显示请求的客户端，该客户端请求向 multipoint 调用添加参与方。

![说明请求向 multipoint 调用添加参与方的调用管理器客户端的关系图](images/cm-17.png)

下图显示了 MCM 驱动程序的客户端，该客户端请求向 multipoint 调用添加参与方。

![说明 mcm 驱动程序客户端的关系图，该驱动程序请求向 multipoint 调用添加参与方](images/fig1-17.png)

在调用 **NdisClAddParty** 之前，客户端必须分配并初始化其上下文区域，以便添加参与方。 通常，客户端将指向此类上下文区域的指针作为 *ProtocolPartyContext* ，并在调用 **NdisClAddParty** 时，将指向该上下文区域中的变量的指针作为 *NdisPartyHandle* 参数。

除了 *NdisVcHandle* 和 *ProtocolPartyContext* 外，客户端还会将调用参数传递 () 为 **NdisClAddParty** 的缓冲 [**联 \_ 调用 \_ 参数**](/previous-versions/windows/hardware/network/ff545384(v=vs.85))结构。 基础网络介质决定了客户端是否可以在 multipoint VC 上指定每方流量参数。

对 **NdisClAddParty** 的调用会使 NDIS 将此请求转发到调用管理器或 MCM 驱动程序的 [**ProtocolCmAddParty**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_add_party) 函数，客户端在该驱动程序中共享给定的 *NdisVcHandle* 。 NDIS 将以下内容传递给 *ProtocolCmAddParty*：

-   指示调用的 VC 的 *CallMgrVcContext* 。

-   指向 CO \_ 调用 \_ 参数结构的指针，该结构包含客户端传递给 **NdisClAddParty** 的调用参数。

-   标识要添加的参与方的 *NdisPartyHandle* 。

*ProtocolCmAddParty* 分配并初始化要添加到调用的参与方所需的任何动态资源。 在 *ProtocolCmAddParty* 中，调用管理器或 MCM 驱动程序会根据需要与网络控制设备或其他特定于媒体的代理通信，以便将指定的参与方添加到 multipoint 调用。

如果客户端传递的调用参数与已为 multipoint VC 建立的调用参数不匹配，则调用管理器或 MCM 驱动程序可以，例如：

-   如果基础网络介质在 multipoint VCs 上支持此功能，请设置每方流量参数。

-   将客户端提供的流量参数重置为其最初为 VC 建立的流量参数。

-   更改 VC 和当前连接的每个参与方的调用参数。

-   客户端尝试添加参与方失败。

对于调用管理器，或在 [**NdisMCmAddPartyComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmaddpartycomplete)（对于 MCM 驱动程序）的情况下， *ProtocolCmAddParty* 可以与 [**NdisCmAddPartyComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmaddpartycomplete)同步或异步完成。 如果调用管理器或 MCM 驱动程序以同步方式还是以异步方式完成操作，则会将缓冲调用参数传递到 NDIS。

调用 **ndis (M) CmAddPartyComplete** 导致 ndis 调用客户端的 [**ProtocolClAddPartyComplete**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_add_party_complete) 函数。 如果客户端成功添加参与方的请求，并且信号协议允许调用管理器或 MCM 驱动程序修改调用参数，则 *ProtocolClAddPartyComplete* 应 \_ \_ 在缓冲的联合调用参数结构中测试调用参数 CHANGED 标志， \_ \_ 以确定是否修改了调用参数。 信号协议确定客户端在发现对 CO 调用参数的修改时可以执行的操作 \_ \_ 。 通常，在这种情况下，客户端将调用 [**NdisClDropParty**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscldropparty) (参阅 [从 Multipoint 调用中删除参与方](dropping-a-party-from-a-multipoint-call.md)) 。

 

