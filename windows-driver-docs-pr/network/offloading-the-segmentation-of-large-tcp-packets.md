---
title: 卸载大型 TCP 数据包的段
description: 卸载大型 TCP 数据包的段
ms.assetid: 6ae162fb-a8fc-47b8-80ae-ff39f3059d53
keywords:
- 任务卸载，WDK TCP/IP 传输，大数据包分段
- 大型 TCP 数据包分段 WDK 网络
- 分段的大型 TCP 数据包 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f7a386de570abd90929988ae3fdf142b339e844
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359559"
---
# <a name="offloading-the-segmentation-of-large-tcp-packets"></a>卸载大型 TCP 数据包的段





NDIS 微型端口驱动程序可以将卸载大型大于最大传输单元 (MTU) 的网络中的 TCP 数据包的分段。 支持的大型 TCP 数据包分段的 NIC 还必须能够：

-   计算的 IP 校验和将包含 IP 选项的数据包发送。

-   计算的 TCP 校验和发送包含 TCP 选项的数据包。

NDIS 版本 6.0 和更高版本支持大量发送卸载版本 1 (LSOV1)，这是类似于大量发送卸载 (LSO) NDIS 5 中。*x*。 NDIS 6.0 及更高版本还支持大量发送卸载版本 2 (LSOV2) 提供了增强的数据包分段服务，包括对 IPv6 的支持。

支持 LSOV2 和 LSOV1 的微型端口驱动程序必须确定将卸载类型从[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构 OOB 信息。 可以使用该驱动程序**类型**的成员[ **NDIS\_TCP\_大\_发送\_卸载\_NET\_缓冲区\_列表\_INFO** ](https://msdn.microsoft.com/library/windows/hardware/ff567882)结构，以确定是否使用驱动程序堆栈的 LSOV2 或 LSOV1 并执行相应卸载服务。 任何 NET\_缓冲区\_列表结构，其中包含 LSOv1 或 LSOv2 OOB 数据还包含一个[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构。 详细了解 NDIS\_TCP\_LARGE\_发送\_卸载\_NET\_缓冲区\_列表\_信息，请参阅[访问 TCP/IP卸载 NET\_缓冲区\_列出信息](accessing-tcp-ip-offload-net-buffer-list-information.md)。

但是，在其中收到微型端口的用例[ **OID\_TCP\_卸载\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff569807)关闭 LSO 功能微型端口和后微型端口OID 已成功完成，微型端口应删除所有[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)其中包含任何非零值 LSOv1 或 LSOv2 OOB 数据 ([ **NDIS\_TCP\_LARGE\_发送\_卸载\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567882)). 

TCP/IP 传输将卸载仅这些大型 TCP 数据包，满足以下条件：

-   数据包是 TCP 数据包。 TCP/IP 传输将分段的大型 UDP 数据包不卸载。

-   数据包至少必须为整除的微型端口驱动程序指定的段的最小数目。 有关详细信息，请参阅[报告的 NIC LSOV1 TCP 数据包分段功能](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md)并[报告 NIC 的 LSOV2 TCP 数据包分段功能](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)。

-   数据包不是环回数据包。

-   不将通过隧道发送数据包。

之前卸载分段，TCP/IP 传输大型 TCP 数据包：

-   更新与关联的大数据包分段信息[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。 此信息很[ **NDIS\_TCP\_LARGE\_发送\_卸载\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567882)结构，它是的一部分**NET\_缓冲区\_列表**与关联的信息**NET\_缓冲区\_列表**结构。 有关详细信息**NET\_缓冲区\_列表**信息，请参阅[访问 TCP/IP 卸载 NET\_缓冲区\_列表信息](accessing-tcp-ip-offload-net-buffer-list-information.md)。 TCP/IP 传输集**MSS**到最大段大小 (MSS) 的值。

-   数据包的 IP 标头的总长度字段中写入大型 TCP 数据包的总长度。 总长度包括 IP 标头的长度、 如果它们存在的 IP 选项的长度、 TCP 标头的长度，如果它们不存在，TCP 选项的长度和 TCP 有效负载的长度。

-   计算 1 的补数的总和 TCP pseudoheader 并将此总和写入到 TCP 标头的校验和字段。 TCP/IP 传输计算补数总和 pseudoheader 中的以下字段：源 IP 地址、 目标 IP 地址和协议。 1 的补数的总和通过 TCP/IP 传输提供 pseudoheader 为 NIC 提供了在计算每个数据包的 NIC 派生自大型 TCP 数据包而无需检查 IP 标头的实际 TCP 校验和最早开始时间。 请注意，可以规定，源 IP 地址、 目标 IP 地址、 协议和 TCP 长度通过计算伪标头校验和。 （TCP 长度为 TCP 标头的长度再加上 TCP 有效负载的长度。 TCP 长度不包括。 伪标头的长度）但是，由于基础的微型端口驱动程序和 NIC 会向下传递通过 TCP/IP 传输大数据包从生成的 TCP 段，则传输协议将不知道的每个 TCP 段的 TCP 有效负载大小以及因此不能包含 TCP 长度以伪标头。 相反，如下所述，NIC 将扩展提供的 TCP/IP 传输以覆盖每个生成的 TCP 段的 TCP 长度的伪标头校验和。

-   TCP 标头的序列号字段中写入正确的序列号。 序列号标识 TCP 有效负载的第一个字节。

后微型端口驱动程序将获取[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构中其[ *MiniportSendNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff559440)或[ **MiniportCoSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff559365)函数，它可以调用[ **NET\_缓冲区\_列表\_INFO** ](https://msdn.microsoft.com/library/windows/hardware/ff568401)宏替换 *\_Id*的**TcpLargeSendNetBufferListInfo**来获取 MSS 值编写通过 TCP/IP 传输。

微型端口驱动程序从数据包的 IP 标头获取大数据包的总长度，并使用 MSS 值划分为较小的数据包的大型 TCP 数据包。 每个较小的数据包包含 MSS 或更少的用户数据字节数。 请注意，只从分段大数据包创建的最后一个数据包应包含少于 MSS 用户数据字节数。 从分段的数据包创建的所有其他数据包应包含 MSS 用户数据字节数。 如果不遵循此规则，则创建和传输不需要额外的数据包可能会降低性能。

微型端口驱动程序客户到派生自大数据包的每个段的 MAC、 IP 和 TCP 标头。 微型端口驱动程序必须计算这些派生的数据包的 IP 和 TCP 校验的和。 若要计算大型的 TCP 数据包通过派生的每个数据包的 TCP 校验和，NIC 计算的可变部分的 TCP 校验和 （对于 TCP 标头和 TCP 有效负载），将此校验和添加到 1 的补数的总和计算通过 pseudoheaderTCP/IP 传输，然后计算 16 位的二进制反码的校验和。 有关计算此类校验和的详细信息，请参阅 RFC 793 和 RFC 1122。

下图显示了较大的数据包分段。

![说明的大数据包分段的关系图](images/segmentation.png)

大型的 TCP 数据包中的 TCP 用户数据的长度应等于或小于微型端口驱动程序将分配给的值**MaxOffLoadSize**值。 有关详细信息**MaxOffLoadSize**值，请参阅[报告 NIC 的 LSOV1 TCP 数据包分段功能](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md)和[Reporting NIC 的 LSOV2 TCP 数据包分段功能](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)。

驱动程序将发出的状态指示指示的更改后**MaxOffLoadSize**值，该驱动程序必须使崩溃如果收到 LSO 发送请求，使用以前**MaxOffLoadSize**值。 相反，该驱动程序可能会在发送请求失败。

独立问题报告中的更改的状态指示中间驱动程序**MaxOffLoadSize**值必须确保不发出状态指示基础微型端口适配器不会获取任何数据包较大的大小比**MaxOffLoadSize**微型端口适配器报告的值。

响应的中间微型端口驱动程序[OID\_TCP\_卸载\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569807)关闭 LSO 服务必须准备好为小窗口的时间，LSO 发送请求仍然无法访问微型端口驱动程序。

段数据包中的 TCP 用户数据的长度必须小于或等于 mss 交互。 MSS 是 TCP 传输使用 LSO NET 向下传递的 ULONG 值\_缓冲区\_与关联的列表信息[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。 请注意，只从分段大数据包创建的最后一个数据包应包含少于 MSS 用户数据字节数。 从分段的数据包创建的所有其他数据包应包含 MSS 用户数据字节数。 如果不遵循此规则，则创建和传输不需要额外的数据包可能会降低性能。

从较大的 TCP 数据包派生的段数据包数必须等于或大于**MinSegmentCount**微型端口驱动程序指定的值。 有关详细信息**MinSegmentCount**值，请参阅[报告 NIC 的 LSOV1 TCP 数据包分段功能](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md)和[Reporting NIC 的 LSOV2 TCP 数据包分段功能](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)。

以下的假设和限制适用于处理 IP 和 TCP 标头：

-   卸载 TCP/IP 传输大型 TCP 数据包 IP 标头中的 MF 位将不会设置，并在 IP 标头中的片段偏移量将为零。

-   大型的 TCP 数据包的 TCP 标头中的 URG、 RST、 和 SYN 标志，则不设置，并与 TCP 报头中紧急的偏移量 （指针） 将为零。

-   如果设置较大的数据包的 TCP 标头中的 FIN 位，微型端口驱动程序必须从大型 TCP 数据包创建的最后一个数据包的 TCP 标头中设置此位。

-   如果设置较大的 TCP 数据包的 TCP 标头中的 PSH 位，微型端口驱动程序必须从大型 TCP 数据包创建的最后一个数据包的 TCP 标头中设置此位。

-   如果大 TCP 数据包包含 IP 选项或 TCP 选项 （或两者），微型端口驱动程序将复制这些选项不变，为每个包，它派生自大型 TCP 数据包。 具体而言，NIC 将递增时间戳选项。

-   数据包的第一个 MDL 将为所有数据包标头 （以太网、 IP、 TCP）。 将不会跨多个 MDLs 拆分标头。 
    > [!TIP]
    > 当启用 LSO，此假设才有效。 否则，如果未启用 LSO，微型端口驱动程序不能假定 IP 标头都在同一个以太网标头作为 MDL。


微型端口驱动程序必须发送数据包[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构，它将接收 NET 顺序\_缓冲区\_列表从 TCP/IP 传输的结构。

在处理大的 TCP 数据包时，微型端口适配器负责仅适用于对数据包进行分段和附加到派生自大型 TCP 数据包的数据包的 MAC、 IP 和 TCP 标头。 TCP/IP 传输会执行所有其他任务 （例如调整发送窗口大小基于远程主机的接收窗口大小）。

完成发送操作的大型数据包之前 (如使用[ **NdisMSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563668)或[ **NdisMCoSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563570))，微型端口驱动程序写入[ **NDIS\_TCP\_大\_发送\_卸载\_NET\_缓冲区\_列表\_INFO** ](https://msdn.microsoft.com/library/windows/hardware/ff567882)值 (NET\_缓冲区\_列表信息的大量发送卸载) 使用的所有数据包中的已成功发送的 TCP 用户数据字节总数从较大的 TCP 数据包创建。

除了上述 LSO 要求，还必须支持 LSOV2 的微型端口驱动程序：

-   支持 IPv4 或 IPv6 或 IPv4 和 IPv6。

-   每个网络接口卡 (NIC) 生成的段数据包中支持的较大的数据包中的 IPv4 选项的复制。

-   支持 IPv6 扩展标头，从大型的 TCP 数据包中，复制每个 TCP 段数据包中。

-   在每个 TCP 段数据包的微型端口驱动程序将生成支持 TCP 选项的复制。

-   使用中的 IP 和 TCP 标头[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)为模板，以生成对于每个段数据包的 TCP/IP 标头的结构。

-   使用介于 0x0000 和 0x7FFF 中 IP 标识号 (IP ID) 值。 （0x8000 到 0xFFFF 的范围被保留的 TCP 烟囱卸载功能的设备。）例如，如果模板 IP 标头开头 0x7FFE 的标识字段值，则第一个 TCP 段数据包必须 0x7FFE 后, 跟 0x7FFF、 0x0000、 0x0001 和等等的 IP ID 值。

-   使用中的字节偏移量**TcpHeaderOffset**的成员[ **NDIS\_TCP\_大\_发送\_卸载\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567882)来确定 TCP 标头，从该数据包的第一个字节开始的位置。

-   限制数[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构所带来的每个 LSOV2 [ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)到一个结构。

-   确定长度的第一个网络数据包的总长度\_缓冲区结构在 NET\_缓冲区\_列表结构。

-   支持 TCP 选项、 IP 选项和 IP 扩展标头。

-   微型端口驱动程序发送操作完成后，必须设置**LsoV2TransmitComplete.Reserved**的成员[ **NDIS_TCP_LARGE_SEND_OFFLOAD_NET_BUFFER_LIST_INFO** ](https://msdn.microsoft.com/library/windows/hardware/ff567882)为零的结构和**LsoV2TransmitComplete.Type** NDIS_TCP_LARGE_SEND_OFFLOAD_V2_TYPE 的成员。 
 

 





