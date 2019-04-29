---
title: OID_SWITCH_PROPERTY_ADD
description: HYPER-V 可扩展交换机的协议边缘发出一个对象标识符 (OID) 组请求的 OID_SWITCH_PROPERTY_ADD 以通知有关的交换机策略属性添加可扩展交换机扩展。
ms.assetid: 63A6D2BE-81F4-4D27-B5DF-68466EFF306E
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PROPERTY_ADD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 76e250ddaf6855e0587968d2d05bb6e64b1946b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380692"
---
# <a name="oidswitchpropertyadd"></a>OID\_交换机\_属性\_添加


HYPER-V 可扩展交换机的协议边缘发出对象标识符 (OID) 组请求的 OID\_切换\_属性\_添加以通知有关的交换机策略属性添加可扩展交换机扩展

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向缓冲区的指针。 此缓冲区包含以下数据：

-   [ **NDIS\_切换\_属性\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598255)结构，它指定的标识和可扩展交换机策略的类型。

-   包含可扩展交换机策略的参数的属性缓冲区。 属性缓冲区包含基于的结构**PropertyType**的成员[ **NDIS\_开关\_属性\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598255)结构。

    **请注意**  从 Windows Server 2012 开始**PropertyType**成员必须设置为**NdisSwitchPropertyTypeCustom**和属性缓冲区必须包含[ **NDIS\_交换机\_属性\_自定义**](https://msdn.microsoft.com/library/windows/hardware/hh598247)结构。

     

<a name="remarks"></a>备注
-------

转发扩展可以处理 OID 集请求的 OID\_交换机\_属性\_添加。 所有其他类型的扩展必须调用[ **NdisFOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561830) OID 请求转发到可扩展交换机驱动程序堆栈中的下一个扩展。

扩展有权添加开关属性决策通过返回 NDIS\_状态\_数据\_不\_OID 请求被接受。 例如，如果扩展不能分配资源，以强制实施的交换机上其已更新的策略，它应能阻止添加请求。

**请注意**  如果扩展插件可以返回其他 NDIS\_状态\_*Xxx*还禁止错误状态代码，创建通知。 但是，返回状态代码为暂时性的情况下，如返回 NDIS\_状态\_资源，可能会导致创建通知的重试。

 

如果扩展不能阻止 OID 请求，它在请求完成时应监视的状态。 该扩展应这样做可以确定 OID 请求已被否决的可扩展交换机控制路径中的基础扩展或可扩展交换机接口。

有关如何处理 OID 的指导原则设置请求的 OID\_交换机\_属性\_添加，请参阅[管理交换机策略](https://msdn.microsoft.com/library/windows/hardware/hh598203)。

### <a name="return-status-codes"></a>返回状态代码

如果转发扩展完成 OID 集请求的 OID\_交换机\_属性\_添加，它将返回一个下面的状态代码。

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
<td><p>该扩展已禁止交换机策略添加通知。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>OID 请求失败，其他原因。</p></td>
</tr>
</tbody>
</table>

 

如果扩展不会完成 OID 集请求的 OID\_切换\_属性\_添加，请在请求完成的可扩展交换机基础的微型端口边缘。 微型端口边缘返回了以下状态代码。

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
[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_交换机\_属性\_自定义**](https://msdn.microsoft.com/library/windows/hardware/hh598247)

[**NDIS\_SWITCH\_PROPERTY\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh598255)

[**NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830)

 

 




