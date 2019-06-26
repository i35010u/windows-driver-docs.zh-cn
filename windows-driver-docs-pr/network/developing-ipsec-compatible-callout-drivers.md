---
title: 开发 IPsec 兼容的标注驱动程序
description: 开发 IPsec 兼容的标注驱动程序
ms.assetid: 5e4fad4e-a790-4294-b3ac-a796f76265ad
keywords:
- IPsec WDK Windows 筛选平台，与 WFP 标注驱动程序的兼容性
- Windows 筛选平台标注驱动程序 WDK，IPsec 兼容性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 059c6fa975f7776fc61cced49462a50ab8cce8a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381382"
---
# <a name="developing-ipsec-compatible-callout-drivers"></a>开发 IPsec 兼容的标注驱动程序


### <a name="layers-that-are-compatible-with-ipsec"></a>IPsec 与兼容的层

若要开始使用 Windows Vista 和 Windows Server 2008 的 IPsec 的 Windows 实现与完全兼容，标注驱动程序应注册一个以下运行时筛选层：

<a href="" id="tcp-packet-filtering"></a>TCP 数据包筛选  
Stream 层：

-   FWPS\_LAYER\_STREAM\_V4

-   FWPS\_LAYER\_STREAM\_V6

<a href="" id="non-tcp-and-non-error-icmp-packet-filtering"></a>非 TCP 和非错误 ICMP 数据包筛选  
数据报数据层：

-   FWPS\_LAYER\_DATAGRAM\_DATA\_V4

-   FWPS\_LAYER\_DATAGRAM\_DATA\_V6

-   FWPS\_LAYER\_DATAGRAM\_DATA\_V4\_DISCARD

-   FWPS\_LAYER\_DATAGRAM\_DATA\_V6\_DISCARD

除了这种情况时传入的数据包必须重新生成之前它们是从数据报数据层接收的注入标注驱动程序在这些数据层注册都与 IPsec 兼容。

### <a name="layers-that-are-incompatible-with-ipsec"></a>与 IPsec 不兼容的层

网络和转发层是与 IPsec 不兼容，因为这些层面 IPsec 流量尚不支持已解密或验证。 在传输层上，网络层分类操作之后发生强制实施 IPsec 策略。

以下运行时筛选层并与 IPsec 不兼容，因为在 Windows 中处理的 IPsec 发生以下图层下方：

FWPS\_LAYER\_INBOUND\_IPPACKET\_V4

FWPS\_LAYER\_INBOUND\_IPPACKET\_V6

FWPS\_层\_入站\_IPPACKET\_V4\_放弃

FWPS\_LAYER\_INBOUND\_IPPACKET\_V6\_DISCARD

FWPS\_LAYER\_OUTBOUND\_IPPACKET\_V4

FWPS\_LAYER\_OUTBOUND\_IPPACKET\_V6

FWPS\_层\_出站\_IPPACKET\_V4\_放弃

FWPS\_层\_出站\_IPPACKET\_V6\_放弃

### <a name="special-considerations-for-transport-layers"></a>传输层的特殊注意事项

若要使是否已注册的传输层的标注驱动程序 (FWPS\_层\_*XXX*\_传输\_V4 或\_V6) 兼容的 IPsec，请按照这些指导原则：

1.  注册在 ALE 标注授权接收/接受层 (**FWPS\_层\_ALE\_身份验证\_收到\_接受\_V4**或**FWPS\_层\_ALE\_身份验证\_收到\_接受\_V6**) 除了传输层 (FWPS\_层\_*XXX*\_传输\_V4 或\_V6)。

2.  若要防止 Windows IPsec 的内部处理的干扰，请注册在具有较低权重比子层标注**FWPM\_子层\_通用**。 使用[ **FwpmSubLayerEnum0** ](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayerenum0)函数，以便查找子层的权重。 有关此函数的信息，请参阅[Windows 筛选平台](https://go.microsoft.com/fwlink/p/?linkid=90220)Microsoft Windows SDK 中的文档。

3.  要求必须在 ALE 检查 ALE 分类的传入传输数据包授权接收/接受层 (**FWPS\_层\_ALE\_身份验证\_收到\_接受\_V4**或**FWPS\_层\_ALE\_身份验证\_收到\_接受\_V6**)。 此类数据包必须允许从传入的传输层。 从 Windows Vista Service Pack 1 (SP1) 和 Windows Server 2008 开始，使用**FWPS\_元数据\_字段\_ALE\_分类\_必需**元数据的标志若要确定是否将传入数据包指定给**FWPM\_层\_ALE\_身份验证\_收到\_接受\_V4**和**FWPM\_层\_ALE\_身份验证\_收到\_接受\_V6**筛选层。 此元数据的标志将替换**FWP\_条件\_标志\_REQUIRES\_ALE\_分类**条件在 Windows Vista 中使用的标志。

4.  若要防止处理的内部 Windows IPsec 的干扰，不截获传输层的 IPsec 隧道模式流量如果未尚未 detunneled IPsec 流量。 下面的代码示例显示如何绕过此类数据包。
    ```C++
    FWPS_PACKET_LIST_INFORMATION0 packetInfo = {0};
    FwpsGetPacketListSecurityInformation0(
     layerData,
        FWPS_PACKET_LIST_INFORMATION_QUERY_IPSEC |
        FWPS_PACKET_LIST_INFORMATION_QUERY_INBOUND,
        &packetInfo
        );

    if (packetInfo.ipsecInformation.inbound.isTunnelMode &&
        !packetInfo.ipsecInformation.inbound.isDeTunneled)
    {
     classifyOut->actionType = FWP_ACTION_PERMIT;
     goto Exit;
    }
    ```

5.  受 IPsec 保护的数据包会被解密并验证在传输层后，AH/ESP 标头将保留在 IP 标头。 如果此类数据包必须进行重新插入回 TCP/IP 堆栈，必须重建 IP 标头，从而删除 AH/ESP 标头。 从 Windows Vista SP1 和 Windows Server 2008 开始，你可以执行此操作通过克隆数据包并调用[ **FwpsConstructIpHeaderForTransportPacket0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsconstructipheaderfortransportpacket0)具有函数*headerIncludeHeaderSize*参数设置为克隆的数据包的 IP 标头大小。

6.  在 ALE 接收/接受层标注可以通过检查来检测受 IPsec 保护通信是否**FWP\_条件\_标志\_IS\_IPSEC\_安全**标志设置。 在传输层上标注可以通过调用检测受 IPsec 保护的通信[ **FwpsGetPacketListSecurityInformation0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsgetpacketlistsecurityinformation0)函数，并检查是否**FWPS\_数据包\_列表\_INFORMATION0**中设置了标志*queryFlags*参数。

### <a name="working-with-ipsec-esp-packets"></a>使用 IPsec ESP 数据包

当引擎指示已解密的封装安全有效负载 (ESP) 数据包时，它将他们排除尾随 ESP 数据截断。 由于引擎可处理此类数据包中的 MDL 数据[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)结构不会反映正确的数据包长度。 可以通过使用获取正确的长度[ **NET\_缓冲区\_数据\_长度**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-data-length)宏要检索的数据长度**NET\_缓冲区**结构。

 

 





