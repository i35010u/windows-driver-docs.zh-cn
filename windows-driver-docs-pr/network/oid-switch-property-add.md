---
title: OID_SWITCH_PROPERTY_ADD
description: Hyper-v 可扩展交换机的协议边缘发出 OID_SWITCH_PROPERTY_ADD 的对象标识符（OID）设置请求，以通知有关添加开关策略属性的可扩展交换机扩展。
ms.assetid: 63A6D2BE-81F4-4D27-B5DF-68466EFF306E
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PROPERTY_ADD 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6a84d1816bacbc067de057c1e4e51e8c04caee65
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843920"
---
# <a name="oid_switch_property_add"></a>OID\_SWITCH\_属性\_添加


Hyper-v 可扩展交换机的协议边缘发出一个对象标识符（OID）\_SWITCH\_属性的设置请求，\_添加以通知可扩展交换机扩展有关添加交换机策略属性的信息

[ **\_OID 的 NDIS\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向缓冲区的指针。 此缓冲区包含以下数据：

-   [**NDIS\_交换机\_属性\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)结构，用于指定可扩展交换机策略的标识和类型。

-   包含可扩展交换机策略参数的属性缓冲区。 属性缓冲区包含一个结构，该结构基于[**NDIS\_SWITCH\_属性\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)结构中的**PropertyType**成员。

    **注意**  从 Windows Server 2012 开始， **PropertyType**成员必须设置为**NdisSwitchPropertyTypeCustom** ，并且属性缓冲区必须包含[**NDIS\_SWITCH\_属性\_自定义**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_custom)构造.

     

<a name="remarks"></a>备注
-------

转发扩展可以处理 OID\_SWITCH\_属性\_添加的 OID 设置请求。 所有其他类型的扩展都必须调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) ，将 OID 请求转发到可扩展交换机驱动程序堆栈中的下一个扩展。

此扩展可以通过将 NDIS\_状态返回\_数据\_未\_为 OID 请求接受，来否决添加 switch 属性。 例如，如果扩展无法分配资源来在交换机上强制实施其更新的策略，则它应否决添加请求。

**请注意**  如果扩展返回\_*Xxx*错误状态代码的其他 NDIS\_状态，则创建通知也被否决。 然而，为暂时性方案返回状态代码（如将 NDIS\_状态返回\_资源）可能会导致创建通知重试。

 

如果扩展不否决 OID 请求，则应在请求完成时监视状态。 扩展应执行此操作，以确定可扩展交换机控制路径中的基础扩展或可扩展交换机接口是否否决了 OID 请求。

有关如何处理 OID\_SWITCH\_属性\_"添加" 的 OID 集请求的指南，请参阅[管理交换机策略](https://docs.microsoft.com/windows-hardware/drivers/network/managing-switch-policies)。

### <a name="return-status-codes"></a>返回状态代码

如果转发扩展插件完成 oid\_SWITCH\_属性\_"添加"，则它将返回以下状态代码之一。

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
<td><p>扩展已拒绝交换机策略添加通知。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>由于其他原因，OID 请求失败。</p></td>
</tr>
</tbody>
</table>

 

如果扩展未完成 OID 的 OID 集请求\_SWITCH\_属性\_"添加"，则请求将由可扩展交换机的基础微型端口边缘完成。 微型端口边缘返回以下状态代码。

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

[ **\_\_自定义的 NDIS\_交换机**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_custom)

[ **\_属性\_参数的 NDIS\_开关**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

 

 




