---
title: OID_SWITCH_PORT_PROPERTY_DELETE
description: Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 OID_SWITCH_PORT_PROPERTY_DELETE 请求，通知有关如何删除可扩展交换机端口的策略属性的可扩展交换机扩展。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PORT_PROPERTY_DELETE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 71445d72bf4ad8fc88350a65eea784bb38bff7fe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805181"
---
# <a name="oid_switch_port_property_delete"></a>OID \_ 交换机 \_ 端口 \_ 属性 \_ 删除


Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 OID \_ 交换机 \_ 端口 \_ 属性 " \_ 删除"，通知有关为可扩展交换机端口删除策略属性的可扩展交换机扩展。

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含一个指向缓冲区的指针，该缓冲区包含 [**NDIS \_ 交换机 \_ 端口 \_ 属性 \_ 删除 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_delete_parameters)结构。

<a name="remarks"></a>备注
-------

转发扩展可以处理 OID \_ 交换机 \_ 端口 \_ 属性删除的 oid 设置请求 \_ 。 所有其他类型的扩展都必须调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) ，将 OID 请求转发到可扩展交换机驱动程序堆栈中的下一个扩展。

有关如何处理 OID 交换机端口属性删除的 OID 集请求的指南 \_ \_ \_ \_ ，请参阅 [管理端口策略](./managing-port-policies.md)。

### <a name="return-status-codes"></a>返回状态代码

如果转发扩展插件完成 oid \_ 交换机端口属性删除的 oid 设置请求 \_ \_ \_ ，它将返回以下状态代码之一。

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
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>转发扩展不支持端口策略。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>由于其他原因，OID 请求失败。</p></td>
</tr>
</tbody>
</table>

 

如果转发扩展未完成 oid \_ 交换机端口属性删除的 oid 设置请求 \_ \_ \_ ，则该请求将由可扩展交换机的基础微型端口边缘完成。 微型端口边缘返回以下状态代码。

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

[**NDIS \_ 交换机 \_ 端口 \_ 属性 \_ 自定义**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_custom)

[**NDIS \_ 交换机 \_ 端口 \_ 属性 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)

[**NDIS \_ 交换机 \_ 端口 \_ 属性 \_ VLAN**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_vlan)

[**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

 

