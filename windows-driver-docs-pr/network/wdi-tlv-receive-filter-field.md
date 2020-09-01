---
title: 'WDI_TLV_RECEIVE_FILTER_FIELD (0x65) '
description: WDI_TLV_RECEIVE_FILTER_FIELD 是一种 TLV，其中包含网络标头中的一个字段的接收筛选器测试条件。
ms.assetid: 9037CD08-742E-4A99-A37B-9969A2BC666A
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_RECEIVE_FILTER_FIELD (0x65) 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: afae0f0ddaee006ccabc023854a566f22f043aff
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214250"
---
# <a name="wdi_tlv_receive_filter_field-0x65"></a>WDI \_ TLV \_ 接收 \_ 筛选器 \_ 字段 (0x65) 


WDI \_ tlv \_ 接收 \_ 筛选器 \_ 字段是一个 tlv，其中包含网络标头中的一个字段的接收筛选器测试条件。

## <a name="tlv-type"></a>TLV 类型


0x65

## <a name="length"></a>Length


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
<td>指定标志的按位 "或"。 可能的标志值为 WDI_RECEIVE_FILTER_FIELD_MAC_HEADER_VLAN_UNTAGGED_OR_ZERO。 如果设置了此标志，则网络适配器只能指示已接收的数据包，这些数据包通过以下标准：
<ul>
<li>数据包的 MAC 地址与指定的 MAC 标头字段测试匹配。</li>
<li>数据包不包含 VLAN 标记，或者其 VLAN 标记的 ID 为零。</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_frame_header" data-raw-source="[&lt;strong&gt;NDIS_FRAME_HEADER&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_frame_header)"><strong>NDIS_FRAME_HEADER</strong></a> (UINT32) </td>
<td>框架标头。 指定框架标头的类型。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_receive_filter_test" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_TEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_receive_filter_test)"><strong>NDIS_RECEIVE_FILTER_TEST</strong></a> (UINT32) </td>
<td>接收筛选器测试。 指定接收筛选器执行的测试类型。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>标头字段。 按照 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_FIELD_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)"><strong>NDIS_RECEIVE_FILTER_FIELD_PARAMETERS</strong></a>中所述，按联合指定协议特定的标头字段类型。HeaderField.</td>
</tr>
<tr class="odd">
<td>UINT8 [16]</td>
<td>字段值。 指定微型端口适配器与传入数据包中相应标头字段值进行比较的值。 标头字段值的位置由 <em>标头字段</em> 元素中指定的字段类型决定。 此值以网络字节顺序排列，并按照 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_FIELD_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)"><strong>NDIS_RECEIVE_FILTER_FIELD_PARAMETERS</strong></a>中所述的联合进行指定。FieldValue.</td>
</tr>
<tr class="even">
<td>UINT8 [16]</td>
<td>测试结果值。 如果 " <em>接收筛选器测试</em> " 元素设置为 "ReceiveFilterTestMaskEqual"，则网络适配器将首先从 <em>字段值</em> 成员的值和 <em>标</em> 头字段成员指定的标头字段值计算结果。 然后，该适配器会将计算结果与 <em>结果值</em>进行比较。 此值与联合指定，如 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_FIELD_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)"><strong>NDIS_RECEIVE_FILTER_FIELD_PARAMETERS</strong></a>中所述。ResultValue.</td>
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

 

