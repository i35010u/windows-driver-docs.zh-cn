---
title: OID_SWITCH_PORT_ARRAY
description: Hyper-v 可扩展交换机扩展)  (OID 发出对象标识符，OID_SWITCH_PORT_ARRAY 获取数组的查询请求。 数组中的每个元素都指定可扩展交换机端口的配置参数。
ms.assetid: 9ED5E7A5-A23E-48E7-B8A2-9089C81851A1
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PORT_ARRAY 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9988770fbb683b47c9735daeee42416d3f82ccf8
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716984"
---
# <a name="oid_switch_port_array"></a>OID \_ 交换机 \_ 端口 \_ 数组


Hyper-v 可扩展交换机扩展)  (OID 发出对象标识符，请求 OID \_ 交换机 \_ 端口 \_ 数组以获取数组。 数组中的每个元素都指定可扩展交换机端口的配置参数。

如果 OID 查询请求成功完成， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向缓冲区的指针。 此缓冲区包含以下数据：

-   用于定义数组中的元素数的 [**NDIS \_ 交换机 \_ 端口 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_array) 结构。

-   [**NDIS \_ 交换机 \_ 端口 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构的数组。 其中每个结构都包含有关可扩展交换机上的端口的信息。

    **注意**   如果未在可扩展交换机上创建端口，则驱动程序会将[**ndis \_ 交换机 \_ 端口 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_array)结构的**NumElements**成员设置为零，且不会返回[**ndis \_ 交换机 \_ 端口 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构。

     

<a name="remarks"></a>备注
-------

\_ \_ \_ 仅当 hyper-v 可扩展交换机完成激活时才必须发出 oid 交换机端口数组 oid。 有关更多详细信息，请参阅 [查询 Hyper-v 可扩展交换机配置](./querying-the-hyper-v-extensible-switch-configuration.md) 。

当扩展处理返回的 [**ndis \_ 交换机 \_ 端口 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters) 结构时，它不能假定 **NDIS \_ 交换机 \_ 端口 \_ 参数** 结构的各个字符串成员（如 **portvalue**）以 null 值终止。 这些字符串成员的数据类型由 [**IF \_ 计数 \_ 字符串**](/windows/win32/api/ifdef/ns-ifdef-_if_counted_string_lh) 结构的类型定义。 驱动程序必须根据此结构的 **length** 成员的值确定字符串长度。

**注意**   如果字符串以 null 结尾，则**长度**成员不能包含终止 null 字符。

 

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘完成 OID 交换机端口数组的 OID 查询 \_ 请求 \_ \_ ，并返回以下状态代码之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>OID 请求已成功完成。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度太小，无法返回 <a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_array" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PORT_ARRAY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_array)"><strong>NDIS_SWITCH_PORT_ARRAY</strong></a> 及其 <a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PORT_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)"><strong>NDIS_SWITCH_PORT_PARAMETERS</strong></a> 元素数组。 可扩展交换机的基础微型端口边缘设置 <strong>数据。QUERY_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>由于其他原因，请求失败。</p></td>
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
<td><p>版本</p></td>
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ 交换机 \_ 端口 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_array)

[**NDIS \_ 交换机 \_ 端口 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)

[查询 Hyper-V 可扩展交换机配置](./querying-the-hyper-v-extensible-switch-configuration.md)

