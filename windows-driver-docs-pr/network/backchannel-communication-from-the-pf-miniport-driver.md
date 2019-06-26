---
title: 从 PF 微型端口驱动程序进行反向通道通信
description: 从 PF 微型端口驱动程序进行反向通道通信
ms.assetid: 819FC32C-D50C-480F-AE6E-078E4ECD3400
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65ae9488cc0be43e8c91e0fcef2d67418c30e84f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384401"
---
# <a name="backchannel-communication-from-the-pf-miniport-driver"></a>从 PF 微型端口驱动程序进行反向通道通信


微型端口驱动程序的 PCI Express (PCIe) 物理函数 (PF) 与微型端口驱动程序的 PCIe 虚拟函数 (VF) VF 配置块的有关数据中的更改将问题通知进行通信。 PF 微型端口驱动程序将发出对这些通知*失效*VF 配置块中的数据。 在响应此通知，VF 微型端口驱动程序可以发出 backchannel 请求到 PF 微型端口驱动程序，从失效的 VF 配置块读取数据。

VF 配置块用于 backchannel PF 和 VF 微型端口驱动程序之间的通信。 IHV 可以定义一个或多个 VF 配置块设备。 每个 VF 配置块都有 IHV 定义的格式、 长度和块 id。

**请注意**  仅由 PF 和 VF 微型端口驱动程序使用每个 VF 配置块中的数据。 格式和内容的此数据是不透明的 Windows 操作系统组件。

 

颁发和处理通知 VF 配置数据无效时，将执行以下步骤：

1.  在来宾操作系统，NDIS 发出的 I/O 控制请求[ **IOCTL\_VPCI\_INVALIDATE\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/vpci/ni-vpci-ioctl_vpci_invalidate_block)。 当完成此 IOCTL 时，NDIS 将通知 VF 配置数据已更改。

2.  管理操作系统中运行的 HYPER-V 父分区中，将执行以下步骤：

    1.  PF 微型端口驱动程序调用[ **NdisMInvalidateConfigBlock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisminvalidateconfigblock)函数，以通知 NDIS VF 配置数据已更改，并将不再有效。 驱动程序集*BlockMask*指定哪些 VF 配置块的 ULONGLONG 位掩码参数已更改。 每一位的位掩码中对应于 VF 配置块。 如果位设置为其中一个，相应 VF 配置块中的数据已更改。
    2.  NDIS 表示虚拟化堆栈，管理在操作系统中运行，有关对 VF 配置块数据的更改。 虚拟化堆栈缓存*BlockMask*参数数据。

        **请注意**  PF 微型端口驱动程序调用每次[ **NdisMInvalidateConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisminvalidateconfigblock)，虚拟化堆栈 Or *BlockMask*与在其缓存中的当前值的参数数据。

         

    3.  虚拟化堆栈通知虚拟 PCI (VPCI) 驱动程序，可以在运行来宾操作系统中，有关 VF 配置数据无效。 虚拟化堆栈发送的已缓存*BlockMask* VPCI 驱动程序的参数数据。

3.  来宾操作系统中运行 HYPER-V 子分区中，将执行以下步骤：

    1.  VPCI 驱动程序将保存的已缓存*BlockMask*中的参数数据**BlockMask**的成员[ **VPCI\_INVALIDATE\_块\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/vpci/ns-vpci-_vpci_invalidate_block_output)与关联的结构[ **IOCTL\_VPCI\_INVALIDATE\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/vpci/ni-vpci-ioctl_vpci_invalidate_block)请求。

    2.  VPCI 驱动程序已成功完成[ **IOCTL\_VPCI\_INVALIDATE\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/vpci/ni-vpci-ioctl_vpci_invalidate_block)请求。 当发生这种情况时，NDIS 发出的对象标识符 (OID) 方法请求[OID\_SRIOV\_VF\_INVALIDATE\_CONFIG\_阻止](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-vf-invalidate-config-block)VF 微型端口驱动程序。 [ **NDIS\_SRIOV\_VF\_INVALIDATE\_配置\_阻止\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info) OID 请求中传递。 此结构包含的已缓存*BlockMask*参数数据。

        NDIS 也会发出另一个[ **IOCTL\_VPCI\_INVALIDATE\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/vpci/ni-vpci-ioctl_vpci_invalidate_block)处理连续的更改通知给 VF 配置数据的请求。

    3.  如果 VF 驱动程序处理[OID\_SRIOV\_VF\_INVALIDATE\_CONFIG\_阻止](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-vf-invalidate-config-block)请求，它可以从指定 VF 配置块按读取数据调用[ **NdisMReadConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismreadconfigblock)。 有关此过程的详细信息，请参阅[VF 微型端口驱动程序从 Backchannel 通信](backchannel-communication-from-a-vf-miniport-driver.md)。

 

 





