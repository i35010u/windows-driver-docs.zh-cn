---
title: OID_QOS_OPERATIONAL_PARAMETERS
description: 基础驱动程序发出的对象标识符 (OID) 查询请求的 OID_QOS_OPERATIONAL_PARAMETERS 来获取当前网络适配器的 NDIS 服务质量 (QoS) 操作的参数。
ms.assetid: 546EE7C6-BCED-4FF9-9B87-A36199B1B31C
ms.date: 08/08/2017
keywords: -OID_QOS_OPERATIONAL_PARAMETERS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 813538ebc3c871eb89fc705f1658e31183e6639b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363396"
---
# <a name="oidqosoperationalparameters"></a>OID\_QOS\_OPERATIONAL\_参数


基础驱动程序将发出对象标识符 (OID) 查询请求的 OID\_QOS\_OPERATIONAL\_参数来获取当前网络适配器的 NDIS 服务质量 (QoS) 操作的参数。 微型端口驱动程序以执行 QoS 数据包传输使用的操作的 NDIS QoS 参数配置的网络适配器。

从 OID 查询请求，成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构。

**请注意**  的微型端口驱动程序，支持 IEEE 802.1 数据中心桥接 (DCB) 接口由 NDIS 处理此 OID 查询请求。

 

<a name="remarks"></a>备注
-------

NDIS 时处理 OID 查询请求的 OID\_QOS\_OPERATIONAL\_参数成功，它返回已缓存的操作的 NDIS QoS 参数从以前[ **NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状态指示颁发的微型端口驱动程序。 驱动程序将发出此状态指示要报告操作的 NDIS QoS 参数的初始集。 每当操作的 NDIS QoS 参数发生更改时，该驱动程序也会发出此状态指示。

返回 NDIS [ **NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)按以下方式初始化结构：

-   如果微型端口驱动程序之前颁发[ **NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状态指示将缓存 NDIS [ **NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)数据，并返回 OID 查询此数据请求的 OID\_QOS\_OPERATIONAL\_参数。

-   如果微型端口驱动程序没有颁发[ **NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状态返回指示 NDIS [ **NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构的所有成员 (除**标头**成员) 将设置为零。

有关操作的 NDIS QoS 参数的详细信息，请参阅[NDIS QoS 参数的概述](https://docs.microsoft.com/windows-hardware/drivers/network/overview-of-ndis-qos-parameters)。

### <a name="return-status-codes"></a>返回状态代码

NDIS 返回下面的状态代码的一个。

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
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>微型端口驱动程序不支持的 NDIS QoS 接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度不超过 sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters" data-raw-source="[&lt;strong&gt;NDIS_QOS_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)"><strong>NDIS_QOS_PARAMETERS</strong></a>)。 NDIS 集<strong>数据。QUERY_INFORMATION。BytesNeeded</strong>中的成员<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
</tr>
<tr class="even">
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
[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismoidrequestcomplete)

[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_QOS\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_capabilities)

[**NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)

[**NDIS\_状态\_QOS\_远程\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)

[OID\_QOS\_PARAMETERS](oid-qos-parameters.md)

 

 




