---
title: 从 PF 微型端口驱动程序进行反向通道通信
description: 从 PF 微型端口驱动程序进行反向通道通信
ms.assetid: 819FC32C-D50C-480F-AE6E-078E4ECD3400
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db02eddd756e45c0c1fd0e68ab23aeb58a175702
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838228"
---
# <a name="backchannel-communication-from-the-pf-miniport-driver"></a>从 PF 微型端口驱动程序进行反向通道通信


PCI Express （PCIe）物理功能（PF）的微型端口驱动程序与 PCIe 虚拟函数（VF）的微型端口驱动程序通信，以发出有关 VF 配置块数据更改的通知。 PF 小型端口驱动程序会发出这些通知，以使 VF 配置块中的数据*无效*。 为响应此通知，VF 微型端口驱动程序可以向 PF 微型端口驱动程序发出 backchannel 请求，以从无效的 VF 配置块中读取数据。

VF 配置块用于 backchannel 和 VF 微型端口驱动程序之间的通信。 IHV 可以为设备定义一个或多个 VF 配置块。 每个 VF 配置块都有一个 IHV 定义的格式、长度和块 ID。

**请注意**，每个 VF 配置块中  的数据仅供 PF 和 VF 微型端口驱动程序使用。 此数据的格式和内容对于 Windows 操作系统的组件是不透明的。

 

发出和处理无效 VF 配置数据的通知时，将执行以下步骤：

1.  在来宾操作系统中，NDIS 发出对 IOCTL\_的 i/o 控制请求[ **\_使\_块无效**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block)。 完成此 IOCTL 后，将通知 NDIS 配置数据已更改。

2.  在 Hyper-v 父分区中运行的管理操作系统中，将执行以下步骤：

    1.  PF 微型端口驱动程序调用[**NdisMInvalidateConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisminvalidateconfigblock)函数，以通知 NDIS VF 配置数据已更改，并且不再有效。 驱动程序将*BlockMask*参数设置为 ULONGLONG 位掩码，该位掩码指定哪些 VF 配置块发生了更改。 位掩码中的每个位对应于一个 VF 配置块。 如果将位设置为1，则相应的 VF 配置块中的数据已更改。
    2.  NDIS 向虚拟化堆栈发出信号，该堆栈在管理操作系统中运行，关于 VF 配置块数据的更改。 虚拟化堆栈缓存*BlockMask*参数数据。

        **请注意**  每次 PF 微型端口驱动程序调用[**NdisMInvalidateConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisminvalidateconfigblock)时，虚拟化堆栈会将*BlockMask*参数数据与缓存中的当前值 or。

         

    3.  虚拟化堆栈会通知虚拟 PCI （VPCI）驱动程序，该驱动程序在来宾操作系统中运行，这与 VF 配置数据的无效有关。 虚拟化堆栈会将缓存的*BlockMask*参数数据发送到 VPCI 驱动程序。

3.  在 Hyper-v 子分区中运行的来宾操作系统中，将执行以下步骤：

    1.  VPCI 驱动程序将缓存的*BlockMask*参数数据保存在 VPCI\_的**BlockMask**成员中会使与[**IOCTL\_VPCI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block) [ **\_块\_输出结构的输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ns-vpci-_vpci_invalidate_block_output)结构无效\_块请求无效。\_

    2.  VPCI 驱动程序已成功完成[**IOCTL\_VPCI\_使\_块请求无效**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block)。 发生这种情况时，NDIS\_SRIOV\_VF 发出 OID 的对象标识符（OID）方法请求， [\_将\_配置\_块无效](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-vf-invalidate-config-block)到 VF 微型端口驱动程序。 [**NDIS\_SRIOV\_VF\_使\_配置\_块无效，\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info)将在 OID 请求中传递。 此结构包含缓存的*BlockMask*参数数据。

        NDIS 还会发出其他[**IOCTL\_VPCI\_使**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block)处理 VF 配置数据更改的连续通知\_块请求无效。

    3.  当 VF 驱动程序处理[OID\_SRIOV\_VF\_使\_配置\_块请求无效](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-vf-invalidate-config-block)时，它可以通过调用[**NdisMReadConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismreadconfigblock)从指定的 VF 配置块中读取数据。 有关此过程的详细信息，请参阅[Backchannel Communication from a VF 微型端口驱动程序](backchannel-communication-from-a-vf-miniport-driver.md)。

 

 





