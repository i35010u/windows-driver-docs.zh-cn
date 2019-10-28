---
title: 开发 IPsec 兼容的标注驱动程序
description: 开发 IPsec 兼容的标注驱动程序
ms.assetid: 5e4fad4e-a790-4294-b3ac-a796f76265ad
keywords:
- IPsec WDK Windows 筛选平台，与 WFP 标注驱动程序的兼容性
- Windows 筛选平台标注驱动程序 WDK，IPsec 兼容性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aac7cf2c0144199f14a56afb37e55eb602ad3dec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838141"
---
# <a name="developing-ipsec-compatible-callout-drivers"></a>开发 IPsec 兼容的标注驱动程序


### <a name="layers-that-are-compatible-with-ipsec"></a>与 IPsec 兼容的层

若要与 windows Vista 和 Windows Server 2008 开始的 IPsec 的 Windows 实现完全兼容，应在以下运行时筛选层之一注册标注驱动程序：

<a href="" id="tcp-packet-filtering"></a>TCP 数据包筛选  
流层：

-   FWPS\_层\_流\_V4

-   FWPS\_层\_流\_V6

<a href="" id="non-tcp-and-non-error-icmp-packet-filtering"></a>非 TCP 和非错误 ICMP 数据包筛选  
数据报-数据层：

-   FWPS\_层\_数据报\_数据\_V4

-   FWPS\_层\_数据报\_数据\_V6

-   FWPS\_层\_数据报\_数据\_V4\_丢弃

-   FWPS\_层\_数据报\_数据\_V6\_放弃

在从数据报中接收传入数据包之前必须重新生成传入数据包的情况除外，在这些数据层上注册的标注驱动程序与 IPsec 兼容。

### <a name="layers-that-are-incompatible-with-ipsec"></a>与 IPsec 不兼容的层

网络和转发层与 IPsec 不兼容，因为在这些层上，IPsec 流量尚未解密或验证。 IPsec 策略在传输层强制执行，在网络层分类操作之后发生。

以下运行时筛选层与 IPsec 不兼容，因为 Windows 中的 IPsec 处理出现在以下层之下：

FWPS\_层\_入站\_IPPACKET\_V4

FWPS\_层\_入站\_IPPACKET\_V6

FWPS\_层\_入站\_IPPACKET\_V4\_丢弃

FWPS\_层\_入站\_IPPACKET\_V6\_放弃

FWPS\_层\_出站\_IPPACKET\_V4

FWPS\_层\_出站\_IPPACKET\_V6

FWPS\_层\_出站\_IPPACKET\_V4\_丢弃

FWPS\_层\_出站\_IPPACKET\_V6\_放弃

### <a name="special-considerations-for-transport-layers"></a>传输层的特殊注意事项

若要使使用传输层（FWPS\_层\_*XXX*\_传输\_V4 或 \_V6）注册的标注驱动程序与 IPsec 兼容，请遵循以下准则：

1.  在 ALE 批准接收/接受层（**FWPS\_层\_ale\_AUTH\_接收\_\_V4**或**FWPS\_\_ALE\_authentication\_receive\_接受\_V6**）除传输层（FWPS\_层\_*XXX*\_传输\_V4 或 \_V6）。

2.  若要防止内部 Windows IPsec 处理发生干扰，请在具有低于**FWPM\_子层\_通用**的子子层上注册标注。 使用[**FwpmSubLayerEnum0**](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayerenum0)函数可查找子层的权重。 有关此功能的信息，请参阅 Microsoft Windows SDK 中的[Windows 筛选平台](https://go.microsoft.com/fwlink/p/?linkid=90220)文档。

3.  需要 ALE 分类的传入传输包必须在 ALE 授权接收/接受层（**FWPS\_层\_ale\_AUTH\_接收\_accept\_V4**或**FWPS\_层之间检查\_ALE\_AUTH\_接收\_ACCEPT\_V6**）。 必须从传入传输层允许这样的数据包。 从带有 Service Pack 1 （SP1）的 Windows Vista 和 Windows Server 2008 开始，使用**FWPS\_元数据\_字段\_ALE\_分类\_必需**的元数据标志来确定是否将传入数据包显示若要将**FWPM\_层\_ALE\_身份验证\_接收\_接受\_V4**和**FWPM\_层\_ALE\_authentication\_接收\_ACCEPT\_V6**筛选层。 此元数据标志会将\_的 .Fwp\_标志替换为\_需要在 Windows Vista 中使用 **\_ALE\_分类**条件标志。

4.  若要防止内部 Windows IPsec 处理发生干扰，如果 IPsec 流量尚未 detunneled，则不要在传输层上拦截 IPsec 隧道模式的流量。 下面的代码示例演示如何绕过此类数据包。
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

5.  在传输层解密并验证受 IPsec 保护的数据包后，AH/ESP 标头将保留在 IP 标头中。 如果必须将此类数据包重新插入文本回 TCP/IP 堆栈，则必须重新生成 IP 标头以删除 AH/ESP 标头。 从 Windows Vista SP1 和 Windows Server 2008 开始，你可以通过克隆数据包并调用[**FwpsConstructIpHeaderForTransportPacket0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsconstructipheaderfortransportpacket0)函数来执行此操作，该函数将*headerIncludeHeaderSize*参数设置为 IP 标头大小克隆包。

6.  在 ALE 接收/接受层中，标注可以通过检查是否**已设置\_条件\_标志\_\_是否设置了 ipsec\_保护**标志来检测受 ipsec 保护的流量。 在传输层上，标注可以通过调用[**FwpsGetPacketListSecurityInformation0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsgetpacketlistsecurityinformation0)函数来检测受 IPsec 保护的流量，并检查 **\_\_\_** 是否在*queryFlags*参数。

### <a name="working-with-ipsec-esp-packets"></a>使用 IPsec ESP 数据包

当引擎指示已解密的封装式安全措施负载（ESP）数据包时，它将截断它们以排除尾随 ESP 数据。 由于引擎处理此类数据包的方式， [**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构中的 MDL 数据不反映正确的数据包长度。 可以使用[**NET\_BUFFER\_数据\_长度**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-data-length)宏获取**网络\_缓冲区**结构的数据长度，以获取正确的长度。

 

 





