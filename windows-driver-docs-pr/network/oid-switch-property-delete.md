---
title: OID_SWITCH_PROPERTY_DELETE
description: HYPER-V 可扩展交换机的协议边缘发出一个对象标识符 (OID) 组请求的 OID_SWITCH_PROPERTY_DELETE 以通知有关交换机策略属性删除可扩展交换机扩展。
ms.assetid: 55291392-C018-4578-9767-DC5621F75D44
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PROPERTY_DELETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 623a3e6caacea31903a1914e2d12d89ec5bd6596
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386977"
---
# <a name="oidswitchpropertydelete"></a>OID\_交换机\_属性\_删除


HYPER-V 可扩展交换机的协议边缘发出对象标识符 (OID) 组请求的 OID\_切换\_属性\_删除以通知有关交换机策略属性删除可扩展交换机扩展。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向包含缓冲区[ **NDIS\_交换机\_属性\_删除\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_delete_parameters)结构。

<a name="remarks"></a>备注
-------

转发扩展可以处理 OID 集请求的 OID\_交换机\_属性\_删除。 所有其他类型的扩展必须调用[ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest) OID 请求转发到可扩展交换机驱动程序堆栈中的下一个扩展。

有关如何处理 OID 的指导原则设置请求的 OID\_交换机\_属性\_删除，请参阅[管理交换机策略](https://docs.microsoft.com/windows-hardware/drivers/network/managing-switch-policies)。

### <a name="return-status-codes"></a>返回状态代码

如果转发扩展完成 OID 集请求的 OID\_交换机\_属性\_删除，它返回一个下面的状态代码。

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
<td><p>转发扩展不支持的交换机策略。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>OID 请求失败，其他原因。</p></td>
</tr>
</tbody>
</table>

 

如果转发扩展不会完成 OID 集请求的 OID\_切换\_属性\_DELETE 请求完成的可扩展交换机基础的微型端口边缘。 微型端口边缘返回了以下状态代码。

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

[**NDIS\_交换机\_属性\_自定义**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_custom)

[**NDIS\_SWITCH\_PROPERTY\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)

 

 




