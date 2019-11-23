---
title: OID_SWITCH_PROPERTY_ENUM
description: Hyper-v 可扩展交换机扩展发出 OID_SWITCH_PROPERTY_ENUM 获取数组的对象标识符（OID）方法请求。
ms.assetid: 45277355-4486-4CE0-ACBF-68D6BC6B79E7
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PROPERTY_ENUM 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 220b0885b9393d13853bd363bcfe93b529fdde4d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843916"
---
# <a name="oid_switch_property_enum"></a>OID\_SWITCH\_属性\_枚举


Hyper-v 可扩展交换机扩展发出 OID 的对象标识符（OID）方法请求\_SWITCH\_属性\_ENUM 来获取数组。 此数组包含与指定条件匹配的预配交换机策略。 数组中的每个元素指定可扩展交换机策略的属性。

[ **\_OID 的 NDIS\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向缓冲区的指针。 此缓冲区包含以下数据：

-   [**NDIS\_交换机\_属性\_枚举\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters)结构，该结构指定可扩展交换机策略枚举的参数。

-   一组[**NDIS\_交换机\_属性\_枚举\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info)结构。 其中每个结构都包含有关可扩展交换机策略的信息。

    **请注意**  如果尚未通过指定的可扩展交换机策略的实例对扩展进行预配，则扩展会将[**NDIS\_SWITCH\_\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters)的**NumProperties**成员设置为零，且不会返回[**ndis\_switch\_属性\_枚举\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info)结构。\_

     

<a name="remarks"></a>备注
-------

仅当 Hyper-v 可扩展交换机完成激活时，才必须发出 OID\_SWITCH\_属性\_ENUM OID。 有关更多详细信息，请参阅[查询 Hyper-v 可扩展交换机配置](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-hyper-v-extensible-switch-configuration)。

与[oid\_switch\_端口\_属性\_枚举](oid-switch-port-property-enum.md)的 oid 查询请求不同，在发出 oid 时无需调用任何*ReferenceSwitchXxx*或*DereferenceSwitchXxx*函数\_在可扩展交换机驱动程序堆栈中\_枚举请求。\_

**请注意**  如果扩展接收 OID 的 oid 方法请求\_SWITCH\_属性\_枚举，则它不能完成 oid 请求。 相反，它必须调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)将 OID 请求向下转发到可扩展交换机驱动程序堆栈。

 

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘\_SWITCH\_属性\_ENUM 完成 oid 查询请求，并返回以下状态代码之一。

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
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度太小，无法返回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PROPERTY_ENUM_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters)"><strong>NDIS_SWITCH_PROPERTY_ENUM_PARAMETERS</strong></a>结构及其<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PROPERTY_ENUM_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info)"><strong>NDIS_SWITCH_PROPERTY_ENUM_INFO</strong></a>元素数组。 可扩展交换机的基础微型端口边缘设置<strong>数据。METHOD_INFORMATION。</strong>将<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_FAILURE</p></td>
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

[**NDIS\_交换机\_属性\_枚举\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_info)

[ **\_属性\_枚举\_参数的 NDIS\_开关**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_property_enum_parameters)

[查询 Hyper-v 可扩展交换机配置](https://docs.microsoft.com/windows-hardware/drivers/network/querying-the-hyper-v-extensible-switch-configuration)

 

 




