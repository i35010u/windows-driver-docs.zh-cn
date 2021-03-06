---
title: 开发 IPsec 兼容的标注驱动程序
description: 开发 IPsec 兼容的标注驱动程序
keywords:
- IPsec WDK Windows 筛选平台，与 WFP 标注驱动程序的兼容性
- Windows 筛选平台标注驱动程序 WDK，IPsec 兼容性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfad816fff2357eb3f396c8fae800b7e89a1bb9a
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248350"
---
# <a name="developing-ipsec-compatible-callout-drivers"></a>开发 IPsec 兼容的标注驱动程序


### <a name="layers-that-are-compatible-with-ipsec"></a>与 IPsec 兼容的层

若要与 windows Vista 和 Windows Server 2008 开始的 IPsec 的 Windows 实现完全兼容，应在以下运行时筛选层之一注册标注驱动程序：

<a href="" id="tcp-packet-filtering"></a>TCP 数据包筛选  
流层：

-   FWPS \_ 层 \_ 流 \_ V4

-   FWPS \_ 层 \_ 流 \_ V6

<a href="" id="non-tcp-and-non-error-icmp-packet-filtering"></a>非 TCP 和非错误 ICMP 数据包筛选  
Datagram-Data 层：

-   FWPS \_ 层 \_ \_ 数据报数据 \_ V4

-   FWPS \_ 层 \_ \_ 数据报数据 \_ V6

-   FWPS \_ 层 \_ \_ 数据报数据 \_ V4 \_ 丢弃

-   FWPS \_ 层 \_ \_ 数据报数据 \_ V6 \_ 丢弃

在从数据报中接收传入数据包之前必须重新生成传入数据包的情况除外，在这些数据层上注册的标注驱动程序与 IPsec 兼容。

### <a name="layers-that-are-incompatible-with-ipsec"></a>与 IPsec 不兼容的层

网络和转发层与 IPsec 不兼容，因为在这些层上，IPsec 流量尚未解密或验证。 IPsec 策略在传输层强制执行，在网络层分类操作之后发生。

以下运行时筛选层与 IPsec 不兼容，因为 Windows 中的 IPsec 处理出现在以下层之下：

FWPS \_ 层 \_ 入站 \_ IPPACKET \_ V4

FWPS \_ 层 \_ 入站 \_ IPPACKET \_ V6

FWPS \_ 层 \_ 入站 \_ IPPACKET \_ V4 \_ 丢弃

FWPS \_ 层 \_ 入站 \_ IPPACKET \_ V6 \_ 丢弃

FWPS \_ 层 \_ 出站 \_ IPPACKET \_ V4

FWPS \_ 层 \_ 出站 \_ IPPACKET \_ V6

FWPS \_ 层 \_ 出站 \_ IPPACKET \_ V4 \_ 丢弃

FWPS \_ 层 \_ 出站 \_ IPPACKET \_ V6 \_ 丢弃

### <a name="special-considerations-for-transport-layers"></a>传输层的特殊注意事项

若要使使用传输层注册的标注驱动程序 (FWPS \_ 层 \_ *XXX* \_ 传输 \_ V4 或 \_ V6) 与 IPsec 兼容，请遵循以下准则：

1.  在 ALE 授权接收/接受层上注册标注 (**FWPS \_ 层 \_ ale \_ 身份验证接收 \_ \_ accept \_ V4** 或 **FWPS \_ 层 \_ ale \_ 身份验证 \_ \_ \_** 接收 accept V6) 除传输层以外，还 (FWPS \_ 层 \_ *XXX* \_ 传输 \_ V4 或 \_ V6) 。

2.  若要防止内部 Windows IPsec 处理出现干扰，请将标注注册到权重低于 **FWPM \_ 子层 \_ 通用** 的子子层。 使用 [**FwpmSubLayerEnum0**](/windows/win32/api/fwpmu/nf-fwpmu-fwpmsublayerenum0) 函数可查找子层的权重。 有关此功能的信息，请参阅 Microsoft Windows SDK 中的 [Windows 筛选平台](/windows/win32/fwp/windows-filtering-platform-start-page) 文档。

3.  需要 ALE 分类的传入传输数据包必须在 ALE 授权接收/接受层上检查 (**FWPS \_ 层 \_ ale \_ 身份验证接收 \_ \_ accept \_ V4** 或 **FWPS \_ 层 \_ ale \_ 身份验证 \_ 接收 \_ accept \_ V6**) 。 必须从传入传输层允许这样的数据包。 从带有 Service Pack 1 的 Windows Vista (SP1) 和 Windows Server 2008 开始，使用 **FWPS \_ METADATA \_ 字段 \_ ALE \_ 分类 \_ 所需** 的元数据标志来确定传入数据包是否将指示 **FWPM \_ 层 \_ ale \_ 身份验证 \_ 接收 \_ accept \_ V4** 和 **FWPM \_ 层 \_ ale \_ 验证 \_ 接收 \_ 接受 \_ V6** 筛选层。 此元数据标志取代了 Windows Vista 中使用的 "已使用的 **\_ \_ \_ \_ ALE \_ 分类** 条件" 标志。

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

5.  在传输层解密并验证受 IPsec 保护的数据包后，AH/ESP 标头将保留在 IP 标头中。 如果必须将此类数据包重新插入文本回 TCP/IP 堆栈，则必须重新生成 IP 标头以删除 AH/ESP 标头。 从 Windows Vista SP1 和 Windows Server 2008 开始，你可以通过克隆数据包并调用 [**FwpsConstructIpHeaderForTransportPacket0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsconstructipheaderfortransportpacket0) 函数来执行此操作，该函数将 *headerIncludeHeaderSize* 参数设置为克隆数据包的 IP 标头大小。

6.  在 ALE 接收/接受层中，标注可以通过检查是否设置了 " **.Fwp \_ 条件 \_ 标志是否 \_ 为 \_ ipsec \_ 安全** 标志" 来检测受 ipsec 保护的流量。 在传输层上，标注可以通过调用 [**FwpsGetPacketListSecurityInformation0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsgetpacketlistsecurityinformation0)函数并检查是否在 *queryFlags* 参数中设置了 **FWPS \_ 数据包 \_ 列表 \_ INFORMATION0** 标志来检测受 IPsec 保护的流量。

### <a name="working-with-ipsec-esp-packets"></a>使用 IPsec ESP 数据包

当引擎指示解密的封装安全负载 (ESP) 数据包时，它将截断它们以排除尾随 ESP 数据。 由于引擎处理此类数据包的方式， [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer) 结构中的 MDL 数据不反映正确的数据包长度。 可以通过使用 [**net \_ buffer \_ DATA \_ length**](/windows-hardware/drivers/ddi/nblaccessors/nf-nblaccessors-net_buffer_data_length) 宏检索 **网络 \_ 缓冲区** 的数据长度来获取正确的长度。

