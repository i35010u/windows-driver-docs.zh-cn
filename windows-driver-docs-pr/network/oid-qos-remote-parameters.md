---
title: OID_QOS_REMOTE_PARAMETERS
description: 过量驱动程序发出对象标识符 (OID) 查询请求 OID_QOS_REMOTE_PARAMETERS，以获取远程对等方的 NDIS 服务 (QoS) 参数。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_QOS_REMOTE_PARAMETERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bddfe19943c6771509ba1d5b26742214333cfed3
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248867"
---
# <a name="oid_qos_remote_parameters"></a>OID \_ QOS \_ 远程 \_ 参数


过量驱动程序发出 (OID 的对象标识符) 查询 OID \_ QOS \_ 远程参数请求 \_ ，以获取远程对等方 (QOS) 参数的 NDIS 服务质量。 微型端口驱动程序使用这些远程 QoS 参数来解析其操作的 NDIS QoS 参数。 驱动程序将包含操作参数的网络适配器配置为执行 QoS 数据包传输。

成功从 OID 查询请求返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**ndis \_ QOS \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构的指针。

**注意**  此 OID 查询请求仅对支持 IEEE 802.1 数据中心桥接 (DCB) 接口的微型端口驱动程序有效。

 

<a name="remarks"></a>备注
-------

当 NDIS 成功处理 OID QOS 远程参数的 OID 请求时 \_ \_ \_ ，它将返回其已从以前的 [**ndis \_ 状态 \_ QOS \_ 远程 \_ 参数 \_**](./ndis-status-qos-remote-parameters-change.md) 缓存的远程 NDIS qos 参数，并更改了微型端口驱动程序颁发的状态指示。 驱动程序发出此状态指示来报告初始远程 NDIS QoS 参数集。 每当远程 NDIS QoS 参数发生更改时，驱动程序还会发出此状态指示。

NDIS 返回按以下方式初始化的 [**ndis \_ QOS \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters) 结构：

-   如果微型端口驱动程序先前颁发了 [**ndis \_ 状态 \_ QOS \_ 远程 \_ 参数 \_ 更改**](./ndis-status-qos-remote-parameters-change.md) 状态指示，ndis 将缓存 [**ndis \_ qos \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters) 数据，并为 oid \_ qos \_ 远程参数的 oid 查询请求返回 \_ 此数据。

-   如果微型端口驱动程序未发出 [**ndis \_ 状态 \_ QOS \_ 远程 \_ 参数 \_ 更改**](./ndis-status-qos-remote-parameters-change.md) 状态指示，ndis 将返回 [**ndis \_ QOS \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters) 结构，其中所有成员均 (，但 **标头** 成员除外) 设置为零。

有关远程 NDIS QoS 参数的详细信息，请参阅 " [Ndis Qos 参数概述](./overview-of-ndis-qos-parameters.md)"。

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
<td><p>信息缓冲区的长度小于 sizeof (<a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters" data-raw-source="[&lt;strong&gt;NDIS_QOS_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)"><strong>NDIS_QOS_PARAMETERS</strong></a>) 。 NDIS 设置 <strong>数据。QUERY_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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
[**NdisMOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[**NDIS \_ QOS \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)

[**NDIS \_ 状态 \_ QOS \_ 操作 \_ 参数 \_ 更改**](./ndis-status-qos-operational-parameters-change.md)

[**NDIS \_ 状态 \_ QOS \_ 远程 \_ 参数 \_ 更改**](./ndis-status-qos-remote-parameters-change.md)

[OID \_ QOS \_ 参数](oid-qos-parameters.md)

