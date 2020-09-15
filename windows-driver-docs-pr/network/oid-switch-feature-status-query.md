---
title: OID_SWITCH_FEATURE_STATUS_QUERY
description: Hyper-v 可扩展交换机的协议边缘发出对象标识符 (OID) 方法请求 OID_SWITCH_FEATURE_STATUS_QUERY，以获取有关可扩展交换机的扩展中的自定义状态信息。
ms.assetid: 580EFBD0-7798-4C56-99C5-84EADB8F8E82
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_FEATURE_STATUS_QUERY 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0f167d9a8a8f680340a2fccf498a7f359339d299
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105674"
---
# <a name="oid_switch_feature_status_query"></a>OID \_ 交换机 \_ 功能 \_ 状态 \_ 查询


Hyper-v 可扩展交换机的协议边缘发出对象标识符 (OID) 方法请求 OID \_ 交换机 \_ 功能 \_ 状态 \_ 查询，以获取有关可扩展交换机的扩展中的自定义状态信息。 此信息称为 *功能状态* 信息。 此信息的格式由独立软件供应商 (ISV) 来定义。

成功从此 OID 方法请求返回后， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向缓冲区的指针。 此缓冲区包含以下数据：

-   [**NDIS \_ 交换机 \_ 功能 \_ 状态 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_feature_status_parameters)结构，指定要返回的功能状态信息类型的参数。

-   一个 [**NDIS \_ 交换机 \_ 功能 \_ 状态 \_ 自定义**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_feature_status_custom) 结构，其中包含可扩展交换机的功能状态信息。

<a name="remarks"></a>备注
-------

有关如何处理 oid 设置 oid \_ 开关 \_ 功能 \_ 状态查询的准则 \_ ，请参阅 [管理自定义交换机功能状态信息](./managing-custom-switch-feature-status-information.md)。

### <a name="return-status-codes"></a>返回状态代码

该扩展插件为 OID \_ 交换机 \_ 功能 \_ 状态查询的 oid 方法请求返回以下状态代码之一 \_ 。

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
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度太小，无法返回功能状态信息以及 <a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_feature_status_custom" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_FEATURE_STATUS_CUSTOM&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_feature_status_custom)"><strong>NDIS_SWITCH_FEATURE_STATUS_CUSTOM</strong></a> 和 <a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_feature_status_parameters" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_FEATURE_STATUS_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_feature_status_parameters)"><strong>NDIS_SWITCH_FEATURE_STATUS_PARAMETERS</strong></a> 结构。 可扩展交换机的基础微型端口边缘设置 <strong>数据。METHOD_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ 交换机 \_ 属性 \_ 类型**](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_property_type)

[**NDIS \_ 交换机 \_ 功能 \_ 状态 \_ 自定义**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_feature_status_custom)

[**NDIS \_ 交换机 \_ 功能 \_ 状态 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_feature_status_parameters)

