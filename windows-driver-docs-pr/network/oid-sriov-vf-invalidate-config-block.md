---
title: OID_SRIOV_VF_INVALIDATE_CONFIG_BLOCK
description: NDIS 发出一个对象标识符 (OID) 方法请求的 OID_SRIOV_VF_INVALIDATE_CONFIG_BLOCK 通知微型端口驱动程序的 PCI Express (PCIe) 虚拟函数 (VF) 的一个或多个配置块内的数据已更改。
ms.assetid: CF73E0DA-20DA-49A0-80B0-0F5A56DCEF5D
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_VF_INVALIDATE_CONFIG_BLOCK 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f335c7a7798bbf74b978956a9c61f9c8ff2466f5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366580"
---
# <a name="oidsriovvfinvalidateconfigblock"></a>OID\_SRIOV\_VF\_INVALIDATE\_配置\_阻止


NDIS 发出对象标识符 (OID) 方法请求的 OID\_SRIOV\_VF\_INVALIDATE\_配置\_块通知微型端口驱动程序的 PCI Express (PCIe) 虚拟函数 (VF) 该数据在一个或多个配置块内已更改。 NDIS 微型端口驱动程序为 PCIe 物理函数 (PF) 调用时发出此 OID [ **NdisMInvalidateConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisminvalidateconfigblock)。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_SRIOV\_VF\_INVALIDATE\_CONFIG\_阻止\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info)结构。 此结构指定其数据已更改一个或多个虚拟函数 (VF) 配置块 (*失效*) PF 微型端口驱动程序。

<a name="remarks"></a>备注
-------

VF 配置块用于 backchannel PF 和 VF 微型端口驱动程序之间的通信。 IHV 可以定义一个或多个 VF 配置块设备。 每个 VF 配置块都有 IHV 定义的格式、 长度和块 id。

**请注意**  仅由 PF 和 VF 微型端口驱动程序使用每个 VF 配置块中的数据。

 

下列驱动程序之间交换 VF 配置数据：

-   VF 驱动程序，在来宾操作系统中运行。 在 HYPER-V 子分区中运行此操作系统。

-   PF 驱动程序，在管理操作系统中运行。 在 HYPER-V 父分区中运行此操作系统。

若要处理的无效 VF 配置数据的通知，NDIS 和微型端口驱动程序执行以下步骤：

1.  在来宾操作系统，NDIS 发出的 I/O 控制请求[ **IOCTL\_VPCI\_INVALIDATE\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/vpci/ni-vpci-ioctl_vpci_invalidate_block)请求。 当完成此 IOCTL 时，NDIS 将通知 VF 配置数据已更改。

2.  在管理操作系统，将执行以下步骤：

    1.  PF 微型端口驱动程序调用[ **NdisMInvalidateConfigBlock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisminvalidateconfigblock)函数，以通知 NDIS VF 配置数据已更改，并将不再有效。 驱动程序集*BlockMask*指定哪些 VF 配置块的 ULONGLONG 位掩码参数已更改。 每一位的位掩码中对应于 VF 配置块。 如果位设置为其中一个，相应 VF 配置块中的数据已更改。
    2.  NDIS 表示虚拟化堆栈，管理在操作系统中运行，有关对 VF 配置块数据的更改。 虚拟化堆栈缓存*BlockMask*参数数据。

        **请注意**  PF 微型端口驱动程序调用每次[ **NdisMInvalidateConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisminvalidateconfigblock)，虚拟化堆栈 Or *BlockMask*与在其缓存中的当前值的参数数据。

         

    3.  虚拟化堆栈通知虚拟 PCI (VPCI) 驱动程序，可以在运行来宾操作系统中，有关 VF 配置数据无效。 虚拟化堆栈发送的已缓存*BlockMask* VPCI 驱动程序的参数数据。

3.  在来宾操作系统，将执行以下步骤：

    1.  VPCI 驱动程序将保存的已缓存*BlockMask*中的参数数据**BlockMask**的成员[ **VPCI\_INVALIDATE\_块\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/vpci/ns-vpci-_vpci_invalidate_block_output)与关联的结构[ **IOCTL\_VPCI\_INVALIDATE\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/vpci/ni-vpci-ioctl_vpci_invalidate_block)请求。

    2.  VPCI 驱动程序已成功完成[ **IOCTL\_VPCI\_INVALIDATE\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/vpci/ni-vpci-ioctl_vpci_invalidate_block)请求。 在此情况下，NDIS 发出 OID 方法请求的 OID\_SRIOV\_VF\_INVALIDATE\_配置\_阻止 VF 微型端口驱动程序。 [ **NDIS\_SRIOV\_VF\_INVALIDATE\_配置\_阻止\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info) OID 请求中传递。 此结构包含的已缓存*BlockMask*参数数据。

        NDIS 也会发出另一个[ **IOCTL\_VPCI\_INVALIDATE\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/vpci/ni-vpci-ioctl_vpci_invalidate_block)处理连续的更改通知给 VF 配置数据的请求。

    3.  如果 VF 驱动程序处理 OID\_SRIOV\_VF\_INVALIDATE\_配置\_块请求，它从读取数据的指定 VF 配置块。

有关单根 I/O 虚拟化 (SR-IOV) 界面内 backchannel 通信的详细信息，请参阅[SR-IOV PF/取景器 Backchannel 通信](https://docs.microsoft.com/windows-hardware/drivers/network/sr-iov-pf-vf-backchannel-communication)。

### <a name="return-status-codes"></a>返回状态代码

微型端口驱动程序将返回一个 OID 的 OID 方法请求的以下状态代码\_SRIOV\_VF\_INVALIDATE\_配置\_阻止。

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
<td><p>一个或多个的成员<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_VF_INVALIDATE_CONFIG_BLOCK_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info)"> <strong>NDIS_SRIOV_VF_INVALIDATE_CONFIG_BLOCK_INFO</strong> </a>结构具有无效值。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 集<strong>数据。SET_INFORMATION。BytesNeeded</strong>中的成员<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>结构的大小<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_VF_INVALIDATE_CONFIG_BLOCK_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info)"> <strong>NDIS_SRIOV_VF_INVALIDATE_CONFIG_BLOCK_INFO</strong></a>结构。</p></td>
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
[**IOCTL\_VPCI\_INVALIDATE\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/vpci/ni-vpci-ioctl_vpci_invalidate_block)

[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_SRIOV\_VF\_INVALIDATE\_CONFIG\_阻止\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info)

[**NdisMInvalidateConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisminvalidateconfigblock)

[OID\_SRIOV\_读取\_VF\_配置\_空间](oid-sriov-read-vf-config-space.md)

[**VPCI\_INVALIDATE\_阻止\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/vpci/ns-vpci-_vpci_invalidate_block_output)

 

 




