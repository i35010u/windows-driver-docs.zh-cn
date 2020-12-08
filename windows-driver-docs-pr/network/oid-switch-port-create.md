---
title: OID_SWITCH_PORT_CREATE
description: Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 OID_SWITCH_PORT_CREATE 请求，通知有关创建可扩展交换机端口的可扩展交换机扩展。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PORT_CREATE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 87f325973b30342ee587dbcb25aa907725bdf5fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805195"
---
# <a name="oid_switch_port_create"></a>OID \_ 交换机 \_ 端口 \_ 创建


Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 OID \_ 交换机 \_ 端口创建的请求 \_ ，通知有关创建可扩展交换机端口的可扩展交换机扩展。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ 交换机 \_ 端口 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构的指针。

<a name="remarks"></a>备注
-------

[**NDIS \_ 交换机 \_ 端口 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构的 **PortId** 成员指定为其进行创建通知的端口。

可扩展交换机扩展必须遵循以下指导原则来处理 oid \_ 交换机端口 CREATE 的 oid 集请求 \_ \_ ：

-   扩展不得修改与 OID 请求关联的 [**NDIS \_ 交换机 \_ 端口 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters) 结构。

-   此扩展可以通过返回 \_ \_ \_ OID 请求不接受的 NDIS 状态数据来否决创建通知 \_ 。 例如，如果扩展无法分配资源来强制在端口上配置策略，则驱动程序应否决创建通知。

    如果扩展返回其他 NDIS \_ 状态 \_ *Xxx* 错误状态代码，则创建通知也被否决。 然而，为暂时性方案返回状态代码（例如返回 NDIS \_ 状态 \_ 资源）可能会导致创建通知重试。

    如果扩展不否决 OID 请求，则应在请求完成时监视状态。 扩展应执行此操作，以确定可扩展交换机控制路径中的基础扩展或可扩展交换机接口是否否决了 OID 请求。

    有关端口策略的详细信息，请参阅 [管理 Hyper-v 可扩展交换机策略](./managing-hyper-v-extensible-switch-extensibility-policies.md)。

-   如果扩展调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) 来转发此 oid 集请求，则扩展应监视此 oid 请求的完成状态。 此扩展用于检测可扩展交换机驱动程序堆栈中的基础扩展是否否决了端口创建通知。

-   在转发 OID 请求并成功完成后，扩展可以为端口发出 Oid 请求，如 [oid \_ 交换机 \_ 端口 \_ 属性 \_ 枚举](oid-switch-port-property-enum.md)，直到发出 [oid \_ 交换机 \_ 端口 \_ 拆卸](oid-switch-port-teardown.md) 的 oid 请求为止。 此 OID 请求通知扩展端口将从可扩展交换机开始删除过程。

-   扩展无法将数据包转发到 [**NDIS \_ 交换机 \_ 端口 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters) 结构中的指定端口，直到已发出 OID [ \_ 交换机 \_ NIC \_ CONNECT](oid-switch-nic-connect.md) 的 oid 请求并成功完成。

**注意**  扩展不得发出 oid 设置 OID \_ 交换机 \_ 端口 \_ 创建请求。

 

有关可扩展交换机端口和网络适配器连接状态的详细信息，请参阅 [Hyper-v 可扩展交换机端口和网络适配器状态](./hyper-v-extensible-switch-port-and-network-adapter-states.md)。

### <a name="return-status-codes"></a>返回状态代码

如果扩展已完成 oid \_ 交换机端口创建的 oid 设置 \_ 请求 \_ ，它将返回以下状态代码之一。

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

 

**注意**  如果扩展完成了 OID 设置请求，则它不能返回 NDIS \_ 状态 " \_ 成功"。

 

如果扩展未完成 oid 交换机端口创建的 OID 集请求 \_ \_ \_ ，则该请求将由可扩展交换机的基础微型端口边缘完成。 基础微型端口边缘返回此 OID 集请求的以下状态代码。

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

[**NDIS \_ 交换机 \_ 端口 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)

[**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[OID \_ 交换机 \_ NIC \_ 连接](oid-switch-nic-connect.md)

[OID \_ 交换机 \_ 端口 \_ 数组](oid-switch-port-array.md)

[OID \_ 交换机 \_ 端口 \_ 属性 \_ 枚举](oid-switch-port-property-enum.md)

 

