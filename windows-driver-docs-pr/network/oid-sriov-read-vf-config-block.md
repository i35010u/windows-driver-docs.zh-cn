---
title: OID_SRIOV_READ_VF_CONFIG_BLOCK
description: 过量驱动程序发出对象标识符 (OID) 方法请求 OID_SRIOV_READ_VF_CONFIG_BLOCK 从指定的 PCI Express (PCIe) 虚拟函数 (VF) 配置块中读取数据。
ms.assetid: A7AC7A18-5DA2-4EE8-B635-04616ABFE08C
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_READ_VF_CONFIG_BLOCK 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d2a3ee5e3da4de087cca914110b37a9ed7a1e076
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102416"
---
# <a name="oid_sriov_read_vf_config_block"></a>OID \_ SRIOV \_ 读取 \_ VF \_ 配置 \_ 块


过量驱动程序发出 (OID 的对象标识符) 方法请求 OID \_ SRIOV \_ read \_ VF \_ CONFIG \_ 块，以便从指定 PCI Express (PCIE) 虚函数 (VF) 配置块中读取数据。

过量驱动程序将此 OID 方法请求发送到网络适配器的 PCIe 物理功能 (PF) 的微型端口驱动程序。 对于支持单个根 i/o 虚拟化 (SR-IOV) 接口的 PF 小型端口驱动程序，需要此 OID 方法请求。

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向调用方分配的缓冲区的指针。 此缓冲区的格式设置为包含以下内容：

-   [**NDIS \_ SRIOV \_ 读取 \_ vf \_ 配置 \_ 块 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters)结构，其中包含从该结构开始到缓冲区内的某个位置的偏移量（以字节为单位），其中包含从 VF 配置块中读取的数据。

-   要从指定的 VF 配置块中读取的数据的额外缓冲区空间。

<a name="remarks"></a>备注
-------

VF 配置块用于 backchannel 和 VF 微型端口驱动程序之间的通信。 IHV 可以为微型端口驱动程序定义一个或多个 VF 配置块。 每个 VF 配置块都有一个 IHV 定义的格式、长度和块 ID。

**注意**   每个 VF 配置块中的数据仅用于 PF 和 VF 微型端口驱动程序。

 

在发出 OID \_ SRIOV read vf config 块的 oid 方法请求之前 \_ \_ \_ \_ ，过量驱动程序必须按以下方式设置 [**NDIS \_ SRIOV \_ READ \_ vf \_ config \_ block \_ PARAMETERS**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters) 结构的成员：

-   将 **VFId** 成员设置为要从中读取信息的 VF 的标识符。

-   将 **块 id** 成员设置为要从中读取信息的 VF 配置块的标识符。

-   将 **Length** 成员设置为要从配置块中读取的字节数。

-   将 **BufferOffset** 成员设置为缓冲区内的偏移量 (**) 成员将** 包含从指定的 VF 配置块中读取的数据。 此偏移量以字节为单位，从 [**NDIS \_ SRIOV \_ 读取 \_ VF \_ 配置 \_ 块 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters) 结构开始。

当它处理 OID \_ SRIOV READ VF CONFIG 块的 oid 方法请求时 \_ \_ \_ \_ ，PF 微型端口驱动程序必须遵循以下准则：

-   PF 微型端口驱动程序必须验证由[**NDIS \_ SRIOV \_ READ \_ VF \_ CONFIG \_ 块 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters)结构的**VFId**成员指定的 VF 是否包含之前已分配的资源。 在 oid [ \_ NIC \_ 交换机 \_ 分配 \_ vf](oid-nic-switch-allocate-vf.md)的 oid 方法请求期间，PF 微型端口驱动程序为 VF 分配资源。 如果没有为指定的 VF 分配资源，则驱动程序必须使 OID 请求失败。

-   PF 微型端口驱动程序必须验证[**NDIS \_ SRIOV \_ READ \_ VF \_ 配置 \_ 块 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters)结构的**块 id**成员是否指定了有效的 VF 配置块。 否则，驱动程序必须使 OID 请求失败。

有关 backchannel) 接口 (的单个根 i/o 虚拟化内的通信的详细信息，请参阅 [SR-IOV PF/VF Backchannel 通信](./sr-iov-pf-vf-backchannel-communication.md)。

### <a name="return-status-codes"></a>返回状态代码

PF 多端口驱动程序为 OID \_ SRIOV \_ 读取 \_ VF \_ 配置 \_ 块的方法请求返回以下状态代码之一。

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
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_READ_VF_CONFIG_BLOCK_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters)"><strong>NDIS_SRIOV_READ_VF_CONFIG_BLOCK_PARAMETERS</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 微型端口驱动程序必须设置 <strong>数据。METHOD_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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
[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ SRIOV \_ 读取 \_ VF \_ 配置 \_ 块 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_block_parameters)

[OID \_ NIC \_ 交换机 \_ 分配 \_ VF](oid-nic-switch-allocate-vf.md)

[OID \_ SRIOV \_ 读取 \_ VF \_ 配置 \_ 空间](oid-sriov-read-vf-config-space.md)

