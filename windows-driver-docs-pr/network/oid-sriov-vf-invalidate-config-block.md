---
title: OID_SRIOV_VF_INVALIDATE_CONFIG_BLOCK
description: NDIS 发出 OID_SRIOV_VF_INVALIDATE_CONFIG_BLOCK 的对象标识符（OID）方法请求，通知一个或多个配置块中的数据已更改，通知 PCI Express （PCIe）虚拟函数（VF）的微型端口驱动程序已更改。
ms.assetid: CF73E0DA-20DA-49A0-80B0-0F5A56DCEF5D
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_VF_INVALIDATE_CONFIG_BLOCK 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 54838ce21ac6c3a5a1007429ce026109b6d79c33
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843976"
---
# <a name="oid_sriov_vf_invalidate_config_block"></a>OID\_SRIOV\_VF\_无效\_配置\_块


NDIS\_SRIOV\_VF 发出 OID 的对象标识符（OID）方法请求\_使\_CONFIG\_块无效，以通知一个或多个配置块中的数据已更改。 当 PCIe 物理功能（PF）的微型端口驱动程序调用[**NdisMInvalidateConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisminvalidateconfigblock)时，NDIS 会发出此 OID。

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_SRIOV\_VF 的指针\_使\_配置\_块\_INFO 结构无效**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info)。 此结构指定一个或多个虚拟函数（VF）配置块，这些配置块的数据已由 PF 微型端口驱动程序更改（*失效*）。

<a name="remarks"></a>备注
-------

VF 配置块用于 backchannel 和 VF 微型端口驱动程序之间的通信。 IHV 可以为设备定义一个或多个 VF 配置块。 每个 VF 配置块都有一个 IHV 定义的格式、长度和块 ID。

**请注意**，每个 VF 配置块中  的数据仅供 PF 和 VF 微型端口驱动程序使用。

 

VF 配置数据在以下驱动程序之间交换：

-   在来宾操作系统中运行的 VF 驱动程序。 此操作系统在 Hyper-v 子分区中运行。

-   PF 驱动程序，它在管理操作系统中运行。 此操作系统在 Hyper-v 父分区中运行。

为了处理无效 VF 配置数据的通知，NDIS 和微型端口驱动程序执行以下步骤：

1.  在来宾操作系统中，NDIS 发出对 IOCTL\_的 i/o 控制请求[ **\_使\_块请求无效**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block)。 完成此 IOCTL 后，将通知 NDIS 配置数据已更改。

2.  在管理操作系统中，将执行以下步骤：

    1.  PF 微型端口驱动程序调用[**NdisMInvalidateConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisminvalidateconfigblock)函数，以通知 NDIS VF 配置数据已更改，并且不再有效。 驱动程序将*BlockMask*参数设置为 ULONGLONG 位掩码，该位掩码指定哪些 VF 配置块发生了更改。 位掩码中的每个位对应于一个 VF 配置块。 如果将位设置为1，则相应的 VF 配置块中的数据已更改。
    2.  NDIS 向虚拟化堆栈发出信号，该堆栈在管理操作系统中运行，关于 VF 配置块数据的更改。 虚拟化堆栈缓存*BlockMask*参数数据。

        **请注意**  每次 PF 微型端口驱动程序调用[**NdisMInvalidateConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisminvalidateconfigblock)时，虚拟化堆栈会将*BlockMask*参数数据与缓存中的当前值 or。

         

    3.  虚拟化堆栈会通知虚拟 PCI （VPCI）驱动程序，该驱动程序在来宾操作系统中运行，这与 VF 配置数据的无效有关。 虚拟化堆栈会将缓存的*BlockMask*参数数据发送到 VPCI 驱动程序。

3.  在来宾操作系统中，将执行以下步骤：

    1.  VPCI 驱动程序将缓存的*BlockMask*参数数据保存在 VPCI\_的**BlockMask**成员中会使与[**IOCTL\_VPCI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block) [ **\_块\_输出结构的输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ns-vpci-_vpci_invalidate_block_output)结构无效\_块请求无效。\_

    2.  VPCI 驱动程序已成功完成[**IOCTL\_VPCI\_使\_块请求无效**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block)。 发生这种情况时，NDIS\_SRIOV\_VF 发出 oid 方法请求，\_将\_配置\_块无效到 VF 微型端口驱动程序。 [**NDIS\_SRIOV\_VF\_使\_配置\_块无效，\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info)将在 OID 请求中传递。 此结构包含缓存的*BlockMask*参数数据。

        NDIS 还会发出其他[**IOCTL\_VPCI\_使**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block)处理 VF 配置数据更改的连续通知\_块请求无效。

    3.  当 VF 驱动程序处理 OID\_SRIOV\_VF\_使\_配置\_块请求无效时，它将读取指定的 VF 配置块中的数据。

有关单根 i/o 虚拟化（SR-IOV）接口中的 backchannel 通信的详细信息，请参阅[SR-IOV PF/VF Backchannel 通信](https://docs.microsoft.com/windows-hardware/drivers/network/sr-iov-pf-vf-backchannel-communication)。

### <a name="return-status-codes"></a>返回状态代码

微型端口驱动程序为 oid\_SRIOV\_VF 的 OID 方法请求之一返回以下状态代码之一\_使\_配置\_块无效。

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
<td><p>微型端口驱动程序不支持单根 i/o 虚拟化（SR-IOV）接口，或者未启用使用接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_VF_INVALIDATE_CONFIG_BLOCK_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info)"><strong>NDIS_SRIOV_VF_INVALIDATE_CONFIG_BLOCK_INFO</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 设置<strong>数据。SET_INFORMATION。</strong>将<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的成员 BytesNeeded 到<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_VF_INVALIDATE_CONFIG_BLOCK_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info)"><strong>NDIS_SRIOV_VF_INVALIDATE_CONFIG_BLOCK_INFO</strong></a>结构的大小。</p></td>
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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**IOCTL\_VPCI\_使\_块无效**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_SRIOV\_VF\_使\_配置无效\_块\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info)

[**NdisMInvalidateConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisminvalidateconfigblock)

[OID\_SRIOV\_读取\_VF\_配置\_空间](oid-sriov-read-vf-config-space.md)

[**VPCI\_使\_块\_输出无效**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ns-vpci-_vpci_invalidate_block_output)

 

 




