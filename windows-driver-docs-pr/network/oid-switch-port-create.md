---
title: OID_SWITCH_PORT_CREATE
description: Hyper-v 可扩展交换机的协议边缘发出 OID_SWITCH_PORT_CREATE 的对象标识符（OID）设置请求，通知有关创建可扩展交换机端口的可扩展交换机扩展。
ms.assetid: 579D51CD-0594-4A06-998E-3886E7325D97
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PORT_CREATE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4c72c4e09af8f2bc6aa2de2319a69fa111cd9d13
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843938"
---
# <a name="oid_switch_port_create"></a>OID\_交换机\_端口\_创建


Hyper-v 可扩展交换机的协议边缘发出一个对象标识符（OID）设置 OID\_SWITCH\_端口\_CREATE，以通知有关创建可扩展交换机端口的可扩展交换机扩展。

[ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_SWITCH\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构的指针。

<a name="remarks"></a>备注
-------

[**NDIS\_SWITCH\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构中的**PortId**成员指定了创建通知所针对的端口。

可扩展交换机扩展必须遵循以下准则，以便处理 OID\_SWITCH\_端口\_创建：

-   扩展不能修改与 OID 请求关联的[**NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构。

-   扩展可以通过将 NDIS\_状态返回\_数据\_未\_为 OID 请求接受，来否决创建通知。 例如，如果扩展无法分配资源来强制在端口上配置策略，则驱动程序应否决创建通知。

    如果扩展返回的其他 NDIS\_状态\_*Xxx*错误状态代码，则创建通知也被否决。 然而，为暂时性方案返回状态代码（如将 NDIS\_状态返回\_资源）可能会导致创建通知重试。

    如果扩展不否决 OID 请求，则应在请求完成时监视状态。 扩展应执行此操作，以确定可扩展交换机控制路径中的基础扩展或可扩展交换机接口是否否决了 OID 请求。

    有关端口策略的详细信息，请参阅[管理 Hyper-v 可扩展交换机策略](https://docs.microsoft.com/windows-hardware/drivers/network/managing-hyper-v-extensible-switch-extensibility-policies)。

-   如果扩展调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)来转发此 oid 集请求，则扩展应监视此 oid 请求的完成状态。 此扩展用于检测可扩展交换机驱动程序堆栈中的基础扩展是否否决了端口创建通知。

-   在转发 OID 请求并成功完成后，扩展可以为端口发出 Oid 请求，如[oid\_交换机\_端口\_属性\_枚举](oid-switch-port-property-enum.md)，直到 oid 请求，\_[端口\_拆卸](oid-switch-port-teardown.md)。\_ 此 OID 请求通知扩展端口将从可扩展交换机开始删除过程。

-   扩展不能将数据包转发到[**NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构中的指定端口，直到 OID 参数结构的 OID [\_交换机\_NIC\_CONNECT](oid-switch-nic-connect.md)发出并成功完成。

**请注意**  扩展不能\_SWITCH\_端口\_CREATE 中发出 oid set 请求。

 

有关可扩展交换机端口和网络适配器连接状态的详细信息，请参阅[Hyper-v 可扩展交换机端口和网络适配器状态](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)。

### <a name="return-status-codes"></a>返回状态代码

如果扩展完成 oid\_SWITCH\_端口\_CREATE 的 OID 设置请求，它将返回以下状态代码之一。

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
<td><p>NDIS_STATUS_DATA_NOT_ACCEPTED</p></td>
<td><p>该扩展否决了创建通知。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_RESOURCES</p></td>
<td><p>由于资源不足，扩展拒绝了创建通知。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>由于其他原因，扩展拒绝了创建通知。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  扩展是否完成了 OID 设置请求，则不能\_SUCCESS 返回 NDIS\_状态。

 

如果扩展未完成 OID\_SWITCH\_端口\_创建的 OID 集请求，则该请求将由可扩展交换机的基础微型端口边缘完成。 基础微型端口边缘返回此 OID 集请求的以下状态代码。

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
[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[OID\_交换机\_NIC\_连接](oid-switch-nic-connect.md)

[OID\_交换机\_端口\_数组](oid-switch-port-array.md)

[OID\_SWITCH\_端口\_属性\_枚举](oid-switch-port-property-enum.md)

 

 




