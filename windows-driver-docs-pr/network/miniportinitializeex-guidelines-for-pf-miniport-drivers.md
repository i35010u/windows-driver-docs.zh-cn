---
title: PF 微型端口驱动程序的 MiniportInitializeEx 指导原则
description: PF 微型端口驱动程序的 MiniportInitializeEx 指导原则
ms.assetid: 338035E7-7677-49FE-A06D-CCFD813B0C10
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 009ba15c94531db6a0169b367b56d40c2e862b0f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844232"
---
# <a name="miniportinitializeex-guidelines-for-pf-miniport-drivers"></a>PF 微型端口驱动程序的 MiniportInitializeEx 指导原则


本主题介绍为 PCI Express （PCIe）物理功能（PF）的微型端口驱动程序编写[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数的准则。 PF 是支持单根 i/o 虚拟化（SR-IOV）的网络适配器组件。

**请注意**  这些准则仅适用于 PF 小型端口驱动程序。 有关适配器的 PCIe 虚拟功能（VF）的微型端口驱动程序的初始化准则，请参阅[初始化 VF 微型端口驱动程序](initializing-a-vf-miniport-driver.md)。

 

当任何 NDIS 微型端口驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数时，PF 微型端口驱动程序将遵循相同的步骤。 有关这些步骤的详细信息，请参阅[初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

除了这些步骤以外，在 NDIS 调用驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数时，PF 微型端口驱动程序还必须执行以下附加步骤：

1.  PF 微型端口驱动程序调用[**NdisGetHypervisorInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgethypervisorinfo)函数来验证它是否正在 hyper-v 父分区中运行。 此函数返回用于定义分区类型的[**NDIS\_虚拟机监控程序\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hypervisor_info)结构。 如果将分区类型报告为**NdisHypervisorPartitionMsHvParent**，则微型端口驱动程序将在附加到适配器上的 PF 的 hyper-v 父分区中运行。

    **注意**  如果将分区类型报告为**NdisHypervisorPartitionMsHvChild**，则微型端口驱动程序将在附加到适配器上的 VF 的 hyper-v 子分区中运行。 在这种情况下，微型端口驱动程序不得初始化为 PF 驱动程序。 如有可能，驱动程序必须初始化为 VF 驱动程序，如[初始化 Vf 微型端口驱动程序](initializing-a-vf-miniport-driver.md)中所述。

     

2.  PF 微型端口驱动程序必须读取 SR-IOV 标准化关键字，以确定是否已启用 SR-IOV 并获取 NIC 交换机配置设置。 有关这些关键字的详细信息，请参阅[sr-iov 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

    **请注意**  如果 PF 微型端口驱动程序已将入口点注册到[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数，则当 NDIS 调用*MiniportSetOptions*时，驱动程序可能以前从注册表获取了这些设置。

     

3.  如果网络适配器支持 SR-IOV、虚拟机队列（VMQ）或 RSS，微型端口驱动程序必须确定要在网络适配器上启用的功能。 有关如何确定此情况的详细信息，请参阅[处理 sr-iov、VMQ 和 RSS 标准化 INF 关键字](handling-sr-iov--vmq--and-rss-standardized-inf-keywords.md)。

4.  除了 RSS 和 VMQ 硬件功能（如果支持），微型端口驱动程序必须报告其完整的硬件 sr-iov 功能集。 无论注册表中的 SR-IOV 标准化关键字设置如何，都必须公布这些功能。

    如果在网络适配器上启用了 SR-IOV，则微型端口驱动程序还必须在适配器上报告 currentlyenabled SR-IOV 设置。

    有关报告 SR-IOV 功能的详细信息，请参阅[确定 Sr-iov 功能](determining-sr-iov-capabilities.md)。

5.  微型端口驱动程序必须报告其整套硬件 NIC 交换机功能。 无论注册表中的 SR-IOV 标准化关键字设置如何，都必须公布这些功能。

    如果在网络适配器上启用了 SR-IOV，则微型端口驱动程序还必须在适配器上报告 currentlyenabled NIC 交换机设置。

    有关如何报告 NIC 交换机功能的详细信息，请参阅[确定 Nic 交换机功能](determining-nic-switch-capabilities.md)。

6.  微型端口驱动程序必须报告其硬件接收筛选功能的完整集。 无论注册表中的 SR-IOV 标准化关键字设置如何，都必须公布这些功能。

    如果在网络适配器上启用了 SR-IOV，则微型端口驱动程序还必须在适配器上报告 currentlyenabled 接收筛选设置。

    有关报告接收筛选功能的详细信息，请参阅[确定接收筛选功能](determining-receive-filtering-capabilities.md)。

7.  如果微型端口驱动程序支持静态 NIC 交换机创建，则必须在调用[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)的上下文中执行以下操作。

    -   驱动程序根据 NIC 交换机标准化关键字设置配置适配器硬件。 根据这些设置，驱动程序将为 NIC 交换机分配必要的硬件和软件资源。

    -   微型端口驱动程序调用[**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)以启用 sr-iov，并在网络适配器上设置 VFs 的数目。 此函数在适配器的 PCI 配置空间中配置 SR-IOV 扩展功能。 如果此函数返回 NDIS\_状态\_SUCCESS，则启用 SR-IOV，并通过 PCIe 接口公开 VFs。

    有关详细信息，请参阅[创建 NIC 交换机的静态](static-creation-of-a-nic-switch.md)。

    **请注意**  如果微型端口驱动程序支持动态 NIC 交换机创建，它将创建开关，并在处理 OID\_\_NIC 的对象标识符（OID）方法请求时启用虚拟化， [\_创建\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)。 有关详细信息，请参阅[动态创建 NIC 交换机](dynamic-creation-of-a-nic-switch.md)。

     

 

 





