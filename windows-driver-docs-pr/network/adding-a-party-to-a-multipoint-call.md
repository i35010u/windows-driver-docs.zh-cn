---
title: 将参与方添加到多点呼叫
description: 将参与方添加到多点呼叫
ms.assetid: 2d6b8ebe-8028-46d0-91bd-7f95b0375cc4
keywords:
- WDK 的 CoNDIS 的参与方
- 多点调用 WDK 的 CoNDIS
- 将参与方添加到多点调用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 680a652a4a6538948dfce38eb495a887769a6547
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362915"
---
# <a name="adding-a-party-to-a-multipoint-call"></a>将参与方添加到多点呼叫





客户端请求使用的多点调用添加的参与方[ **NdisClAddParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscladdparty)。 客户端可以将参与方添加到现有的多点调用-也就是说，调用仅为其提供客户端*ProtocolPartyContext*到[ **NdisClMakeCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclmakecall)（请参阅[调用](making-a-call.md))。

下图显示的某调用的客户端请求将参与方添加到 multipoint 呼叫管理器。

![说明客户端的请求添加到多点调用的参与方的呼叫管理器的关系图](images/cm-17.png)

下图显示了客户端的请求添加到多点调用的参与方的 MCM 驱动程序。

![说明请求添加到多点调用的参与方的 mcm 驱动程序的客户端的关系图](images/fig1-17.png)

在调用之前**NdisClAddParty**，客户端必须分配并初始化其要添加的参与方的上下文区域。 客户端通常将指针传递到此类的上下文区域作为*ProtocolPartyContext*并为该上下文的区域内的变量的指针*NdisPartyHandle*时它们调用的参数**NdisClAddParty**。

除了*NdisVcHandle*和一个*ProtocolPartyContext*，客户端将调用参数传递 (缓冲[**共同\_调用\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))结构) 到**NdisClAddParty**。 基础网络中确定客户端是否可以在 multipoint VC 上指定每个参与方流量参数。

在调用**NdisClAddParty**会导致此请求转发到的 NDIS [ **ProtocolCmAddParty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cm_add_party)呼叫管理器或客户端与之共享的 MCM 驱动程序的函数给定*NdisVcHandle* 。 NDIS 将传递到以下*ProtocolCmAddParty*:

-   一个*CallMgrVcContext* ，该值指示调用 VC。

-   指针到 CO\_调用\_包含客户端传递到调用参数的参数结构**NdisClAddParty**。

-   *NdisPartyHandle* ，它标识要添加的参与方。

*ProtocolCmAddParty*分配并初始化所需的参与方添加到在调用任何动态资源。 从*ProtocolCmAddParty*，呼叫管理器或 MCM 驱动程序与通信网络控制设备或其他特定于媒体的代理，在必要时，将指定的参与方添加到多点调用。

如果客户端与那些已建立的 multipoint VC、 呼叫管理器或 MCM 驱动程序不匹配的参数可以执行的调用中传递：

-   如果基础网络中支持此功能在 multipoint VCs 上，设置的每个参与方流量参数。

-   客户端提供流量参数重置为那些最初为 VC 建立。

-   VC 和当前连接上其每个参与方，请更改调用参数。

-   无法在客户端尝试添加的参与方。

*ProtocolCmAddParty*可以使用完成同步或者，更可能，以异步方式[ **NdisCmAddPartyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmaddpartycomplete)，在调用管理器的情况下或[ **NdisMCmAddPartyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmaddpartycomplete)，在 MCM 驱动程序的情况下。 是否呼叫管理器或 MCM 驱动程序以同步方式还是以异步方式完成的操作，它会传递到 NDIS 的缓冲的调用参数。

在调用**Ndis (M) CmAddPartyComplete**会导致调用客户端的 NDIS [ **ProtocolClAddPartyComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_cl_add_party_complete)函数。 如果添加参与方的客户端的请求成功，信号协议允许修改所调用的参数，则呼叫管理器或 MCM 驱动程序*ProtocolClAddPartyComplete*应测试调用\_参数\_已更改的标志中缓冲共同\_调用\_参数结构，以确定是否已修改的调用参数。 信号的协议决定客户端可以执行的操作如果它找到对共同修改\_调用\_不可接受的参数。 通常情况下，客户端调用[ **NdisClDropParty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscldropparty)在这种情况下 (请参阅[Multipoint 调用正在删除参与方](dropping-a-party-from-a-multipoint-call.md))。

 

 





