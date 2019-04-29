---
title: WDI_TLV_RECEIVE_COALESCING_CAPABILITIES
description: WDI_TLV_RECEIVE_COALESCING_CAPABILITIES 是包含硬件辅助 TLV 接收筛选器功能。
ms.assetid: 87BC1F55-90C6-4B22-9E8E-A54FF42515F3
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_RECEIVE_COALESCING_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c7d1434689d85916a941568db6b644998891b623
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360178"
---
# <a name="wditlvreceivecoalescingcapabilities"></a>WDI\_TLV\_接收\_COALESCING\_功能


WDI\_TLV\_接收\_COALESCING\_功能是包含硬件辅助 TLV 接收筛选器功能。

## <a name="tlv-type"></a>TLV 类型


0x9A

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>在任务栏的搜索框中键入</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT32</td>
<td>启用筛选器类型。 位或运算的标志，用于指定启用的接收筛选器的类型。 以下标志是有效的。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_VMQ_FILTERS_ENABLED</dt>
<dd><p>指定启用 VMQ 筛选器。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_PACKET_COALESCING_FILTERS_ENABLED</dt>
<dd><p>指定 NDIS 数据包合并接收筛选器启用。</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>已启用的队列类型。 位或运算的标志，用于指定启用的接收队列的类型。 以下标志是有效的。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_VM_QUEUES_ENABLED</dt>
<dd><p>指定启用了虚拟机 (VM) 队列。 使用微型端口驱动程序启用要使用 VMQ 接口时，VM 队列。</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>网络适配器支持的虚拟机队列数。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>受支持的虚拟机队列属性。 指定的网络适配器支持的虚拟机队列属性的标志的按位 OR。 以下标志是有效的。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_MSI_X_SUPPORTED</dt>
<dd><p>网络适配器分配每个接收队列的 MSI X 表条目。 为多个接收队列，网络适配器必须使用一个 MSI X 表条目。 此标志是必需的微型端口驱动程序支持 VMQ 或 SR-IOV 接口。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_VM_QUEUE_SUPPORTED</dt>
<dd><p>网络适配器提供了支持虚拟机队列数据包筛选的最低要求。 如果已启用要使用 VMQ 或 SR-IOV 接口，微型端口驱动程序必须设置此标志。</p>
<p>有关 VM 队列数据包筛选 VMQ 要求的详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff570780" data-raw-source="[Setting and Clearing VMQ Filters](https://msdn.microsoft.com/library/windows/hardware/ff570780)">设置和清除 VMQ 筛选器</a>。</p>
<p>有关 SR-IOV 的虚拟机队列数据包筛选要求的详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh440224" data-raw-source="[Setting a Receive Filter on a Virtual Port](https://msdn.microsoft.com/library/windows/hardware/hh440224)">上虚拟端口设置接收的筛选器</a>。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_LOOKAHEAD_SPLIT_SUPPORTED</dt>
<dd><p>网络适配器支持拆分预测先行的偏移量处接收到传入数据包的虚拟机队列。 此偏移量为等于或大于请求的预期大小。 网络适配器使用 DMA 预测先行和 post 预测先行将数据传输到单独的共享的内存段。</p>
<div class="alert">
<strong>请注意</strong>  从 NDIS 6.30 开始，将数据包数据拆分为单独的预测先行缓冲区不再受支持。 支持此版本的 NDIS 的微型端口驱动程序必须不设置此标志。
</div>
<div>
 
</div>
</dd>
<dt>NDIS_RECEIVE_FILTER_DYNAMIC_PROCESSOR_AFFINITY_CHANGE_SUPPORTED</dt>
<dd><p>网络适配器，可将动态更改以下处理器关联属性之一：</p>
<ul>
<li><p>处理器关联的 VMQ 接口中的虚拟机队列。 通过 OID 集请求的更改处理器关联<a href="https://msdn.microsoft.com/library/windows/hardware/ff569794" data-raw-source="[OID_RECEIVE_FILTER_QUEUE_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff569794)">OID_RECEIVE_FILTER_QUEUE_PARAMETERS</a>。</p></li>
<li><p>处理器关联的非默认虚拟端口 (VPort) 的 SR-IOV 界面中创建并附加到 PCI Express (PCIe) 物理 (PF) 网络适配器的功能。 通过 OID 集请求的更改处理器关联<a href="https://msdn.microsoft.com/library/windows/hardware/hh451825" data-raw-source="[OID_NIC_SWITCH_VPORT_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/hh451825)">OID_NIC_SWITCH_VPORT_PARAMETERS</a>。</p></li>
</ul>
</dd>
<dt>NDIS_RECEIVE_FILTER_INTERRUPT_VECTOR_COALESCING_SUPPORTED</dt>
<dd><p>网络适配器支持收到的数据包上的以下任何合并的中断：</p>
<ul>
<li><p>VMQ 界面中的多个虚拟机队列。</p></li>
<li><p>附加到 PF SR-IOV 界面中的多个 VPorts。</p></li>
</ul>
<p>如果设置此标志，必须合并的网络适配器接收的虚拟机队列或具有相同的处理器关联的 VPorts 中断。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_IMPLAT_MIN_OF_QUEUES_MODE</dt>
<dd><p>指示 VM 可用的队列数是从负载平衡故障转移 (LBFO) 团队的任何成员可用的队列的最小数目。 此标志适用于 LBFO 筛选器。 微型端口未设置此标志。</p>
</dd>
<dt> NDIS_RECEIVE_FILTER_IMPLAT_SUM_OF_QUEUES_MODE</dt>
<dd><p>指示 VM 可用的队列数是可从 LBFO 团队的每个成员的所有队列的总和。 此标志适用于 LBFO 筛选器。 微型端口未设置此标志。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_PACKET_COALESCING_SUPPORTED_ON_DEFAULT_QUEUE</dt>
<dd><p>网络适配器支持 NDIS 数据包合并。 在默认仅支持数据包合并接收的网络适配器的队列。 此接收队列具有 NDIS_DEFAULT_RECEIVE_QUEUE_ID 的标识符。</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>支持筛选器的测试。 指定微型端口驱动程序支持的测试操作的标志的按位 OR。 以下标志是有效的。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_TEST_HEADER_FIELD_EQUAL_SUPPORTED</dt>
<dd><p>网络适配器支持测试选定的标头字段，以确定它是否等于给定的值。</p>
<div class="alert">
<strong>请注意</strong>  如果微型端口驱动程序支持 VMQ 或 SR-IOV 接口，它必须设置此标志。
</div>
<div>
 
</div>
</dd>
<dt>NDIS_RECEIVE_FILTER_TEST_HEADER_FIELD_MASK_EQUAL_SUPPORTED</dt>
<dd><p>网络适配器支持屏蔽 （即，按位与） 的所选标头字段，以确定结果是否等于指定的值。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_TEST_HEADER_FIELD_NOT_EQUAL_SUPPORTED</dt>
<dd><p>网络适配器支持测试选定的标头字段，以确定是否不等于指定的值。</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>受支持的标头。 指定的网络数据包标头的微型端口驱动程序可以检查类型的标志的位或运算。 以下标志是有效的。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_SUPPORTED</dt>
<dd><p>网络适配器可以检查网络数据包的介质访问控制 (MAC) 标头。 <strong>SupportedMacHeaderFields</strong>成员定义从 MAC 标头可检查各个字段。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_ARP_HEADER_SUPPORTED</dt>
<dd><p>网络适配器可以检查网络数据包的地址解析协议 (ARP) 标头。 <strong>SupportedArpHeaderFields</strong>成员定义从 ARP 标头可检查各个字段。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_IPV4_HEADER_SUPPORTED</dt>
<dd><p>网络适配器可以检查 IP 版本 4 (IPv4) 的网络数据包标头。 <strong>SupportedIPv4HeaderFields</strong>成员定义从 IPv4 标头可检查各个字段。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_IPV6_HEADER_SUPPORTED</dt>
<dd><p>网络适配器可以检查 IP 版本 6 (IPv6) 的网络数据包标头。 <strong>SupportedIPv6HeaderFields</strong>成员定义从 IPv6 标头可检查各个字段。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_UDP_HEADER_SUPPORTED</dt>
<dd><p>网络适配器可以检查网络数据包的用户数据报协议 (UDP) 标头。 <strong>SupportedIPv6HeaderFields</strong>成员定义从 UDP 标头可检查各个字段。</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>支持的 MAC 标头字段。 位或运算的标志，用于指定可以检查微型端口驱动程序的 MAC 标头字段的类型。 以下标志是有效的。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_DEST_ADDR_SUPPORTED</dt>
<dd><p>检查和筛选的网络适配器支持基于目标 MAC 标头中的 MAC 地址。</p>
<div class="alert">
<strong>请注意</strong>  从 NDIS 6.30 开始，支持 VMQ 或 SR-IOV 接口的微型端口驱动程序必须设置此标志。
</div>
<div>
 
</div>
</dd>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_SOURCE_ADDR_SUPPORTED</dt>
<dd><p>网络适配器支持检查并筛选基于的源 MAC 标头中的 MAC 地址。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_PROTOCOL_SUPPORTED</dt>
<dd><p>网络适配器支持检查并筛选基于 MAC 标头中的以太网类型标识符。 例如，IPv4 数据包的 EtherType 标识符是 0x0800。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_VLAN_ID_SUPPORTED</dt>
<dd><p>网络适配器支持检查并筛选基于 MAC 标头中的 VLAN 标识符。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_PRIORITY_SUPPORTED</dt>
<dd><p>网络适配器支持检查并筛选基于 MAC 标头中的优先级标记。</p>
</dd>
<dt>NDIS_RECEIVE_FILTER_MAC_HEADER_PACKET_TYPE_SUPPORTED</dt>
<dd><p>网络适配器支持检查和筛选的基于 IEEE 802.2 子网访问协议的数据包类型字段 （对齐） 标头 802.3 MAC 标头中。</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>MAC 标头筛选器的微型端口驱动程序支持的最大数目。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>最大队列组。 保留此值。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>每个队列组的最大队列。 保留此值。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>最小的大小，以字节为单位，预测先行数据包缓冲区为支持的网络适配器。
<div class="alert">
<strong>请注意</strong>  从 NDIS 6.30 开始，将数据包数据拆分为单独的预测先行缓冲区不再受支持。 支持此版本的 NDIS 的微型端口驱动程序必须将此成员设置为零。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>最大大小，以字节为单位，预测先行数据包缓冲区为支持的网络适配器。
<div class="alert">
<strong>请注意</strong>  从 NDIS 6.30 开始，将数据包数据拆分为单独的预测先行缓冲区不再受支持。 支持此版本的 NDIS 的微型端口驱动程序必须将此成员设置为零。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>受支持的 ARP 标头字段。 位或运算的标志，用于指定类型的微型端口驱动程序可以检查的 ARP 标头字段。 以下标志是有效的。
<p></p>
<dl>
<dt>NDIS_RECEIVE_FILTER_ARP_HEADER_OPERATION_SUPPORTED</dt>
<dd><p>网络适配器支持接收对 ARP 操作字段进行筛选。</p>
</dd>
<dt> NDIS_RECEIVE_FILTER_ARP_HEADER_SPA_SUPPORTED</dt>
<dd><p>网络适配器支持接收对 ARP 源协议地址 (SPA) 字段进行筛选。</p>
</dd>
<dt> NDIS_RECEIVE_FILTER_ARP_HEADER_TPA_SUPPORTED</dt>
<dd><p>网络适配器支持接收对 ARP 目标协议 (TPA) 地址字段进行筛选。</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>支持的 IPv4 标头字段。 位或运算的标志，用于指定 IPv4 标头字段的微型端口驱动程序可以检查的类型。 以下标志是有效的。
<p></p>
<dl>
<dt> NDIS_RECEIVE_FILTER_IPV4_HEADER_PROTOCOL_SUPPORTED</dt>
<dd><p>网络适配器支持接收对 IPv4 协议字段进行筛选。</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>支持的 IPv6 标头字段。 位或运算的标志，用于指定类型的微型端口驱动程序可以检查的 IPv6 标头字段。 以下标志是有效的。
<p></p>
<dl>
<dt> NDIS_RECEIVE_FILTER_IPV6_HEADER_PROTOCOL_SUPPORTED</dt>
<dd><p>网络适配器支持接收对 IPv6 协议字段进行筛选。</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>支持的 UDP 标头字段。 位或运算的标志，用于指定类型的微型端口驱动程序可以检查的 IPv6 标头字段。 以下标志是有效的。
<p></p>
<dl>
<dt> NDIS_RECEIVE_FILTER_UDP_HEADER_DEST_PORT_SUPPORTED</dt>
<dd><p>网络适配器支持接收针对 UDP 目标端口字段进行筛选。</p>
<div class="alert">
<strong>请注意</strong>  接收的 UDP 数据包中包含 IPv4 选项或 IPv6 扩展标头，如果网络适配器可以自动删除所接收的数据包并将它视为像 UDP 筛选器测试失败。
</div>
<div>
 
</div>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>最大数据包标头字段，可以指定单个数据包合并筛选器的测试数。 有关数据包合并的详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh451601" data-raw-source="[NDIS Packet Coalescing](https://msdn.microsoft.com/library/windows/hardware/hh451601)">NDIS 数据包合并</a>。
<div class="alert">
<strong>请注意</strong>  支持数据包合并的网络适配器必须支持为单个数据包合并筛选器可以指定的五个或多个数据包标头字段。 如果适配器不支持合并的数据包，微型端口驱动程序必须将此值设置为零。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>最大数据包合并接收的网络适配器支持的筛选器。
<div class="alert">
<strong>请注意</strong>  支持数据包合并的网络适配器必须支持 10 个或多个数据包合并筛选器。 如果适配器不支持合并的数据包，微型端口驱动程序必须将此值设置为零。
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
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_RECEIVE\_FILTER\_CAPABILITIES**](https://msdn.microsoft.com/library/windows/hardware/ff566864)

 

 




