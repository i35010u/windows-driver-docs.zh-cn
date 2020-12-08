---
title: OID_SRIOV_VF_INVALIDATE_CONFIG_BLOCK
description: NDIS (OID 发出对象标识符) 方法请求 OID_SRIOV_VF_INVALIDATE_CONFIG_BLOCK，以通知 PCI Express (PCIe) 虚拟函数 (虚拟函数的微型端口驱动程序) 虚拟一个或多个配置块中的数据已更改。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_VF_INVALIDATE_CONFIG_BLOCK 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e4ebd32a3a9410b435484be038e997e040470621
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812965"
---
# <a name="oid_sriov_vf_invalidate_config_block"></a>OID \_ SRIOV \_ VF \_ 使 \_ 配置 \_ 块无效


NDIS (oid 发出对象标识符) 方法请求 OID \_ SRIOV \_ vf \_ 使 \_ CONFIG 块无效 \_ ，以通知 PCI Express (PCIe 的微型端口驱动程序) 虚函数 (VF) 一个或多个配置块中的数据已更改。 当 PCIe 物理功能的微型端口驱动程序 (PF) 调用 [**NdisMInvalidateConfigBlock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisminvalidateconfigblock)时，NDIS 会发出此 OID。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 ndis SRIOV VF 的指针，该指针会 [**\_ \_ \_ 使 \_ 配置 \_ 块 \_ 信息结构无效**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info)。 此结构指定了一个或多个虚拟函数 (VF) 配置块，这些配置块的数据已更改 (无效，而 PF 微型端口驱动程序) *失效* 。

<a name="remarks"></a>备注
-------

VF 配置块用于 backchannel 和 VF 微型端口驱动程序之间的通信。 IHV 可以为设备定义一个或多个 VF 配置块。 每个 VF 配置块都有一个 IHV 定义的格式、长度和块 ID。

**注意**  每个 VF 配置块中的数据仅用于 PF 和 VF 微型端口驱动程序。

 

VF 配置数据在以下驱动程序之间交换：

-   在来宾操作系统中运行的 VF 驱动程序。 此操作系统在 Hyper-v 子分区中运行。

-   PF 驱动程序，它在管理操作系统中运行。 此操作系统在 Hyper-v 父分区中运行。

为了处理无效 VF 配置数据的通知，NDIS 和微型端口驱动程序执行以下步骤：

1.  在来宾操作系统中，NDIS 发出对 [**IOCTL \_ VPCI \_ 无效 \_ 块**](/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block) 请求的 i/o 控制请求。 完成此 IOCTL 后，将通知 NDIS 配置数据已更改。

2.  在管理操作系统中，将执行以下步骤：

    1.  PF 微型端口驱动程序调用 [**NdisMInvalidateConfigBlock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisminvalidateconfigblock) 函数，以通知 NDIS VF 配置数据已更改，并且不再有效。 驱动程序将 *BlockMask* 参数设置为 ULONGLONG 位掩码，该位掩码指定哪些 VF 配置块发生了更改。 位掩码中的每个位对应于一个 VF 配置块。 如果将位设置为1，则相应的 VF 配置块中的数据已更改。
    2.  NDIS 向虚拟化堆栈发出信号，该堆栈在管理操作系统中运行，关于 VF 配置块数据的更改。 虚拟化堆栈缓存 *BlockMask* 参数数据。

        **注意**  每次 PF 微型端口驱动程序调用 [**NdisMInvalidateConfigBlock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisminvalidateconfigblock)时，虚拟化堆栈会将 *BlockMask* 参数数据与缓存中的当前值 or。

         

    3.  虚拟化堆栈会通知虚拟 PCI (VPCI) 驱动程序，该驱动程序在来宾操作系统中运行，这与 VF 配置数据的无效有关。 虚拟化堆栈会将缓存的 *BlockMask* 参数数据发送到 VPCI 驱动程序。

3.  在来宾操作系统中，将执行以下步骤：

    1.  VPCI 驱动程序将缓存的 *BlockMask* 参数数据保存在与 [**IOCTL \_ VPCI 无效 \_ \_ Block**](/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block)请求关联的 [**VPCI \_ \_ \_**](/windows-hardware/drivers/ddi/vpci/ns-vpci-_vpci_invalidate_block_output)的 **BlockMask** 成员中。

    2.  VPCI 驱动程序已成功完成 [**IOCTL \_ VPCI \_ 无效 \_ 块**](/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block) 请求。 发生这种情况时，NDIS 会发出 OID 的 OID 方法请求， \_ SRIOV \_ vf 会 \_ 使 \_ 配置 \_ 块无效，从而导致 VF 微型端口驱动程序。 在 OID 请求中， [**NDIS \_ SRIOV \_ VF 会 \_ 使 \_ 配置 \_ 块 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info) 无效。 此结构包含缓存的 *BlockMask* 参数数据。

        NDIS 还会发出其他 [**IOCTL \_ VPCI \_ 无效 \_ 块**](/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block) 请求来处理对 VF 配置数据所做的更改的连续通知。

    3.  当 VF 驱动程序处理 OID \_ SRIOV \_ VF \_ 使 \_ CONFIG 块请求无效时 \_ ，它将读取指定的 VF 配置块中的数据。

有关 backchannel) 接口 (的单个根 i/o 虚拟化内的通信的详细信息，请参阅 [SR-IOV PF/VF Backchannel 通信](./sr-iov-pf-vf-backchannel-communication.md)。

### <a name="return-status-codes"></a>返回状态代码

对于 OID \_ SRIOV \_ VF \_ 使 \_ CONFIG \_ 块无效的 oid 方法请求，微型端口驱动程序返回以下状态代码之一。

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
<td><p><a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_VF_INVALIDATE_CONFIG_BLOCK_INFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info)"><strong>NDIS_SRIOV_VF_INVALIDATE_CONFIG_BLOCK_INFO</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 设置 <strong>数据。SET_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 到 <a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_VF_INVALIDATE_CONFIG_BLOCK_INFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info)"><strong>NDIS_SRIOV_VF_INVALIDATE_CONFIG_BLOCK_INFO</strong></a> 结构的大小。</p></td>
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

## <a name="see-also"></a>请参阅


****
[**IOCTL \_ VPCI \_ 无效 \_ 块**](/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ SRIOV \_ VF \_ 使 \_ 配置 \_ 块 \_ 信息无效**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info)

[**NdisMInvalidateConfigBlock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisminvalidateconfigblock)

[OID \_ SRIOV \_ 读取 \_ VF \_ 配置 \_ 空间](oid-sriov-read-vf-config-space.md)

[**VPCI \_ 无效的 \_ 块 \_ 输出**](/windows-hardware/drivers/ddi/vpci/ns-vpci-_vpci_invalidate_block_output)

