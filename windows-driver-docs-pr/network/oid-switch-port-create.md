---
title: OID_SWITCH_PORT_CREATE
description: HYPER-V 可扩展交换机的协议边缘发出一个对象标识符 (OID) 组请求的 OID_SWITCH_PORT_CREATE 以通知有关的可扩展交换机端口创建可扩展的交换机扩展。
ms.assetid: 579D51CD-0594-4A06-998E-3886E7325D97
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PORT_CREATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 60ecb89e17e9df2bb7fa39a1cf0256c1cc795b81
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356110"
---
# <a name="oidswitchportcreate"></a>OID\_交换机\_端口\_创建


HYPER-V 可扩展交换机的协议边缘发出对象标识符 (OID) 组请求的 OID\_切换\_端口\_创建，以通知有关的可扩展交换机端口创建可扩展的交换机扩展。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构。

<a name="remarks"></a>备注
-------

**PortId**的成员[ **NDIS\_开关\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构为其指定的端口创建通知进行了。

可扩展的交换机扩展必须遵守以下原则处理 OID 设置请求的 OID\_切换\_端口\_创建：

-   该扩展不能修改[ **NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)与 OID 请求关联的结构。

-   扩展有权创建通知决策通过返回 NDIS\_状态\_数据\_不\_OID 请求被接受。 例如，如果扩展不能分配资源，以强制实施其配置的端口上的策略，该驱动程序应能阻止创建通知。

    如果扩展插件可以返回其他 NDIS\_状态\_*Xxx*还禁止错误状态代码，创建通知。 但是，返回状态代码为暂时性的情况下，如返回 NDIS\_状态\_资源，可能会导致创建通知的重试。

    如果扩展不能阻止 OID 请求，它在请求完成时应监视的状态。 该扩展应这样做可以确定 OID 请求已被否决的可扩展交换机控制路径中的基础扩展或可扩展交换机接口。

    端口策略的详细信息，请参阅[管理的 HYPER-V 可扩展交换机策略](https://docs.microsoft.com/windows-hardware/drivers/network/managing-hyper-v-extensible-switch-extensibility-policies)。

-   如果扩展将调用[ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)转发此 OID 集请求，该扩展应监视此 OID 请求的完成状态。 扩展执行此检测中可扩展交换机驱动程序堆栈的基础扩展是否已被否决端口创建通知操作。

-   OID 请求被转发和成功完成后，该扩展可以 Oid 的发出请求端口，如[OID\_交换机\_端口\_属性\_枚举](oid-switch-port-property-enum.md)，直到OID 的请求[OID\_交换机\_端口\_拆卸](oid-switch-port-teardown.md)发出。 此 OID 请求向扩展通知端口将开始删除过程从可扩展的交换机。

-   扩展不能将数据包转发到在指定的端口[ **NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构，直到 OID 设置请求[OID\_交换机\_NIC\_CONNECT](oid-switch-nic-connect.md)发出和已成功完成。

**请注意**  扩展插件必须发出 OID 集请求的 OID\_交换机\_端口\_创建。

 

有关可扩展交换机端口和网络适配器连接的状态的详细信息，请参阅[HYPER-V 可扩展交换机端口和网络适配器状态](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)。

### <a name="return-status-codes"></a>返回状态代码

如果该扩展完成 OID 集请求的 OID\_交换机\_端口\_创建，它返回一个下面的状态代码。

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
<td><p>扩展操作禁止创建通知。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_RESOURCES</p></td>
<td><p>该扩展被否决由于资源不足的情况创建通知。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>扩展操作由于其他原因禁止创建通知。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  如果扩展完成 OID 集请求，它必须返回 NDIS\_状态\_成功。

 

如果扩展不会完成 OID 集请求的 OID\_切换\_端口\_可扩展交换机基础的微型端口边缘完成创建，该请求。 基础的微型端口边缘返回此 OID 集请求的以下状态代码。

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
<td><p>Version</p></td>
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)

[OID\_交换机\_NIC\_连接](oid-switch-nic-connect.md)

[OID\_交换机\_端口\_数组](oid-switch-port-array.md)

[OID\_SWITCH\_PORT\_PROPERTY\_ENUM](oid-switch-port-property-enum.md)

 

 




