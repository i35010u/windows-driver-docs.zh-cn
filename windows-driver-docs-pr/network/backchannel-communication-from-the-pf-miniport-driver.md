---
title: 从 PF 微型端口驱动程序进行反向通道通信
description: 从 PF 微型端口驱动程序进行反向通道通信
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e4f42e557bed2ea6a512a30069b545b896ecba0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813021"
---
# <a name="backchannel-communication-from-the-pf-miniport-driver"></a>从 PF 微型端口驱动程序进行反向通道通信


PCI Express (PCIe) 物理功能 (PF 的微型端口驱动程序) 与 PCIe 虚拟函数的微型端口驱动程序通信 (VF) 来发出有关 VF 配置块数据更改的通知。 PF 小型端口驱动程序会发出这些通知，以使 VF 配置块中的数据 *无效* 。 为响应此通知，VF 微型端口驱动程序可以向 PF 微型端口驱动程序发出 backchannel 请求，以从无效的 VF 配置块中读取数据。

VF 配置块用于 backchannel 和 VF 微型端口驱动程序之间的通信。 IHV 可以为设备定义一个或多个 VF 配置块。 每个 VF 配置块都有一个 IHV 定义的格式、长度和块 ID。

**注意**  每个 VF 配置块中的数据仅用于 PF 和 VF 微型端口驱动程序。 此数据的格式和内容对于 Windows 操作系统的组件是不透明的。

 

发出和处理无效 VF 配置数据的通知时，将执行以下步骤：

1.  在来宾操作系统中，NDIS 发出对 [**IOCTL \_ VPCI \_ 无效 \_ 块**](/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block)的 i/o 控制请求。 完成此 IOCTL 后，将通知 NDIS 配置数据已更改。

2.  在 Hyper-v 父分区中运行的管理操作系统中，将执行以下步骤：

    1.  PF 微型端口驱动程序调用 [**NdisMInvalidateConfigBlock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisminvalidateconfigblock) 函数，以通知 NDIS VF 配置数据已更改，并且不再有效。 驱动程序将 *BlockMask* 参数设置为 ULONGLONG 位掩码，该位掩码指定哪些 VF 配置块发生了更改。 位掩码中的每个位对应于一个 VF 配置块。 如果将位设置为1，则相应的 VF 配置块中的数据已更改。
    2.  NDIS 向虚拟化堆栈发出信号，该堆栈在管理操作系统中运行，关于 VF 配置块数据的更改。 虚拟化堆栈缓存 *BlockMask* 参数数据。

        **注意**  每次 PF 微型端口驱动程序调用 [**NdisMInvalidateConfigBlock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisminvalidateconfigblock)时，虚拟化堆栈会将 *BlockMask* 参数数据与缓存中的当前值 or。

         

    3.  虚拟化堆栈会通知虚拟 PCI (VPCI) 驱动程序，该驱动程序在来宾操作系统中运行，这与 VF 配置数据的无效有关。 虚拟化堆栈会将缓存的 *BlockMask* 参数数据发送到 VPCI 驱动程序。

3.  在 Hyper-v 子分区中运行的来宾操作系统中，将执行以下步骤：

    1.  VPCI 驱动程序将缓存的 *BlockMask* 参数数据保存在与 [**IOCTL \_ VPCI 无效 \_ \_ Block**](/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block)请求关联的 [**VPCI \_ \_ \_**](/windows-hardware/drivers/ddi/vpci/ns-vpci-_vpci_invalidate_block_output)的 **BlockMask** 成员中。

    2.  VPCI 驱动程序已成功完成 [**IOCTL \_ VPCI \_ 无效 \_ 块**](/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block) 请求。 发生这种情况时，NDIS) 方法请求 (oid 发出对象标识符，而 oid [ \_ SRIOV \_ VF 会 \_ 使 \_ 配置 \_ 块无效](./oid-sriov-vf-invalidate-config-block.md) 到 VF 微型端口驱动程序。 在 OID 请求中， [**NDIS \_ SRIOV \_ VF 会 \_ 使 \_ 配置 \_ 块 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info) 无效。 此结构包含缓存的 *BlockMask* 参数数据。

        NDIS 还会发出其他 [**IOCTL \_ VPCI \_ 无效 \_ 块**](/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block) 请求来处理对 VF 配置数据所做的更改的连续通知。

    3.  当 VF 驱动程序处理 [OID \_ SRIOV \_ VF \_ 使 \_ CONFIG \_ 块请求无效](./oid-sriov-vf-invalidate-config-block.md) 时，它可以通过调用 [**NdisMReadConfigBlock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismreadconfigblock)从指定的 VF 配置块中读取数据。 有关此过程的详细信息，请参阅 [Backchannel Communication from a VF 微型端口驱动程序](backchannel-communication-from-a-vf-miniport-driver.md)。

 

