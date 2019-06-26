---
title: OID_SWITCH_PORT_PROPERTY_ENUM
description: HYPER-V 可扩展交换机扩展问题的对象标识符 (OID) 方法请求的 OID_SWITCH_PORT_PROPERTY_ENUM 以获取数组。
ms.assetid: 5C391B82-FCA6-4A95-992F-EDB5DF6183C7
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PORT_PROPERTY_ENUM 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fd20c78d4cdf91e3e88a975f4002e94f5ab1e4e9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386990"
---
# <a name="oidswitchportpropertyenum"></a>OID\_SWITCH\_PORT\_PROPERTY\_ENUM


HYPER-V 可扩展交换机扩展发出对象标识符 (OID) 方法请求的 OID\_切换\_端口\_属性\_枚举以获取数组。 此数组包含与指定的条件匹配的预配的端口策略。 数组中的每个元素指定用于指定可扩展交换机端口的策略的属性。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向缓冲区的指针。 此缓冲区包含以下数据：

-   [ **NDIS\_交换机\_端口\_属性\_枚举\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_parameters)结构，它指定策略参数指定的端口的枚举。

-   一个数组[ **NDIS\_交换机\_端口\_属性\_枚举\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_info)结构。 每个这些结构包含可扩展交换机端口策略的属性有关的信息。

    **请注意**  如果**NumProperties**的成员[ **NDIS\_交换机\_端口\_属性\_枚举\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_parameters)结构设置为零，否[ **NDIS\_交换机\_端口\_属性\_枚举\_信息** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_info)返回结构。

     

<a name="remarks"></a>备注
-------

它所颁发的 OID 的 OID 方法请求之前\_切换\_端口\_属性\_枚举，可扩展交换机扩展必须遵守以下原则：

-   扩展只能颁发 OID\_切换\_端口\_属性\_枚举请求之后的可扩展交换机问题的协议边缘[OID\_切换\_端口\_创建](oid-switch-port-create.md)请求并且之前它所颁发[OID\_交换机\_端口\_拆卸](oid-switch-port-teardown.md)请求。

-   扩展必须调用[ *ReferenceSwitchPort* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port)调用之前[ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)发出 OID\_开关\_端口\_属性\_枚举请求。 这可以确保，OID 请求完成后，指定的端口不会删除之前。

    OID 请求完成后，则扩展必须调用[ *DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_dereference_switch_port)。 扩展必须调用此函数而不考虑 OID 请求是否已完成使用 NDIS\_状态\_成功。

OID\_切换\_端口\_属性\_的 HYPER-V 可扩展交换机完成激活后，才必须发出枚举 OID。 请参阅[查询的 HYPER-V 可扩展交换机配置](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-hyper-v-extensible-switch-configuration)的更多详细信息。

**请注意**  如果在扩展插件接收 OID 方法请求的 OID\_交换机\_端口\_属性\_枚举，它必须完成的 OID 请求。 相反，它必须调用[ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)可扩展交换机在驱动程序堆栈的下层 OID 请求转发。

 

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础的微型端口边缘完成 OID 查询请求的 OID\_切换\_端口\_属性\_枚举，并返回以下状态代码。

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

[**NDIS\_交换机\_端口\_属性\_枚举\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_info)

[**NDIS\_交换机\_端口\_属性\_枚举\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)

[查询的 HYPER-V 可扩展交换机配置](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-hyper-v-extensible-switch-configuration)

[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port)

 

 




