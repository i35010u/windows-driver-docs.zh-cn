---
title: OID_QOS_HARDWARE_CAPABILITIES
description: 过量驱动程序发出 OID_QOS_HARDWARE_CAPABILITIES 的对象标识符（OID）查询请求，以获取网络适配器的 NDIS 服务质量（QoS）硬件功能。
ms.assetid: 50D93F3F-DEA0-4D7D-8866-4155EED8D8BC
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_QOS_HARDWARE_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 37ef7ffb5e07ed976a67246b12c8c4c2fc12780a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844030"
---
# <a name="oid_qos_hardware_capabilities"></a>OID\_QOS\_硬件\_功能


过量驱动程序发出 OID\_QOS\_硬件\_功能的对象标识符（OID）查询请求，以获取网络适配器的 NDIS 服务质量（QoS）硬件功能。

成功从 OID 查询请求返回后， [**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis\_QOS\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)结构的指针。

**请注意**  此 OID 查询请求由支持 IEEE 802.1 数据中心桥接（DCB）接口的微型端口驱动程序的 NDIS 处理。

 

<a name="remarks"></a>备注
-------

[**Ndis\_QOS\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)结构包含有关网络适配器的 NDIS QOS 硬件功能的信息。 这些功能可能包括 INF 文件设置或**高级**属性页当前禁用的硬件功能。

**请注意**  网络适配器的所有 NDIS QoS 硬件功能都是通过 OID\_QOS\_硬件\_功能的 oid 查询请求返回的，不管是启用还是禁用功能。

 

在调用[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数时，微型端口驱动程序会注册网络适配器的 NDIS QoS 硬件功能。 驱动程序会按照以下步骤注册这些功能：

1.  驱动程序使用 NDIS QoS 硬件功能初始化[**ndis\_QOS\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)结构。

2.  驱动程序将[**ndis\_微型端口\_适配器的 HardwareQosCapabilities 成员设置\_硬件\_协助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构到指向 [**NDIS\_QOS\_功能的指针**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)结构。

3.  然后，微型端口驱动程序将调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数，并将*MiniportAttributes*参数设置为指向[**NDIS\_微型端口的指针\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构。

**请注意**  在绑定或附加操作期间，ndis 不会报告网络适配器的 NDIS QoS 硬件功能，以覆盖其协议和筛选器驱动程序。

 

有关如何注册 NDIS QoS 功能的详细信息，请参阅[注册 Ndis Qos 功能](https://docs.microsoft.com/windows-hardware/drivers/network/registering-ndis-qos-capabilities)。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID\_QOS 查询请求，\_对微型端口驱动程序的硬件\_功能请求，并返回以下状态代码之一。

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
<td><p>信息缓冲区的长度小于 sizeof （<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities" data-raw-source="[&lt;strong&gt;NDIS_QOS_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)"><strong>NDIS_QOS_CAPABILITIES</strong></a>）。 NDIS 设置<strong>数据。QUERY_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的 BytesNeeded 成员到所需的最小缓冲区大小。</p></td>
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
[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)

[**NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)

[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_QOS\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)

 

 




