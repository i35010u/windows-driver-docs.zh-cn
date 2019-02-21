---
title: WDI_TLV_RECEIVE_FILTER_FIELD (0x65)
description: WDI_TLV_RECEIVE_FILTER_FIELD 是包含接收筛选器 TLV 网络标头中进行测试的一个字段的条件。
ms.assetid: 9037CD08-742E-4A99-A37B-9969A2BC666A
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_RECEIVE_FILTER_FIELD (0x65) 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5f49ff68eb1b443af8793f826e96b24fc39892d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545490"
---
# <a name="wditlvreceivefilterfield-0x65"></a>WDI\_TLV\_RECEIVE\_FILTER\_FIELD (0x65)


WDI\_TLV\_接收\_筛选器\_字段是包含网络标头中的一个字段的接收筛选器测试条件 TLV。

## <a name="tlv-type"></a>TLV 类型


0x65

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
<td>指定标志的按位 OR。 可能的标志值为 WDI_RECEIVE_FILTER_FIELD_MAC_HEADER_VLAN_UNTAGGED_OR_ZERO。 如果设置此标志，网络适配器必须仅指示满足以下条件的接受的数据包：
<ul>
<li>数据包&#39;的 MAC 地址与指定的 MAC 标头字段测试相匹配。</li>
<li>数据包不包含的 VLAN 标记，或一个 VLAN 标记具有 ID 为 0。</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff565581" data-raw-source="[&lt;strong&gt;NDIS_FRAME_HEADER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565581)"><strong>NDIS_FRAME_HEADER</strong></a> (UINT32)</td>
<td>框架标头。 指定框架标头的类型。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff567183" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_TEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567183)"><strong>NDIS_RECEIVE_FILTER_TEST</strong></a> (UINT32)</td>
<td>收到筛选测试。 指定接收筛选器执行的测试的类型。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>标头字段。 与联合中指定的特定于协议的标头字段类型，如中所述<a href="https://msdn.microsoft.com/library/windows/hardware/ff567169" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_FIELD_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567169)"> <strong>NDIS_RECEIVE_FILTER_FIELD_PARAMETERS</strong></a>。HeaderField。</td>
</tr>
<tr class="odd">
<td>UINT8[16]</td>
<td>字段值。 指定的微型端口适配器将与传入的数据包中的相应标头字段值进行比较的值。 标头字段值的位置由中指定的字段类型<em>标头字段</em>元素。 此值是以网络字节顺序，如中所述，使用联合指定<a href="https://msdn.microsoft.com/library/windows/hardware/ff567169" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_FIELD_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567169)"> <strong>NDIS_RECEIVE_FILTER_FIELD_PARAMETERS</strong></a>。FieldValue。</td>
</tr>
<tr class="even">
<td>UINT8[16]</td>
<td>测试结果值。 如果<em>接收筛选器测试</em>元素设置为 ReceiveFilterTestMaskEqual、 网络适配器首先计算中的值的结果<em>字段值</em>成员和标头字段与指定的值通过<em>标头字段</em>成员。 然后，适配器会比较计算的结果与<em>导致值</em>。 如中所述，指定此值与联合<a href="https://msdn.microsoft.com/library/windows/hardware/ff567169" data-raw-source="[&lt;strong&gt;NDIS_RECEIVE_FILTER_FIELD_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567169)"> <strong>NDIS_RECEIVE_FILTER_FIELD_PARAMETERS</strong></a>。ResultValue。</td>
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

 

 




