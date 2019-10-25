---
title: OID_QOS_REMOTE_PARAMETERS
description: 过量驱动程序发出 OID_QOS_REMOTE_PARAMETERS 的对象标识符（OID）查询请求，以获取远程对等方的 NDIS 服务质量（QoS）参数。
ms.assetid: F9DA87FF-577F-4E06-929B-4AD65105B2F0
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_QOS_REMOTE_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4b2ded1c4f44ccea3969828ff7aa0138e6d53724
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844023"
---
# <a name="oid_qos_remote_parameters"></a>OID\_QOS\_远程\_参数


过量驱动程序发出 OID 的对象标识符（OID）查询请求\_QOS\_远程\_参数获取远程对等方的 NDIS 服务质量（QoS）参数。 微型端口驱动程序使用这些远程 QoS 参数来解析其操作的 NDIS QoS 参数。 驱动程序将包含操作参数的网络适配器配置为执行 QoS 数据包传输。

成功从 OID 查询请求返回后， [**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构的指针。

**请注意**  此 OID 查询请求仅对支持 IEEE 802.1 数据中心桥接（DCB）接口的微型端口驱动程序有效。

 

<a name="remarks"></a>备注
-------

当 NDIS\_QOS 处理 OID 的 OID 请求时，将会成功地\_远程\_参数，它将返回从上一个 NDIS 缓存的远程 NDIS QoS 参数[ **\_状态\_QOS\_远程\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)由微型端口驱动程序颁发的状态指示。 驱动程序发出此状态指示来报告初始远程 NDIS QoS 参数集。 每当远程 NDIS QoS 参数发生更改时，驱动程序还会发出此状态指示。

NDIS 按以下方式返回[ **\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构进行初始化：

-   如果微型端口驱动程序先前已将[**ndis\_状态\_QOS\_远程\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)状态指示，ndis 会缓存[**ndis\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)数据并返回此数据对于 OID\_QOS 查询请求\_远程\_参数。

-   如果微型端口驱动程序未发出[**ndis\_状态\_QOS\_远程\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)状态指示，ndis 将返回具有所有成员的[**ndis\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构（**标头**成员除外）设置为零。

有关远程 NDIS QoS 参数的详细信息，请参阅 " [Ndis Qos 参数概述](https://docs.microsoft.com/windows-hardware/drivers/network/overview-of-ndis-qos-parameters)"。

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
<td><p>微型端口驱动程序不支持 NDIS QoS 接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度小于 sizeof （<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters" data-raw-source="[&lt;strong&gt;NDIS_QOS_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)"><strong>NDIS_QOS_PARAMETERS</strong></a>）。 NDIS 设置<strong>数据。QUERY_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的 BytesNeeded 成员到所需的最小缓冲区大小。</p></td>
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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_QOS\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)

[**NDIS\_状态\_QOS\_操作\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)

[**NDIS\_状态\_QOS\_远程\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)

[OID\_QOS\_参数](oid-qos-parameters.md)

 

 




