---
title: OID_SRIOV_BAR_RESOURCES
description: NDIS 发出对象标识符 (OID) 方法请求 OID_SRIOV_BAR_RESOURCES，以确定分配给 PCI Express (PCIe) 基址寄存器 ()  (VF) 的内存资源。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_BAR_RESOURCES 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d7d6fc9085f0c31e5bc42a461b36fb1139d9f789
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248809"
---
# <a name="oid_sriov_bar_resources"></a>OID \_ SRIOV \_ BAR \_ 资源


NDIS 发出对象标识符 (oid) 方法请求 OID \_ SRIOV \_ BAR \_ 资源，以确定分配给 PCI Express (PCIe) 基址寄存器 ()  (VF) 的内存资源。

NDIS 向网络适配器的 PCIe 物理功能 (PF) 的微型端口驱动程序发出此 OID 方法请求。 对于支持单个根 i/o 虚拟化 (SR-IOV) 接口的 PF 小型端口驱动程序，需要此 OID 方法请求。

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向缓冲区的指针。 此缓冲区包含以下结构：

-   用于指定 PF 微端口驱动程序返回其资源信息的 VF 和栏的 [**NDIS \_ SRIOV \_ BAR \_ 资源 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info) 结构。

-   一个 [**CM \_ 部分 \_ 资源 \_ 描述符**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor) 结构，它遵循 [**NDIS \_ SRIOV \_ BAR \_ 资源 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info) 结构。 **CM \_ 部分 \_ 资源 \_ 描述符** 结构包含有关分配给指定条形的内存资源的信息。

<a name="remarks"></a>备注
-------

NDIS 发出 OID SRIOV BAR 资源的 OID 方法请求， \_ \_ \_ 以获取分配给 VF 栏的内存资源的系统物理地址和长度。 在它发出 OID 方法请求之前，NDIS 按以下方式设置 [**ndis \_ SRIOV \_ BAR \_ 资源 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info) 结构的格式：

-   NDIS 将 [**ndis \_ SRIOV \_ BAR \_ 资源 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)结构的 **VFId** 成员设置为与 VF 关联的标识符。

-   NDIS 将 [**ndis \_ SRIOV \_ BAR \_ 资源 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)结构的 **BARINDEX** 成员设置为指定 VF 的条形索引。 条形索引是 PCI 配置空间中的栏表内寄存器的偏移量。

-   NDIS 将 [**ndis \_ SRIOV \_ bar \_ 资源 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)结构的 **BarResourcesOffset** 成员设置为偏移量（以字节为单位），从 **NDIS \_ SRIOV \_ bar \_ 资源 \_ 信息** 结构开始到 [**CM \_ 部分 \_ 资源 \_ 说明符**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor)结构。

**注意**  过量驱动程序（如协议或筛选器驱动程序）不能将 OID SRIOV BAR 资源的 OID 方法请求发送 \_ \_ \_ 到 PF 微型端口驱动程序。

 

当 PF 微型端口驱动程序接收到 OID 方法请求时，驱动程序将通过在 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员中设置 [**CM \_ 部分 \_ 资源 \_ 描述符**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor)结构的格式，来返回指定条形图的资源。 驱动程序将 **CM \_ 部分 \_ 资源 \_ 描述符** 结构与与指定 VF 的栏相关联的系统硬件资源进行格式化。

**注意**  驱动程序必须为 **CmResourceTypeMemory** 的资源类型设置结构格式。

 

### <a name="return-status-codes"></a>返回状态代码

对于 OID \_ SRIOV BAR 资源的方法请求，PF 微型端口驱动程序返回以下状态代码 \_ 之一 \_ 。

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
<td><p>PF 微型端口驱动程序不支持 (SR-IOV) 接口的单个根 i/o 虚拟化，或者未启用使用该接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_BAR_RESOURCES_INFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)"><strong>NDIS_SRIOV_BAR_RESOURCES_INFO</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区小于 (sizeof (<a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_BAR_RESOURCES_INFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)"><strong>NDIS_SRIOV_BAR_RESOURCES_INFO</strong></a>) + <a href="/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor" data-raw-source="[&lt;strong&gt;CM_PARTIAL_RESOURCE_DESCRIPTOR&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor)"><strong>sizeof (CM_PARTIAL_RESOURCE_DESCRIPTOR) 。</strong></a> PF 微型端口驱动程序必须设置 <strong>数据。METHOD_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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
[**CM \_ 部分 \_ 资源 \_ 说明符**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[**NDIS \_ SRIOV \_ BAR \_ 资源 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_bar_resources_info)

