---
title: OID_SWITCH_NIC_RESTORE
description: Hyper-v 可扩展交换机的协议边缘发出 OID_SWITCH_NIC_RESTORE 的对象标识符（OID）设置请求，通知可扩展交换机扩展关于可为可扩展交换机端口及其网络适配器还原的运行时数据连接.
ms.assetid: 252FB1D2-932F-4FB8-83D6-2690171D746D
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_RESTORE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 224a73a8433f4dbc84b34d9ed499678e429438e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843950"
---
# <a name="oid_switch_nic_restore"></a>OID\_交换机\_NIC\_还原


Hyper-v 可扩展交换机的协议边缘发出 OID\_SWITCH\_NIC 的对象标识符（OID）设置请求\_RESTORE，以通知可扩展交换机扩展有关可为可扩展交换机端口还原的运行时数据及其网络适配器连接。

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_SWITCH\_NIC 的指针\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构。 此结构由可扩展交换机的协议边缘分配。

<a name="remarks"></a>备注
-------

当它接收到 oid\_SWITCH\_NIC\_还原时，可扩展交换机扩展必须首先确定它是否拥有运行时数据。 此扩展通过比较[ **\_\_NIC 的 NDIS 交换机**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)的**ExtensionId**成员的值，\_将\_状态结构保存到扩展用于标识自身的 GUID 值。

如果扩展插件拥有可扩展交换机端口的运行时数据，则将按以下方式还原这些数据：

1.  该扩展将**SaveData**成员中的运行时数据复制到扩展分配的存储中。

    **请注意**  NDIS\_交换机的**PortId**成员的值[ **\_NIC\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构可能与保存运行时数据时的**PortId**值不同。 如果在实时迁移从一台主机到另一台主机时保存了运行时数据，则会发生这种情况。 但是，可扩展交换机端口的配置会在实时迁移时保留。 这使该扩展可以使用新的**PortId**值将运行时数据还原到可扩展交换机端口。

     

2.  扩展完成 OID 集请求，其 NDIS\_状态\_成功。

如果扩展不拥有指定的运行时数据，则扩展将调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)将此 OID 集请求转发到可扩展交换机驱动程序堆栈中的基础扩展。 在这种情况下，扩展不能修改[**NDIS\_交换机\_NIC\_保存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)与 OID 请求关联\_状态结构。

如果 OID\_交换机\_NIC\_还原集请求由可扩展交换机的微型端口边缘接收，则它将完成 OID 请求，并将 NDIS\_\_状态设置为 "成功"。 这会通知可扩展交换机的协议边缘，其中没有扩展拥有运行时数据。

有关如何还原运行时数据的详细信息，请参阅[还原 Hyper-v 可扩展交换机运行时数据](https://docs.microsoft.com/windows-hardware/drivers/network/restoring-hyper-v-extensible-switch-run-time-data)。

**请注意**  如果扩展无法进行 OID 设置请求，则可扩展交换机会使整个还原操作失败。 因此，在可能的情况下，扩展应避免在 OID 请求时失败。 例如，如果扩展无法分配还原运行时数据所需的资源，则在不还原运行时数据的情况下它无法正常工作的情况下，OID 请求应该会失败。 但是，如果扩展可以从失败条件中恢复，则不应使 OID 设置请求失败。

 

### <a name="return-status-codes"></a>返回状态代码

如果扩展\_NIC\_还原完成 oid\_切换请求，则将返回以下状态代码之一。

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
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
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

[**NDIS\_交换机\_NIC\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

 

 




