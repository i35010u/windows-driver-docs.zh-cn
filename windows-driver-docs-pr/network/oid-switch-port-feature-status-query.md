---
title: OID_SWITCH_PORT_FEATURE_STATUS_QUERY
description: 对象标识符 (OID) 方法请求的 OID_SWITCH_PORT_FEATURE_STATUS_QUERY 以获取自定义状态信息从可扩展交换机端口有关的扩展的 HYPER-V 可扩展交换机问题协议边缘。
ms.assetid: 577CF1C2-9737-4FB0-9C40-AEE529EF1439
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PORT_FEATURE_STATUS_QUERY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 20b880b46f5a1defe558c0cc7e64a0856f56f065
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356104"
---
# <a name="oidswitchportfeaturestatusquery"></a>OID\_交换机\_端口\_功能\_状态\_查询


HYPER-V 可扩展交换机的协议边缘发出对象标识符 (OID) 方法请求的 OID\_切换\_端口\_功能\_状态\_查询以获取从自定义状态信息有关可扩展交换机端口的扩展。 此信息被称为*功能状态*信息。 此信息的格式由独立软件供应商 (ISV) 定义。

通过此 OID 方法请求成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含指向缓冲区的指针。 此缓冲区包含以下数据：

-   [ **NDIS\_交换机\_端口\_功能\_状态\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters)结构，它指定的类型的参数要返回的功能状态信息。

-   [ **NDIS\_交换机\_端口\_功能\_状态\_自定义**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_custom)结构，其中包含有关状态的功能信息可扩展交换机端口中。

<a name="remarks"></a>备注
-------

有关如何处理 OID 的指导原则设置请求的 OID\_交换机\_端口\_功能\_状态\_查询，请参阅[管理自定义端口功能状态信息](https://docs.microsoft.com/windows-hardware/drivers/network/managing-custom-port-feature-status-information)。

### <a name="return-status-codes"></a>返回状态代码

扩展插件可以返回一个 OID 的 OID 方法请求的以下状态代码\_交换机\_端口\_功能\_状态\_查询。

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
<td><p>信息缓冲区长度太小，无法返回功能的状态信息并将<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_custom" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PORT_FEATURE_STATUS_CUSTOM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_custom)"> <strong>NDIS_SWITCH_PORT_FEATURE_STATUS_CUSTOM</strong> </a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_PORT_FEATURE_STATUS_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters)"> <strong>NDIS_SWITCH_PORT_FEATURE_STATUS_PARAMETERS</strong> </a>结构。 可扩展交换机设置的基础的微型端口边缘<strong>数据。METHOD_INFORMATION。BytesNeeded</strong>中的成员<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>请求由于其他原因而失败。</p></td>
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

[**NDIS\_交换机\_端口\_功能\_状态\_自定义**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_custom)

[**NDIS\_交换机\_端口\_功能\_状态\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_feature_status_parameters)

[**NDIS\_SWITCH\_PORT\_PROPERTY\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_switch_port_property_type)

 

 




