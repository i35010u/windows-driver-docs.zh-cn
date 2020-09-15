---
title: OID_SRIOV_CURRENT_CAPABILITIES
description: 过量驱动程序发出对象标识符 (OID) 查询请求 OID_SRIOV_CURRENT_CAPABILITIES 获取网络适配器的当前单一根 i/o 虚拟化 (SR-IOV) 功能。
ms.assetid: EE76B3F8-2883-484A-B2EE-6F7D4738934E
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_CURRENT_CAPABILITIES 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ad7a8e0ec8c9d3615e8b65efac230c954d9b651f
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102828"
---
# <a name="oid_sriov_current_capabilities"></a>OID \_ SRIOV \_ 当前 \_ 功能


过量驱动程序会发出对象标识符 (OID) query 请求， \_ \_ \_ 以获取网络适配器的当前单一根 i/o 虚拟化 (sr-iov) 功能。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ SRIOV \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)结构的指针。

<a name="remarks"></a>备注
-------

从 NDIS 6.30 开始，微型端口驱动程序在调用 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数时，将在网络适配器上提供已启用的 sr-iov 硬件功能。 驱动程序使用当前启用的 SR-IOV 硬件功能初始化[**ndis \_ SRIOV \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)结构，并将[**ndis \_ 微型端口 \_ 适配器 \_ 硬件 \_ 辅助 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构的**CurrentSriovCapabilities**成员设置为指向**NDIS \_ SRIOV \_ 功能**结构的指针。 然后，小型端口驱动程序将调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) 函数，并将 *MiniportAttributes* 参数设置为指向 **NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 协助 \_ 属性** 结构的指针。

过量协议和筛选器驱动程序不必发出 oid \_ SRIOV 当前功能的 oid 查询 \_ 请求 \_ 。 NDIS 按以下方式向这些驱动程序提供当前启用的网络适配器 SR-IOV 功能：

-   NDIS 在绑定操作过程中报告基本网络适配器当前启用的 SR-IOV 功能，以便在[**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构的**SriovCapabilities**成员中覆盖协议驱动程序。

-   NDIS 报告基础网络适配器当前启用的 SR-IOV 功能，以便在附加操作期间覆盖[**NDIS \_ 筛选器 \_ 附加 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)结构的**SriovCapabilities**成员中的驱动程序。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理对 \_ \_ 微型端口驱动程序的 oid SRIOV 当前功能请求的 oid 查询请求 \_ 。 将不会向此 OID 请求颁发驱动程序。

当 NDIS 处理 OID \_ SRIOV \_ CURRENT \_ 功能请求时，它将返回以下状态代码之一：

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
<td><p>微型端口驱动程序不支持 (SR-IOV) 接口的单个根 i/o 虚拟化，或者未启用使用该接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 微型端口驱动程序必须设置 <strong>数据。QUERY_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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

## <a name="see-also"></a>另请参阅


****
[**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS \_ 筛选器 \_ 附加 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 辅助 \_ 特性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)

[**NDIS \_ SRIOV \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)

[**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

