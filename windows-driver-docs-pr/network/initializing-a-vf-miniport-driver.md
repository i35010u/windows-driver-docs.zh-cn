---
title: 初始化 VF 微型端口驱动程序
description: 初始化 VF 微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cbb8216aee0b299ef7794f8f473bd0da7545487
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832231"
---
# <a name="initializing-a-vf-miniport-driver"></a>初始化 VF 微型端口驱动程序


本主题介绍了为 PCI Express (PCIe) 虚函数 (VF) 编写小型端口驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数的准则。 VF 通过支持单个根 i/o 虚拟化 (SR-IOV) 的网络适配器公开。

> [!NOTE]
> 这些准则仅适用于 SR-IOV 网络适配器的 VF 微型端口驱动程序。 有关 PCIe 物理功能的微型端口驱动程序 (PF) 适配器的初始化准则，请参阅 [初始化 Pf 微型端口驱动程序](initializing-a-pf-miniport-driver.md)。 

调用 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数时，VF 微型端口驱动程序与任何 NDIS 微型端口驱动程序遵循相同的步骤。 有关这些步骤的详细信息，请参阅 [初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

除了这些步骤以外，在 NDIS 调用驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数时，VF 微型端口驱动程序还必须执行以下附加步骤：

- VF 微型端口驱动程序调用 [**NdisGetHypervisorInfo**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgethypervisorinfo) 函数来验证它是否正在 hyper-v 子分区中运行。 此函数返回用于定义分区类型的 [**NDIS \_ 虚拟机监控程序 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hypervisor_info) 结构。 如果将分区类型报告为 **NdisHypervisorPartitionMsHvChild**，则微型端口驱动程序将在附加到适配器上的 PF 的 hyper-v 子分区中运行。

  > [!NOTE] 
  > 如果将分区类型报告为 **NdisHypervisorPartitionMsHvParent**，则微型端口驱动程序将在附加到适配器上的 PF 的 hyper-v 父分区中运行。 在这种情况下，微型端口驱动程序不得初始化为 VF 驱动程序。 如果可能，驱动程序必须初始化为 pf 驱动程序，如 [Pf 小型端口驱动程序的初始化顺序](initialization-sequence-for-pf-miniport-drivers.md)中所述。     

- 与 PF 小型端口驱动程序不同，VF 微型端口驱动程序不得与 SR-IOV 标准化关键字一起安装，并且不能尝试读取这些关键字。 有关这些关键字的详细信息，请参阅 [sr-iov 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

- VF 微型端口驱动程序通过以下方式初始化的 [**NDIS \_ SRIOV \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities) 结构报告基础虚拟网络适配器的 sr-iov 硬件功能：

  1. 微型端口驱动程序初始化 **标头** 成员。 驱动程序将 **标头** 的 **类型** 成员设置为 NDIS \_ 对象 \_ 类型 \_ 默认值。

     从 NDIS 6.30 开始，微型端口驱动程序会将 **标头** 的 **修订** 成员设置为 ndis \_ SRIOV \_ 功能 \_ 修订版本 \_ 1，并将 **Size** 成员设置为 ndis \_ SIZEOF \_ SRIOV \_ 功能 \_ 修订版本 \_ 1。

  2. 微型端口驱动程序 \_ \_ \_ 在 SriovCapabilities 成员中设置 NDIS SRIOV cap PF \_ 微端口标志，以报告 sr-iov 功能。 **SriovCapabilities**

     > [!NOTE]
     > VF 微型端口驱动程序必须同时设置 NDIS \_ SRIOV \_ cap \_ VF \_ 微型端口标志和 ndis \_ SRIOV \_ cap \_ SRIOV \_ 支持的标志。         

  VF 微型端口驱动程序通过执行以下步骤，注册网络适配器的 SR-IOV 功能：

  1.  微型端口驱动程序初始化 [**NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 辅助 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes) 结构。

      微型端口驱动程序将 **HardwareSriovCapabilities** 和 **CurrentSriovCapabilities** 成员设置为指向 previouslyinitialized [**NDIS \_ SRIOV \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities) 结构的指针。

  2.  驱动程序调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) ，并将 *MiniportAttributes* 参数设置为指向 [**NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 协助 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes) 结构的指针。

- VF 微型端口驱动程序不得 (VMQ) 功能播发虚拟机队列。 但是，驱动程序可以为其他 NDIS 技术（例如，电源管理和接收方缩放 (RSS) ）公布支持。

  有关 RSS 的详细信息，请参阅 [接收方缩放](./receive-side-scaling-version-2-rssv2-.md)。

 

