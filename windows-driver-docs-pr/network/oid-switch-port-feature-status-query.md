---
title: OID_SWITCH_PORT_FEATURE_STATUS_QUERY
description: Hyper-v 可扩展交换机的协议边缘发出 OID_SWITCH_PORT_FEATURE_STATUS_QUERY 的对象标识符（OID）方法请求，以获取有关可扩展交换机端口的扩展中的自定义状态信息。
ms.assetid: 577CF1C2-9737-4FB0-9C40-AEE529EF1439
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PORT_FEATURE_STATUS_QUERY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a3ec424d3e9451c56ba669d170dba9392c325aca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843934"
---
# <a name="oid_switch_port_feature_status_query"></a>OID\_交换机\_端口\_功能\_状态\_查询


Hyper-v 可扩展交换机的协议边缘发出 OID 的对象标识符（OID）方法请求\_SWITCH\_端口\_功能\_状态\_查询，以获取有关的扩展中的自定义状态信息可扩展交换机端口。 此信息称为*功能状态*信息。 此信息的格式是由独立软件供应商（ISV）定义的。

成功从此 OID 方法请求返回后， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向**缓冲区的指针**。 此缓冲区包含以下数据：

-   [**NDIS\_交换机\_端口\_功能\_状态\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters)结构，它指定要返回的功能状态信息类型的参数。

-   [**NDIS\_交换机\_端口\_功能\_状态\_自定义**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_custom)结构，其中包含可扩展交换机端口的功能状态信息。

<a name="remarks"></a>备注
-------

有关如何处理 OID\_SWITCH\_端口\_功能\_状态\_查询的 OID 集请求的指南，请参阅[管理自定义端口功能状态信息](https://docs.microsoft.com/windows-hardware/drivers/network/managing-custom-port-feature-status-information)。

### <a name="return-status-codes"></a>返回状态代码

该扩展将为 OID 的 OID 方法请求（\_SWITCH\_端口\_功能\_状态\_查询）返回以下状态代码之一。

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
<td><p>信息缓冲区的长度太小，无法返回功能状态信息以及<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_custom" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PORT_FEATURE_STATUS_CUSTOM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_custom)"><strong>NDIS_SWITCH_PORT_FEATURE_STATUS_CUSTOM</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PORT_FEATURE_STATUS_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters)"><strong>NDIS_SWITCH_PORT_FEATURE_STATUS_PARAMETERS</strong></a>结构。 可扩展交换机的基础微型端口边缘设置<strong>数据。METHOD_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的 BytesNeeded 成员到所需的最小缓冲区大小。</p></td>
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

[**NDIS\_交换机\_端口\_功能\_状态\_自定义**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_custom)

[**NDIS\_交换机\_端口\_功能\_状态\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters)

[**NDIS\_交换机\_端口\_属性\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_port_property_type)

 

 




