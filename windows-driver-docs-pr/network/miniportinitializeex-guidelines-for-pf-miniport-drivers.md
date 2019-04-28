---
title: PF 微型端口驱动程序的 MiniportInitializeEx 指导原则
description: PF 微型端口驱动程序的 MiniportInitializeEx 指导原则
ms.assetid: 338035E7-7677-49FE-A06D-CCFD813B0C10
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b19b82c301bf078459699dbbe253f93c1af040f7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354621"
---
# <a name="miniportinitializeex-guidelines-for-pf-miniport-drivers"></a>PF 微型端口驱动程序的 MiniportInitializeEx 指导原则


本主题介绍进行写入的准则[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)微型端口驱动程序的 PCI Express (PCIe) 物理函数 (PF) 的函数。 PF 是支持单根 I/O 虚拟化 (SR-IOV) 的网络适配器的组件。

**请注意**  这些指南仅适用于 PF 微型端口驱动程序。 微型端口驱动程序的 PCIe 虚拟函数 (VF) 的适配器的初始化准则，请参阅[初始化 VF 微型端口驱动程序](initializing-a-vf-miniport-driver.md)。

 

PF 微型端口驱动程序遵循相同的步骤为任何 NDIS 微型端口驱动程序时其[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数。 有关这些步骤的详细信息，请参阅[初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

除了这些步骤中，PF 微型端口驱动程序时必须遵守下列附加步骤 NDIS 调用驱动程序的[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数：

1.  PF 微型端口驱动程序调用[ **NdisGetHypervisorInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff562635)函数来验证它是否正在运行的 HYPER-V 父分区中。 此函数将返回[ **NDIS\_虚拟机监控程序\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff565708)结构，它定义的分区类型。 如果分区类型将报告为**NdisHypervisorPartitionMsHvParent**，微型端口驱动程序运行附加到在适配器上 PF 在 HYPER-V 父分区中。

    **请注意**  如果分区类型将报告为**NdisHypervisorPartitionMsHvChild**，微型端口驱动程序是否正在附加到 VF 在适配器上的 HYPER-V 子分区。 在这种情况下，作为 PF 驱动程序必须初始化微型端口驱动程序。 如果可能，该驱动程序必须将初始化为某个 VF 驱动程序中所述[初始化 VF 微型端口驱动程序](initializing-a-vf-miniport-driver.md)。

     

2.  PF 微型端口驱动程序必须读取要确定是否启用 SR-IOV，并获取配置设置的 NIC 交换机的 SR-IOV 标准化关键字。 有关这些关键字的详细信息，请参阅[SR-IOV 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

    **请注意**  PF 微型端口驱动程序如果注册的入口点[ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)函数，该驱动程序可能已以前获得了这些设置注册表 NDIS 调用时*MiniportSetOptions*。

     

3.  如果网络适配器支持 SR-IOV、 虚拟机队列 (VMQ) 或 RSS，微型端口驱动程序必须确定哪种功能的网络适配器上启用。 有关如何确定这一点的详细信息，请参阅[处理 SR-IOV、 VMQ 和 RSS 标准化 INF 关键字](handling-sr-iov--vmq--and-rss-standardized-inf-keywords.md)。

4.  RSS 和 VMQ 硬件功能 （如果支持），以及的微型端口驱动程序必须报告其完整的硬件的 SR-IOV 功能集。 这些功能必须播发在注册表中的 SR-IOV 标准化关键字设置无关。

    如果网络适配器上启用了 SR-IOV，微型端口驱动程序还必须在适配器上报告 currentlyenabled 的 SR-IOV 设置。

    报告的 SR-IOV 功能的详细信息，请参阅[确定的 SR-IOV 功能](determining-sr-iov-capabilities.md)。

5.  微型端口驱动程序必须报告其完整的 NIC 的硬件交换机功能集。 这些功能必须播发在注册表中的 SR-IOV 标准化关键字设置无关。

    如果网络适配器上启用了 SR-IOV，微型端口驱动程序还必须在适配器上报告 currentlyenabled NIC 交换机设置。

    有关详细信息报告 NIC 上切换功能，请参阅[确定 NIC 切换功能](determining-nic-switch-capabilities.md)。

6.  微型端口驱动程序必须报告其完整的硬件设置接收的筛选功能。 这些功能必须播发在注册表中的 SR-IOV 标准化关键字设置无关。

    如果网络适配器上启用了 SR-IOV，微型端口驱动程序还必须报告 currentlyenabled 接收适配器上的筛选设置。

    报告接收筛选功能的详细信息，请参阅[确定收到的筛选功能](determining-receive-filtering-capabilities.md)。

7.  如果微型端口驱动程序支持静态 NIC 交换机创建，它必须执行以下操作的调用上下文中[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)。

    -   该驱动程序配置基于 NIC 交换机标准化关键字设置适配器硬件。 根据这些设置，则驱动程序为 NIC 开关分配所需的硬件和软件资源。

    -   微型端口驱动程序调用[ **NdisMEnableVirtualization** ](https://msdn.microsoft.com/library/windows/hardware/hh451481)启用 SR-IOV 和网络适配器上设置的 VFs 数。 此函数适配器的 PCI 配置空间中配置的 SR-IOV 扩展功能。 如果此函数返回 NDIS\_状态\_成功后，启用 SR-IOV 和 VFs 公开通过 PCIe 接口。

    有关详细信息，请参阅[静态创建的 NIC 交换机](static-creation-of-a-nic-switch.md)。

    **请注意**  如果微型端口驱动程序支持动态 NIC 交换机创建，它创建了交换机和它处理的对象标识符 (OID) 方法请求时，可以实现虚拟化[OID\_NIC\_交换机\_创建\_交换机](https://msdn.microsoft.com/library/windows/hardware/hh451815)。 有关详细信息，请参阅[动态创建的 NIC 交换机](dynamic-creation-of-a-nic-switch.md)。

     

 

 





