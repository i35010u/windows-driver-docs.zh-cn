---
title: OID_QOS_OPERATIONAL_PARAMETERS
description: 过量驱动程序发出对象标识符 (OID) query 请求 OID_QOS_OPERATIONAL_PARAMETERS 获取网络适配器的当前 NDIS 服务 (QoS) 操作参数。
ms.assetid: 546EE7C6-BCED-4FF9-9B87-A36199B1B31C
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_QOS_OPERATIONAL_PARAMETERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2729a7c36494fd633cbbf64f88533cc0cf1c32c3
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103331"
---
# <a name="oid_qos_operational_parameters"></a>OID \_ QOS \_ 操作 \_ 参数


过量驱动程序发出 (OID 的对象标识符) 查询 OID \_ QOS \_ 操作参数的请求 \_ ，以获取网络适配器的当前 NDIS 服务 (QOS) 操作参数。 微型端口驱动程序将网络适配器配置为具有操作的 NDIS QoS 参数，以便执行 QoS 数据包传输。

成功从 OID 查询请求返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis \_ QOS \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构的指针。

**注意**   此 OID 查询请求由支持 IEEE 802.1 数据中心桥接 (DCB) 接口的微型端口驱动程序的 NDIS 处理。

 

<a name="remarks"></a>注解
-------

当 NDIS 成功处理 OID QOS 操作参数的 OID 查询请求时 \_ \_ \_ ，它将返回其已从以前的 [**ndis \_ 状态 \_ QOS \_ 操作 \_ 参数 \_ **](./ndis-status-qos-operational-parameters-change.md) 缓存的操作 NDIS qos 参数更改了由微型端口驱动程序颁发的状态指示。 驱动程序发出此状态指示来报告初始的操作 NDIS QoS 参数集。 每当操作 NDIS QoS 参数发生变化时，驱动程序还会发出此状态指示。

NDIS 返回按以下方式初始化的 [**ndis \_ QOS \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters) 结构：

-   如果微型端口驱动程序以前颁发了 [**ndis \_ 状态 \_ QOS \_ 操作 \_ 参数 \_ 更改**](./ndis-status-qos-operational-parameters-change.md) 状态指示，ndis 将缓存 [**ndis \_ qos \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters) 数据，并为 oid \_ qos \_ 操作参数的 oid 查询请求返回 \_ 此数据。

-   如果微型端口驱动程序未发出 [**ndis \_ 状态 \_ QOS \_ 操作 \_ 参数 \_ 更改**](./ndis-status-qos-operational-parameters-change.md) 状态指示，ndis 将返回 [**ndis \_ QOS \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters) 结构，其中的所有成员 (的 **标头** 成员除外) 设置为零。

有关操作 NDIS QoS 参数的详细信息，请参阅 " [Ndis Qos 参数概述](./overview-of-ndis-qos-parameters.md)"。

### <a name="return-status-codes"></a>返回状态代码

NDIS 返回以下状态代码之一。

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
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>微型端口驱动程序不支持 NDIS QoS 接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度小于 sizeof (<a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters" data-raw-source="[&lt;strong&gt;NDIS_QOS_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)"><strong>NDIS_QOS_PARAMETERS</strong></a>) 。 NDIS 设置 <strong>数据。QUERY_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
</tr>
<tr class="even">
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

## <a name="see-also"></a>请参阅


****
[**NdisMOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ QOS \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)

[**NDIS \_ 状态 \_ QOS \_ 操作 \_ 参数 \_ 更改**](./ndis-status-qos-operational-parameters-change.md)

[**NDIS \_ 状态 \_ QOS \_ 远程 \_ 参数 \_ 更改**](./ndis-status-qos-remote-parameters-change.md)

[OID \_ QOS \_ 参数](oid-qos-parameters.md)

