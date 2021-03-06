---
title: OID_SWITCH_PORT_PROPERTY_ENUM
description: Hyper-v 可扩展交换机扩展发出对象标识符 (OID) 方法请求 OID_SWITCH_PORT_PROPERTY_ENUM 获取数组。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PORT_PROPERTY_ENUM 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2e9198f19f1fb354460af86eccf706e4dfc70ca7
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248803"
---
# <a name="oid_switch_port_property_enum"></a>OID \_ 交换机 \_ 端口 \_ 属性 \_ 枚举


Hyper-v 可扩展交换机扩展发出对象标识符 (OID \_ 转换端口属性枚举的) 方法请求 \_ \_ \_ ，以获取一个数组。 此数组包含与指定条件匹配的预配端口策略。 数组中的每个元素都为指定的可扩展交换机端口指定了策略的属性。

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向缓冲区的指针。 此缓冲区包含以下数据：

-   [**NDIS \_ 交换机 \_ 端口 \_ 属性 \_ 枚举 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_parameters)结构，为指定端口的策略枚举指定参数。

-   [**NDIS \_ 交换机 \_ 端口 \_ 属性 \_ 枚举 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_info)结构的数组。 其中每个结构都包含有关可扩展交换机端口策略的属性的信息。

    **注意** 如果 [**ndis \_ 交换机 \_ 端口 \_ 属性 " \_ 枚举 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_parameters)结构" 的 **NumProperties** 成员设置为零，则不会返回 [**ndis \_ 交换机 \_ 端口 \_ 属性 \_ 枚举 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_info)结构。

     

<a name="remarks"></a>备注
-------

在发出 OID 交换机端口属性枚举的 OID 方法请求之前 \_ \_ \_ \_ ，可扩展交换机扩展必须遵循以下准则：

-   扩展只能在 \_ \_ \_ \_ 可扩展交换机的协议边缘发出 oid 交换机端口 [ \_ \_ \_ 创建](oid-switch-port-create.md) 请求之后，并且在发出 [oid \_ 交换机 \_ 端口 \_ 拆卸](oid-switch-port-teardown.md) 请求之前发出 oid 交换机端口属性 ENUM 请求。

-   扩展必须在调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)之前调用 [*ReferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port) ，以发出 OID \_ 交换机 \_ 端口 \_ 属性 \_ ENUM 请求。 这可确保在完成 OID 请求之前，不会删除指定的端口。

    完成 OID 请求后，扩展必须调用 [*DereferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port)。 此扩展必须调用此函数，而不考虑 OID 请求是否已完成，并且 NDIS \_ 状态是否 \_ 成功。

\_ \_ \_ \_ 仅当 hyper-v 可扩展交换机完成激活时才必须发出 oid 交换机端口属性枚举 oid。 有关更多详细信息，请参阅 [查询 Hyper-v 可扩展交换机配置](./querying-the-hyper-v-extensible-switch-configuration.md) 。

**注意**  如果扩展插件收到 oid \_ 交换机端口属性枚举的 oid 方法请求 \_ \_ \_ ，则它不能完成 oid 请求。 相反，它必须调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) 将 OID 请求向下转发到可扩展交换机驱动程序堆栈。

 

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘完成 OID \_ 交换机端口属性枚举的 oid 查询 \_ 请求 \_ \_ ，并返回以下状态代码。

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
[*DereferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[**NDIS \_ 交换机 \_ 端口 \_ 属性 \_ 枚举 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_info)

[**NDIS \_ 交换机 \_ 端口 \_ 属性 \_ 枚举 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_enum_parameters)

[**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[查询 Hyper-V 可扩展交换机配置](./querying-the-hyper-v-extensible-switch-configuration.md)

[*ReferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)

 

