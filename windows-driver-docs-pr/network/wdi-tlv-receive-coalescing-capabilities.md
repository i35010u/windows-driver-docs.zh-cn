---
title: WDI_TLV_RECEIVE_COALESCING_CAPABILITIES
description: WDI_TLV_RECEIVE_COALESCING_CAPABILITIES 是包含硬件辅助接收筛选器功能的 TLV。
ms.assetid: 87BC1F55-90C6-4B22-9E8E-A54FF42515F3
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_RECEIVE_COALESCING_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cec4fa9135d910e3a5fde13cc94401e59df22716
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105872"
---
# <a name="wdi_tlv_receive_coalescing_capabilities"></a>WDI \_ TLV \_ 接收 \_ 合并 \_ 功能


WDI \_ tlv \_ 接收 \_ 合并 \_ 功能是包含硬件辅助接收筛选器功能的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x9A

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>类型</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT32</td>
<td>已启用筛选器类型。 标志的按位 "或"，用于指定启用的接收筛选器的类型。 以下标志是有效的。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_VMQ_FILTERS_ENABLED</dt>
<dd><p>指定启用 VMQ 筛选器。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_PACKET_COALESCING_FILTERS_ENABLED</dt>
<dd><p>指定启用 NDIS 数据包合并接收筛选器。</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>已启用队列类型。 标志的按位 "或"，用于指定已启用的接收队列的类型。 以下标志是有效的。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_VM_QUEUES_ENABLED</dt>
<dd><p>指定启用虚拟机 (VM) 队列。 当启用了微型端口驱动程序以使用 VMQ 接口时，将使用 VM 队列。</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>网络适配器支持的 VM 队列的数量。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>支持的 VM 队列属性。 标志的按位 "或"，用于指定网络适配器支持的 VM 队列属性。 以下标志是有效的。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_MSI_X_SUPPORTED</dt>
<dd><p>网络适配器为每个接收队列分配了一个 MSI-X 表条目。 对于多个接收队列，网络适配器不得使用一个 MSI-X 表项。 对于支持 VMQ 或 SR-IOV 接口的微型端口驱动程序，此标志是必需的。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_VM_QUEUE_SUPPORTED</dt>
<dd><p>网络适配器提供支持 VM 队列数据包筛选的最低要求。 如果启用了此标志，则该标志必须设置为使用 VMQ 或 SR-IOV 接口。</p>
<p>有关 VM 队列数据包筛选的 VMQ 要求的详细信息，请参阅 <a href="/windows-hardware/drivers/network/setting-and-clearing-vmq-filters" data-raw-source="[Setting and Clearing VMQ Filters](./setting-and-clearing-vmq-filters.md)">设置和清除 Vmq 筛选器</a>。</p>
<p>有关 VM 队列数据包筛选的 SR-IOV 要求的详细信息，请参阅 <a href="/windows-hardware/drivers/network/setting-a-receive-filter-on-a-virtual-port" data-raw-source="[Setting a Receive Filter on a Virtual Port](./setting-a-receive-filter-on-a-virtual-port.md)">设置虚拟端口上的接收筛选器</a>。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_LOOKAHEAD_SPLIT_SUPPORTED</dt>
<dd><p>网络适配器支持 VM 队列，该队列在预测先行偏移量处拆分收到的传入数据包。 此偏移量等于或大于请求的预测先行大小。 网络适配器使用 DMA 将预测先行和后期预测数据传输到单独的共享内存段。</p>
<div class="alert">
<strong>注意</strong>   从 NDIS 6.30 开始，不再支持将数据包数据拆分为单独的预测先行缓冲区。 支持此版本的 NDIS 的微型端口驱动程序不能设置此标志。
</div>
<div>
 
</div>
</dd>
<dt>NDIS_RECEIVE_FILTER_DYNAMIC_PROCESSOR_AFFINITY_CHANGE_SUPPORTED</dt>
<dd><p>网络适配器支持动态更改以下处理器关联属性之一：</p>
<ul>
<li><p>VMQ 接口中 VM 队列的处理器关联。 处理器关联通过 <a href="/windows-hardware/drivers/network/oid-receive-filter-queue-parameters" data-raw-source="[OID_RECEIVE_FILTER_QUEUE_PARAMETERS](./oid-receive-filter-queue-parameters.md)">OID_RECEIVE_FILTER_QUEUE_PARAMETERS</a>的 OID 集请求进行更改。</p></li>
<li><p>非默认虚拟端口 (VPort) 的处理器关联，该端口是在 SR-IOV 接口中创建的，并附加到了 PCI Express (PCIe) 物理功能 (网络适配器的 "PF) "。 处理器关联通过 <a href="/windows-hardware/drivers/network/oid-nic-switch-vport-parameters" data-raw-source="[OID_NIC_SWITCH_VPORT_PARAMETERS](./oid-nic-switch-vport-parameters.md)">OID_NIC_SWITCH_VPORT_PARAMETERS</a>的 OID 集请求进行更改。</p></li>
</ul>
</dd>
<dt>NDIS_RECEIVE_FILTER_INTERRUPT_VECTOR_COALESCING_SUPPORTED</dt>
<dd><p>网络适配器在以下任何一种情况下都支持接收的数据包的中断合并：</p>
<ul>
<li><p>VMQ 接口中有多个 VM 队列。</p></li>
<li><p>与 SR-IOV 接口中的 PF 连接的多个 VPorts。</p></li>
</ul>
<p>如果设置此标志，网络适配器必须合并具有相同处理器关联的 VM 队列或 VPorts 的接收中断。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_IMPLAT_MIN_OF_QUEUES_MODE</dt>
<dd><p>表示可用的 VM 队列数是 (LBFO) 团队的负载平衡故障转移的任何成员中可用的最小队列数。 此标志仅适用于 LBFO 筛选器。 此标志未设置为微型端口。</p>
</dd>
<dt> NDIS_RECEIVE_FILTER_IMPLAT_SUM_OF_QUEUES_MODE</dt>
<dd><p>指示可用 VM 队列的数目是 LBFO 团队的每个成员中可用的所有队列的总和。 此标志仅适用于 LBFO 筛选器。 此标志未设置为微型端口。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_PACKET_COALESCING_SUPPORTED_ON_DEFAULT_QUEUE</dt>
<dd><p>网络适配器支持 NDIS 数据包合并。 数据包合并仅在网络适配器的默认接收队列中受支持。 此接收队列具有 NDIS_DEFAULT_RECEIVE_QUEUE_ID 的标识符。</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>支持的筛选器测试。 标志的按位 "或"，用于指定微型端口驱动程序支持的测试操作。 以下标志是有效的。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_TEST_HEADER_FIELD_EQUAL_SUPPORTED</dt>
<dd><p>网络适配器支持测试选定的标头字段，以确定它是否等于给定的值。</p>
<div class="alert">
<strong>注意</strong>   如果微型端口驱动程序支持 VMQ 或 SR-IOV 接口，则必须设置此标志。
</div>
<div>
 
</div>
</dd>
<dt>NDIS_RECEIVE_FILTER_TEST_HEADER_FIELD_MASK_EQUAL_SUPPORTED</dt>
<dd><p>网络适配器支持屏蔽 (即所选标头字段的按位 "与") ，以确定结果是否与指定的值相等。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_TEST_HEADER_FIELD_NOT_EQUAL_SUPPORTED</dt>
<dd><p>网络适配器支持测试选定的标头字段，以确定它是否不等于指定值。</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>支持的标头。 指定微型端口驱动程序可检查的网络数据包标头类型的按位 "或" 标志。 以下标志是有效的。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_SUPPORTED</dt>
<dd><p>网络适配器可以检查网络数据包 (MAC) 标头的媒体访问控制。 <strong>SupportedMacHeaderFields</strong>成员定义可以检查的 MAC 标头中的各个字段。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_ARP_HEADER_SUPPORTED</dt>
<dd><p>网络适配器可以检查网络数据包 (ARP) 标头的地址解析协议。 <strong>SupportedArpHeaderFields</strong>成员定义可以检查的 ARP 标头中的各个字段。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_IPV4_HEADER_SUPPORTED</dt>
<dd><p>网络适配器可以检查网络数据包 (IPv4) 标头的 IP 版本4。 <strong>SupportedIPv4HeaderFields</strong>成员定义可以检查的 IPv4 标头中的各个字段。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_IPV6_HEADER_SUPPORTED</dt>
<dd><p>网络适配器可以检查网络数据包的 IP 版本 6 (IPv6) 标头。 <strong>SupportedIPv6HeaderFields</strong>成员定义可以检查的 IPv6 标头中的各个字段。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_UDP_HEADER_SUPPORTED</dt>
<dd><p>网络适配器可以检查网络数据包 (UDP) 标头的用户数据报协议。 <strong>SupportedIPv6HeaderFields</strong>成员定义可以检查的 UDP 标头中的各个字段。</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>支持的 MAC 标头字段。 标志的按位 "或"，用于指定微型端口驱动程序可以检查的 MAC 标头字段的类型。 以下标志是有效的。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_DEST_ADDR_SUPPORTED</dt>
<dd><p>网络适配器支持基于 MAC 标头中的目标 MAC 地址进行检查和筛选。</p>
<div class="alert">
<strong>注意</strong>   从 NDIS 6.30 开始，支持 VMQ 或 SR-IOV 接口的微型端口驱动程序必须设置此标志。
</div>
<div>
 
</div>
</dd>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_SOURCE_ADDR_SUPPORTED</dt>
<dd><p>网络适配器支持基于 MAC 标头中的源 MAC 地址进行检查和筛选。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_PROTOCOL_SUPPORTED</dt>
<dd><p>网络适配器支持基于 MAC 标头中的 EtherType 标识符进行检查和筛选。 例如，IPv4 数据包的 EtherType 标识符为0x0800。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_VLAN_ID_SUPPORTED</dt>
<dd><p>网络适配器支持基于 MAC 标头中的 VLAN 标识符检查和筛选。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_PRIORITY_SUPPORTED</dt>
<dd><p>网络适配器支持基于 MAC 标头中的优先级标记进行检查和筛选。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_PACKET_TYPE_SUPPORTED</dt>
<dd><p>网络适配器支持基于 IEEE 802.2 子网访问协议的 "数据包类型" 字段的检查和筛选， (对齐 802.3 MAC 标头中的) 标头。</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>微型端口驱动程序支持的 MAC 标头筛选器的最大数目。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>最大队列组。 此值为保留值。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>每个队列组的最大队列数。 此值为保留值。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>网络适配器支持的预测先行包缓冲区的最小大小（以字节为单位）。
<div class="alert">
<strong>注意</strong>   从 NDIS 6.30 开始，不再支持将数据包数据拆分为单独的预测先行缓冲区。 支持此版本的 NDIS 的微型端口驱动程序必须将此成员设置为零。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>网络适配器支持的预测先行包缓冲区的最大大小（以字节为单位）。
<div class="alert">
<strong>注意</strong>   从 NDIS 6.30 开始，不再支持将数据包数据拆分为单独的预测先行缓冲区。 支持此版本的 NDIS 的微型端口驱动程序必须将此成员设置为零。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>支持的 ARP 标头字段。 标志的按位 "或"，用于指定微型端口驱动程序可以检查的 ARP 标头字段的类型。 以下标志是有效的。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_ARP_HEADER_OPERATION_SUPPORTED</dt>
<dd><p>网络适配器支持对 ARP 操作字段进行接收筛选。</p>
</dd>
<dt> NDIS_RECEIVE_FILTER_ARP_HEADER_SPA_SUPPORTED</dt>
<dd><p>网络适配器支持对 ARP 源协议地址 (SPA) "字段的接收筛选。</p>
</dd>
<dt> NDIS_RECEIVE_FILTER_ARP_HEADER_TPA_SUPPORTED</dt>
<dd><p>网络适配器支持对 ARP 目标协议地址的接收筛选 (TPA) 字段。</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>支持的 IPv4 标头字段。 标志的按位 "或"，用于指定微型端口驱动程序可以检查的 IPv4 标头字段的类型。 以下标志是有效的。
<p></p>
<dl>
<dt> NDIS_RECEIVE_FILTER_IPV4_HEADER_PROTOCOL_SUPPORTED</dt>
<dd><p>网络适配器支持对 IPv4 协议字段进行接收筛选。</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>支持的 IPv6 标头字段。 标志的按位 "或"，用于指定微型端口驱动程序可以检查的 IPv6 标头字段的类型。 以下标志是有效的。
<p></p>
<dl>
<dt> NDIS_RECEIVE_FILTER_IPV6_HEADER_PROTOCOL_SUPPORTED</dt>
<dd><p>网络适配器支持对 IPv6 协议字段进行接收筛选。</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>支持的 UDP 标头字段。 标志的按位 "或"，用于指定微型端口驱动程序可以检查的 IPv6 标头字段的类型。 以下标志是有效的。
<p></p>
<dl>
<dt> NDIS_RECEIVE_FILTER_UDP_HEADER_DEST_PORT_SUPPORTED</dt>
<dd><p>网络适配器支持对 UDP "目标端口" 字段进行接收筛选。</p>
<div class="alert">
<strong>注意</strong>   如果收到的 UDP 数据包包含 IPv4 选项或 IPv6 扩展标头，网络适配器可以自动删除接收的数据包，并将其视为未通过 UDP 筛选器测试。
</div>
<div>
 
</div>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>可为单个数据包合并筛选器指定的数据包标头字段上的最大测试数。 有关数据包合并的详细信息，请参阅 <a href="/windows-hardware/drivers/network/ndis-packet-coalescing" data-raw-source="[NDIS Packet Coalescing](./ndis-packet-coalescing.md)">NDIS 数据包合并</a>。
<div class="alert">
<strong>注意</strong>   支持数据包合并的网络适配器必须支持5个或更多可为单个数据包合并筛选器指定的数据包标头字段。 如果适配器不支持数据包合并，微型端口驱动程序必须将此值设置为零。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>网络适配器支持的数据包合并接收筛选器的最大数量。
<div class="alert">
<strong>注意</strong>   支持数据包合并的网络适配器必须支持10个或更多数据包合并筛选器。 如果适配器不支持数据包合并，微型端口驱动程序必须将此值设置为零。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)

