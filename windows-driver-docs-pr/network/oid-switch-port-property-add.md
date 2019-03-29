---
title: OID_SWITCH_PORT_PROPERTY_ADD
description: HYPER-V 可扩展交换机的协议边缘发出一个对象标识符 (OID) 组请求的 OID_SWITCH_PORT_PROPERTY_ADD 以通知有关的可扩展交换机端口的策略属性添加可扩展交换机扩展。
ms.assetid: 6F246E5A-A02A-4303-9DB0-51E2FD4DC9E7
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PORT_PROPERTY_ADD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f600ffb9f9ef5e6fb125ce09adf9b243950cd9de
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348644"
---
# <a name="oidswitchportpropertyadd"></a>OID\_SWITCH\_PORT\_PROPERTY\_ADD


HYPER-V 可扩展交换机的协议边缘发出对象标识符 (OID) 组请求的 OID\_切换\_端口\_属性\_添加以通知有关的策略添加可扩展交换机扩展可扩展交换机端口的属性。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向缓冲区的指针。 此缓冲区包含以下数据：

-   [ **NDIS\_交换机\_端口\_属性\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598238)结构，它指定的标识和端口参数的类型策略。

-   包含端口的策略的参数的属性缓冲区。 属性缓冲区包含基于的结构**PropertyType**的成员[ **NDIS\_开关\_端口\_属性\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598238)结构。 例如，如果**PropertyType**成员设置为**NdisSwitchPortPropertyTypeVlan**，属性缓冲区包含[ **NDIS\_交换机\_端口\_属性\_VLAN** ](https://msdn.microsoft.com/library/windows/hardware/hh598243)结构。

<a name="remarks"></a>备注
-------

转发扩展可以处理 OID 集请求的 OID\_交换机\_端口\_属性\_添加。 所有其他类型的扩展必须调用[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830) OID 请求转发到可扩展交换机驱动程序堆栈中的下一个扩展。

扩展有权添加端口属性决策通过返回 NDIS\_状态\_数据\_不\_OID 请求被接受。 例如，如果扩展不能分配资源，以强制实施其配置的端口上的策略，它应能阻止添加请求。

**请注意**  如果扩展插件可以返回其他 NDIS\_状态\_*Xxx*还禁止错误状态代码，创建通知。 但是，返回状态代码为暂时性的情况下，如返回 NDIS\_状态\_资源，可能会导致创建通知的重试。

 

如果扩展不能阻止 OID 请求，它在请求完成时应监视的状态。 该扩展应这样做可以确定 OID 请求已被否决的可扩展交换机控制路径中的基础扩展或可扩展交换机接口。

有关如何处理 OID 的指导原则设置请求的 OID\_交换机\_端口\_属性\_添加，请参阅[管理端口策略](https://msdn.microsoft.com/library/windows/hardware/hh598202)。

### <a name="return-status-codes"></a>返回状态代码

如果转发扩展完成 OID 集请求的 OID\_交换机\_端口\_属性\_添加，它将返回以下状态代码之一：

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
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区长度太小，无法处理<a href="https://msdn.microsoft.com/library/windows/hardware/hh598238" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PORT_PROPERTY_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh598238)"> <strong>NDIS_SWITCH_PORT_PROPERTY_PARAMETERS</strong> </a>结构和结构的属性缓冲区中的数据。 扩展集<strong>数据。SET_INFORMATION。BytesNeeded</strong>中的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_DATA_NOT_ACCEPTED</p></td>
<td><p>转发扩展已禁止端口策略添加通知。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>转发扩展不支持端口策略。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>OID 请求失败，其他原因。</p></td>
</tr>
</tbody>
</table>

 

如果扩展不会完成 OID 集请求的 OID\_切换\_端口\_属性\_添加，请在请求完成的可扩展交换机基础的微型端口边缘。 微型端口边缘返回了以下状态代码：

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
[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_交换机\_端口\_属性\_自定义**](https://msdn.microsoft.com/library/windows/hardware/hh598230)

[**NDIS\_交换机\_端口\_属性\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598238)

[**NDIS\_交换机\_端口\_属性\_VLAN**](https://msdn.microsoft.com/library/windows/hardware/hh598243)

[**NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830)

 

 




