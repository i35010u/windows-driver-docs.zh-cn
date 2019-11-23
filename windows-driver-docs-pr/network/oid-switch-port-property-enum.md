---
title: OID_SWITCH_PORT_PROPERTY_ENUM
description: Hyper-v 可扩展交换机扩展发出 OID_SWITCH_PORT_PROPERTY_ENUM 获取数组的对象标识符（OID）方法请求。
ms.assetid: 5C391B82-FCA6-4A95-992F-EDB5DF6183C7
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PORT_PROPERTY_ENUM 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 801b7a5116d7dad1280ba71368abc363da8f3e4e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843927"
---
# <a name="oid_switch_port_property_enum"></a>OID\_SWITCH\_端口\_属性\_枚举


Hyper-v 可扩展交换机扩展发出 OID\_SWITCH\_端口\_\_属性的对象标识符（OID）方法请求，以获取一个数组。 此数组包含与指定条件匹配的预配端口策略。 数组中的每个元素都为指定的可扩展交换机端口指定了策略的属性。

[ **\_OID 的 NDIS\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向缓冲区的指针。 此缓冲区包含以下数据：

-   [**NDIS\_交换机\_端口\_属性\_枚举\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_parameters)结构，该结构指定指定端口的策略枚举的参数。

-   一组[**NDIS\_交换机\_端口\_属性\_枚举\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_info)结构。 其中每个结构都包含有关可扩展交换机端口策略的属性的信息。

    **请注意**  如果 NDIS\_的**NumProperties**成员[**切换\_端口\_属性\_枚举\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_parameters)结构设置为零，则不[**NDIS\_交换机\_端口\_返回\_枚举\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_info)结构的属性。

     

<a name="remarks"></a>备注
-------

在发出 OID 的 OID 方法请求之前\_SWITCH\_端口\_属性\_枚举，可扩展交换机扩展必须遵循以下准则：

-   扩展只能在可扩展交换机的协议边缘发出[oid](oid-switch-port-create.md)时，\_交换机\_端口\_属性\_枚举请求，然后才会发出 oid\_switch\_\_请求，并在发出[oid\_交换机\_拆卸](oid-switch-port-teardown.md)请求之前。\_

-   扩展必须先调用[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port) ，然后才能调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)\_端口\_属性\_枚举请求来发出 OID\_。 这可确保在完成 OID 请求之前，不会删除指定的端口。

    完成 OID 请求后，扩展必须调用[*DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port)。 无论 OID 请求是否已完成，其 NDIS\_状态都\_成功，扩展必须调用此函数。

仅当 Hyper-v 可扩展交换机完成激活时，才必须发出 OID\_SWITCH\_端口\_属性\_枚举 OID。 有关更多详细信息，请参阅[查询 Hyper-v 可扩展交换机配置](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-hyper-v-extensible-switch-configuration)。

**请注意**  如果扩展接收 OID 的 oid 方法请求\_交换机\_端口\_属性\_枚举，则它不能完成 oid 请求。 相反，它必须调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)将 OID 请求向下转发到可扩展交换机驱动程序堆栈。

 

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘完成 OID\_SWITCH\_端口\_属性\_枚举的 OID 查询请求，并返回以下状态代码。

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
[*DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_交换机\_端口\_属性\_枚举\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_info)

[**NDIS\_交换机\_端口\_属性\_枚举\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[查询 Hyper-v 可扩展交换机配置](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-hyper-v-extensible-switch-configuration)

[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)

 

 




