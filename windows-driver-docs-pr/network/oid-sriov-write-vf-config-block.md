---
title: OID_SRIOV_WRITE_VF_CONFIG_BLOCK
description: 基础驱动程序发出的对象标识符 (OID) 组请求的 OID_SRIOV_WRITE_VF_CONFIG_BLOCK 将数据写入到 PCI Express (PCIe) 的虚拟函数 (VF) 配置块。
ms.assetid: 60527938-5627-482D-B94D-522DA8E32540
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_WRITE_VF_CONFIG_BLOCK 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8466e7d2bba5468c73a5f78f7598c2c381329355
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362886"
---
# <a name="oidsriovwritevfconfigblock"></a>OID\_SRIOV\_编写\_VF\_配置\_阻止


基础驱动程序将发出对象标识符 (OID) 组请求的 OID\_SRIOV\_编写\_VF\_配置\_块来将数据写入到 PCI Express (PCIe) 的虚拟函数 (VF) 配置块。

基础驱动程序此 OID 集向发出请求的微型端口驱动程序的网络适配器的 PCIe 物理函数 (PF)。 此 OID 方法请求是必需的支持的单个根 I/O 虚拟化 (SR-IOV) 接口的 PF 微型端口驱动程序。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含调用方分配的缓冲区的指针。 此缓冲区已格式化为包含以下信息：

-   [ **NDIS\_SRIOV\_编写\_VF\_配置\_阻止\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_block_parameters)结构，它包含的偏移量，以字节为单位，从缓冲区中的位置到此结构的开头包含到 VF 配置块写入的数据。

-   要写入到指定 VF 配置块数据的附加缓冲区空间。

<a name="remarks"></a>备注
-------

VF 配置块用于 backchannel PF 和 VF 微型端口驱动程序之间的通信。 IHV 可以定义一个或多个 VF 配置块微型端口驱动程序。 每个 VF 配置块都有 IHV 定义的格式、 长度和块 id。

**请注意**  仅由 PF 和 VF 微型端口驱动程序使用每个 VF 配置块中的数据。

 

它会发出的 OID OID 集请求之前\_SRIOV\_编写\_VF\_CONFIG\_阻止过量驱动程序必须设置的成员[ **NDIS\_SRIOV\_编写\_VF\_CONFIG\_阻止\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_block_parameters)结构如下所示：

-   设置**VFId**成员添加到为其的信息是要写入的 VF 的标识符。

-   设置**BlockId**成员添加到配置块是要写入信息的标识符。

-   设置**长度**成员添加到的字节数写入到 VF 配置块。

-   设置**BufferOffset**成员添加到缓冲区中的偏移量 (由引用**InformationBuffer**成员)，其中包含从指定 VF 配置块写入的数据。 从开始处的以字节为单位指定此偏移量[ **NDIS\_SRIOV\_编写\_VF\_配置\_阻止\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_block_parameters)结构。

当它处理 OID 集请求的 OID\_SRIOV\_编写\_VF\_配置\_阻止，PF 微型端口驱动程序必须遵循这些准则：

-   PF 微型端口驱动程序必须验证指定 VF **VFId**的成员[ **NDIS\_SRIOV\_编写\_VF\_配置\_阻止\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_block_parameters)结构，具有先前已分配的资源。 PF 微型端口驱动程序 OID 方法请求的过程将资源分配的 VF [OID\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)。 如果尚未分配指定 VF 的资源的驱动程序必须失败 OID 请求。

-   PF 微型端口驱动程序必须验证**BlockId**的成员[ **NDIS\_SRIOV\_编写\_VF\_配置\_块\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_block_parameters)结构指定有效的 VF 配置块。 如果没有，该驱动程序必须使该 OID 请求失败。

有关单根 I/O 虚拟化 (SR-IOV) 界面内 backchannel 通信的详细信息，请参阅[SR-IOV PF/取景器 Backchannel 通信](https://docs.microsoft.com/windows-hardware/drivers/network/sr-iov-pf-vf-backchannel-communication)。

### <a name="return-status-codes"></a>返回状态代码

微型端口驱动程序返回以下状态代码之一 OID 设置请求的 OID\_SRIOV\_编写\_VF\_配置\_阻止：

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
<td><p>微型端口驱动程序不支持的单个根 I/O 虚拟化 (SR-IOV) 接口，或未启用要使用的界面。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>一个或多个的成员<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_block_parameters" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_WRITE_VF_CONFIG_BLOCK_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_block_parameters)"> <strong>NDIS_SRIOV_WRITE_VF_CONFIG_BLOCK_PARAMETERS</strong> </a>结构具有无效值。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 集<strong>数据。SET_INFORMATION。BytesNeeded</strong>中的成员<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
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

[**NDIS\_SRIOV\_编写\_VF\_CONFIG\_阻止\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_block_parameters)

[OID\_NIC\_SWITCH\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

[OID\_SRIOV\_读取\_VF\_配置\_空间](oid-sriov-read-vf-config-space.md)

 

 




