---
title: OID_QOS_OPERATIONAL_PARAMETERS
description: 过量驱动程序发出 OID_QOS_OPERATIONAL_PARAMETERS 的对象标识符（OID）查询请求，以获取网络适配器的当前 NDIS 服务质量（QoS）操作参数。
ms.assetid: 546EE7C6-BCED-4FF9-9B87-A36199B1B31C
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_QOS_OPERATIONAL_PARAMETERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c3ad5bdcaa1ae8bfc5d11d09f2316f3bfee3d829
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844028"
---
# <a name="oid_qos_operational_parameters"></a>OID\_QOS\_操作\_参数


过量驱动程序发出 OID\_QOS\_操作\_参数的对象标识符（OID）查询请求，以获取网络适配器的当前 NDIS 服务质量（QoS）操作参数。 微型端口驱动程序将网络适配器配置为具有操作的 NDIS QoS 参数，以便执行 QoS 数据包传输。

成功从 OID 查询请求返回后， [**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构的指针。

**请注意**  此 OID 查询请求由支持 IEEE 802.1 数据中心桥接（DCB）接口的微型端口驱动程序的 NDIS 处理。

 

<a name="remarks"></a>备注
-------

当 NDIS\_QOS 处理 OID 的 OID 查询请求时，它会成功地\_操作\_参数，它将返回它已从以前的 NDIS 缓存的操作 NDIS QoS 参数[ **\_状态\_QOS\_操作\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)由微型端口驱动程序颁发的状态指示。 驱动程序发出此状态指示来报告初始的操作 NDIS QoS 参数集。 每当操作 NDIS QoS 参数发生变化时，驱动程序还会发出此状态指示。

NDIS 按以下方式返回[ **\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构进行初始化：

-   如果微型端口驱动程序先前已将[**ndis\_状态\_QOS\_操作\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状态指示，ndis 会将[**ndis\_qos\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)数据缓存，并为 oid 的 oid 查询请求返回此数据\_QOS\_操作\_参数。

-   如果微型端口驱动程序未发出[**NDIS\_状态\_QOS\_操作\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状态指示，ndis 将返回[**ndis\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构，其中所有成员（**标头**成员除外）均设置为零。

有关操作 NDIS QoS 参数的详细信息，请参阅 " [Ndis Qos 参数概述](https://docs.microsoft.com/windows-hardware/drivers/network/overview-of-ndis-qos-parameters)"。

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
<td><p>信息缓冲区的长度小于 sizeof （<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters" data-raw-source="[&lt;strong&gt;NDIS_QOS_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)"><strong>NDIS_QOS_PARAMETERS</strong></a>）。 NDIS 设置<strong>数据。QUERY_INFORMATION。</strong>将<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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

 

 




