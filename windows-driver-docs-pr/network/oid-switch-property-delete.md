---
title: OID_SWITCH_PROPERTY_DELETE
description: Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 OID_SWITCH_PROPERTY_DELETE 请求，通知有关删除交换机策略属性的可扩展交换机扩展。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PROPERTY_DELETE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9b19097640051ab77a1db74083fdbe6133912864
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248197"
---
# <a name="oid_switch_property_delete"></a>OID \_ 开关 \_ 属性 \_ 删除


Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 OID \_ 交换机 \_ 属性 DELETE 的请求 \_ ，以通知有关删除交换机策略属性的可扩展交换机扩展。

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含一个指向缓冲区的指针，该缓冲区包含 [**NDIS \_ 交换机 \_ 属性 \_ 删除 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_delete_parameters)结构。

<a name="remarks"></a>备注
-------

转发扩展可以处理 OID \_ 开关属性删除的 oid 设置请求 \_ \_ 。 所有其他类型的扩展都必须调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) ，将 OID 请求转发到可扩展交换机驱动程序堆栈中的下一个扩展。

有关如何处理 OID 交换机属性删除的 OID 集请求的 \_ 指南 \_ \_ ，请参阅 [管理交换机策略](./managing-switch-policies.md)。

### <a name="return-status-codes"></a>返回状态代码

如果转发扩展插件完成 oid \_ 开关属性 DELETE 的 oid 设置 \_ 请求 \_ ，它将返回以下状态代码之一。

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
<td><p>转发扩展不支持交换机策略。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>由于其他原因，OID 请求失败。</p></td>
</tr>
</tbody>
</table>

 

如果转发扩展未完成 oid 开关属性删除的 OID 集请求 \_ \_ \_ ，则该请求将由可扩展交换机的基础微型端口边缘完成。 微型端口边缘返回以下状态代码。

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
<td><p>Version</p></td>
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标题</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[**NDIS \_ 交换机 \_ 属性 \_ 自定义**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_custom)

[**NDIS \_ 开关 \_ 属性 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)

[**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

 

