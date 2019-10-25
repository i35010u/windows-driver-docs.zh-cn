---
title: OID_SWITCH_PORT_ARRAY
description: Hyper-v 可扩展交换机扩展发出 OID_SWITCH_PORT_ARRAY 的对象标识符（OID）查询请求，以获取一个数组。 数组中的每个元素都指定可扩展交换机端口的配置参数。
ms.assetid: 9ED5E7A5-A23E-48E7-B8A2-9089C81851A1
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PORT_ARRAY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 62726f7a73eb82ccb946462f6343c73858830c47
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843940"
---
# <a name="oid_switch_port_array"></a>OID\_交换机\_端口\_数组


Hyper-v 可扩展交换机扩展发出 OID\_SWITCH\_端口\_数组的对象标识符（OID）查询请求，以获取一个数组。 数组中的每个元素都指定可扩展交换机端口的配置参数。

如果 OID 查询请求成功完成， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构中的**InformationBuffer**成员包含指向缓冲区的指针。 此缓冲区包含以下数据：

-   [**NDIS\_交换机\_端口\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_array)结构，用于定义数组中的元素数目。

-   [**NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构的数组。 其中每个结构都包含有关可扩展交换机上的端口的信息。

    **注意**  如果未在可扩展交换机上创建任何端口，驱动程序会将[**ndis\_switch\_端口\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_array)结构的**NumElements**成员设置为零，且不会[ **\_的 ndis\_返回端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构。

     

<a name="remarks"></a>备注
-------

仅当 Hyper-v 可扩展交换机完成激活时，才必须发出 OID\_SWITCH\_端口\_ARRAY OID。 有关更多详细信息，请参阅[查询 Hyper-v 可扩展交换机配置](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-hyper-v-extensible-switch-configuration)。

当扩展处理返回的[**ndis\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构时，它不能假定 NDIS\_交换机的各个字符串成员 **\_端口\_参数**结构，如as **portvalue**，以 null 结尾。 [**如果\_计数\_字符串**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-_if_counted_string_lh)结构，则这些字符串成员的数据类型由类型定义。 驱动程序必须根据此结构的**length**成员的值确定字符串长度。

**请注意**  如果字符串以 null 结尾，则**长度**成员不能包含终止 null 字符。

 

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘完成 OID\_SWITCH\_端口\_数组的 OID 查询请求，并返回以下状态代码之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>OID 请求已成功完成。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度太小，无法返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_array" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PORT_ARRAY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_array)"><strong>NDIS_SWITCH_PORT_ARRAY</strong></a>及其<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PORT_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)"><strong>NDIS_SWITCH_PORT_PARAMETERS</strong></a>元素数组。 可扩展交换机的基础微型端口边缘设置<strong>数据。QUERY_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的 BytesNeeded 成员到所需的最小缓冲区大小。</p></td>
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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_交换机\_端口\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_array)

[**NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)

[查询 Hyper-v 可扩展交换机配置](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-hyper-v-extensible-switch-configuration)

 

 




