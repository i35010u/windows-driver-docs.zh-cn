---
title: OID_SWITCH_PORT_PROPERTY_DELETE
description: Hyper-v 可扩展交换机的协议边缘发出 OID_SWITCH_PORT_PROPERTY_DELETE 的对象标识符（OID）设置请求，通知有关为可扩展交换机端口删除策略属性的可扩展交换机扩展。
ms.assetid: BA8AB5D9-FF2C-4E16-B09F-B09E3EC19B90
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PORT_PROPERTY_DELETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f57290bb4268a59ca745158796b34124aa7b56a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843930"
---
# <a name="oid_switch_port_property_delete"></a>OID\_SWITCH\_端口\_属性\_DELETE


Hyper-v 可扩展交换机的协议边缘发出 OID 的对象标识符（OID）设置请求\_SWITCH\_端口\_属性\_DELETE，以通知可扩展交换机扩展有关删除的策略属性可扩展交换机端口。

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个指向缓冲区的指针，该缓冲区包含一个[**NDIS\_SWITCH\_端口\_属性\_删除\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_delete_parameters)构造.

<a name="remarks"></a>备注
-------

转发扩展可以处理 OID\_SWITCH\_端口\_属性\_DELETE 的 OID 集请求。 所有其他类型的扩展都必须调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) ，将 OID 请求转发到可扩展交换机驱动程序堆栈中的下一个扩展。

有关如何处理 OID\_SWITCH\_端口\_属性\_DELETE 的 OID 集请求的指南，请参阅[管理端口策略](https://docs.microsoft.com/windows-hardware/drivers/network/managing-port-policies)。

### <a name="return-status-codes"></a>返回状态代码

如果转发扩展插件\_端口\_属性\_DELETE 完成 oid 的 OID 设置\_请求，则将返回以下状态代码之一。

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
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>转发扩展不支持端口策略。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>由于其他原因，OID 请求失败。</p></td>
</tr>
</tbody>
</table>

 

如果转发扩展未完成 OID\_SWITCH\_端口\_属性\_DELETE 的 OID 集请求，则该请求将由可扩展交换机的基础微型端口边缘完成。 微型端口边缘返回以下状态代码。

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

[**NDIS\_交换机\_端口\_属性\_自定义**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_custom)

[**NDIS\_交换机\_端口\_属性\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters)

[**NDIS\_交换机\_端口\_属性\_VLAN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_vlan)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

 

 




