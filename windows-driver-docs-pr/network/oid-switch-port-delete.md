---
title: OID_SWITCH_PORT_DELETE
description: HYPER-V 可扩展交换机的协议边缘发出一个对象标识符 (OID) 组请求的 OID_SWITCH_PORT_DELETE 以通知有关可扩展交换机端口删除可扩展交换机扩展。
ms.assetid: D8893395-3D33-4777-B8F0-4DD6BE9B8A37
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PORT_DELETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cda916bdb9c95e7acb57644df252bb49e81594fd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356106"
---
# <a name="oidswitchportdelete"></a>OID\_交换机\_端口\_删除


HYPER-V 可扩展交换机的协议边缘发出对象标识符 (OID) 组请求的 OID\_切换\_端口\_删除以通知有关可扩展交换机端口删除可扩展交换机扩展。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构。

<a name="remarks"></a>备注
-------

**PortId**的成员[ **NDIS\_切换\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构指定的可扩展交换机端口为其删除通知进行了。

如果网络适配器已连接到指定的端口，可扩展交换机的协议边缘将删除连接，然后再删除该端口。 在这种情况下，协议边缘将执行以下步骤，然后再删除该端口：

-   协议边缘颁发的 OID 集请求[OID\_切换\_NIC\_断开连接](oid-switch-nic-disconnect.md)通知正在之间的网络适配器和可扩展交换机端口的连接的扩展已删除。

-   所有挂起的指定可扩展交换机端口的数据包已取消或完成后，协议边缘颁发的 OID 集请求[OID\_切换\_NIC\_删除](oid-switch-nic-delete.md)通知扩展之间的网络适配器和可扩展交换机端口的连接已被删除。

    在此情况下，协议边缘可以开始删除该端口。

当删除可扩展交换机端口时，可扩展交换机的协议边缘遵循以下步骤：

1.  可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_端口\_拆卸](oid-switch-port-teardown.md)。 此 OID 请求通知基础可扩展交换机扩展有关的可扩展交换机端口的删除过程开始。

2.  协议边缘发出 OID 集请求的 OID\_切换\_端口\_可扩展交换机端口的所有 OID 请求已都完成后删除。

    **请注意**  像扩展之前已调用[ *ReferenceSwitchPort* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port)增加端口的引用计数器，它必须调用[ *DereferenceSwitchPort* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_dereference_switch_port)协议边缘问题之前[OID\_交换机\_NIC\_删除](oid-switch-nic-delete.md)请求。

     

扩展必须遵守以下原则处理 OID 设置请求的 OID\_交换机\_端口\_删除：

-   该扩展不能修改[ **NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)与 OID 请求关联的结构。

-   扩展始终将转发对基础扩展的 OID 集请求。 扩展必须不会使请求失败。

-   之后 OID\_交换机\_端口\_DELETE 请求已完成并且 NDIS\_状态\_成功后，该扩展将不会收到任何数据包或已删除的端口的 OID 请求。 该扩展不能将数据包转发到已删除的端口。 扩展还不能发出 OID 请求，也不调用[ *ReferenceSwitchPort* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port)函数已删除的端口。

**请注意**  可扩展交换机扩展必须发出 OID 集请求的 OID\_切换\_端口\_删除。

 

有关可扩展交换机端口和网络适配器连接的状态的详细信息，请参阅[HYPER-V 可扩展交换机端口和网络适配器状态](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础的微型端口边缘完成 OID 集请求的 OID\_切换\_端口\_删除并返回以下状态代码。

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
[*DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_dereference_switch_port)

[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)

[OID\_交换机\_NIC\_删除](oid-switch-nic-delete.md)

[OID\_交换机\_端口\_数组](oid-switch-port-array.md)

[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port)

 

 




